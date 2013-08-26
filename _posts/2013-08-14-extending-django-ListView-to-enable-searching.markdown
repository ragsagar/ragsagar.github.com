---
layout: post
title: "Extending django ListView for enabling search"
date: 2013-08-14 22:00:00
categories: django
tags: django ListView Search CBV
published: true 
---

You have a dozen of views for listing Model objects. One day your client wants to
add search into every page which are listing objects. Nightmare!! I had a couple of views like this
which lists the objects in a table. I was happy with what provided by the
django's generic `ListView`. I just had to inherit from it and define the model and
template. So i didn't want to give away this comfort. I just wanted the the same function,
with search enabled on certain fields defined. This is where we can make use of the real
power of django's class based views. There is a method `get_queryset` in
`ListView` which returns the list of all objects in the given model. By
overriding this method, instead of returning all objects we can do the
filtering based on the search term passed as get parameter and return the subset.
The rest will work as it is :)

{% highlight python %}
from django.views.generic.list import ListView

class ListSearchView(ListView):
    """
    This is a view that can be inherited from to add search functionality to a
    ListView.
    An extra context variable `query_string` will be available in template.
    This can be used to print the search string.
    """
    order_by_field = None
    search_fields = []

    def get_order_by_field(self):
        """
        Get the field by which the results will be ordered.
        If `order_by_field` is not defined no ordering will be done.
        """
        return self.order_by_field

    def get_search_fields(self):
        """
        Return the fields in table to search for.
        """
        return self.search_fields

    def get_queryset(self):
        """
        Get the query string from url and find the items from the database.
        """
        self.query_string = ''
        found_items = None
        queryset = super(ListSearchView, self).get_queryset()
        # Check if query string is there in get, otherwise just return the
        # queryset.
        if ('q' in self.request.GET) and self.request.GET['q'].strip():
            self.query_string = self.request.GET['q']
            # Q object made by ORing search fields
            entry_query = get_query(self.query_string, self.get_search_fields())
            found_items = queryset.filter(entry_query)
            # Order if order_by field is given
            order_by_field = self.get_order_by_field()
            if order_by_field:
                found_items = found_items.order_by('%s' % order_by_field)
            return found_items
        else:
            return queryset

    def get_context_data(self, **kwargs):
        """
        Update the context data with query_string.
        """
        kwargs.update({'query_string': self.query_string})
        return super(ListSearchView, self).get_context_data(**kwargs)

{% endhighlight %}

This view depends on the [`get_query` method by Julien Phalip](http://julienphalip.com/post/2825034077/adding-search-to-a-django-site-in-a-snap).
On providing the search term and the fields to search it will return a
combination of Q objects which can be passed to Queryset's filter method for
filtering it. 

{% highlight python %}

import re
from django.db.models import Q

def normalize_query(query_string,
                    findterms=re.compile(r'"([^"]+)"|(\S+)').findall,
                    normspace=re.compile(r'\s{2,}').sub):
    """
        Splits the query string in invidual keywords, getting rid of unecessary spaces
        and grouping quoted words together.
        Example:
        
        >>> normalize_query('  some random  words "with   quotes  " and   spaces')
        ['some', 'random', 'words', 'with quotes', 'and', 'spaces']
    
    """
    return [normspace(' ', (t[0] or t[1]).strip()) for t in findterms(query_string)] 

def get_query(query_string, search_fields):
    """
        Returns a query, that is a combination of Q objects. That combination
        aims to search keywords within a model by testing the given search fields.
    """
    query = None # Query to search for every search term        
    terms = normalize_query(query_string)
    for term in terms:
        or_query = None # Query to search for a given term in each field
        for field_name in search_fields:
            q = Q(**{"%s__icontains" % field_name: term})
            if or_query is None:
                or_query = q
            else:
                or_query = or_query | q
        if query is None:
            query = or_query
        else:
            query = query & or_query
    return query

{% endhighlight %}

Now you can extend `ListSearchView` instead of generic `ListView` to support search in
your views like this.

{% highlight python %}

class ContactListView(ListSearchView):
    model = Contact
    template_name = 'list_contacts.html'
    search_fields = ['first_name', 'last_name']

{% endhighlight %}

`ListSearchView` also injects the search term into the context data. So in
template you can check if `query_string` exists and add messages like the
following.

{% highlight python %}
{% raw %}
{% if query_string %}
Search results for <strong>{{ query_string }}</strong> in My Contacts
{% endif %}
{% endraw %}
{% endhighlight %}

You can add search box like the following, So when the user is searching,
the search term will be filled in the textbox, If there is no search term
it will show the placeholder 'Search'.

{% highlight python %}
<form class="navbar-search pull-left" method="GET" action="">
    <input type="text" value="{% raw %}{{ query_string }}{% endraw %}" placeholder="Search" name="q">
</form>
{% endhighlight %}
