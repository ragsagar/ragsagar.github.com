Making a field in a django admin form visible or invisible depending on the user
################################################################################
:date: 2012-05-09 22:52
:category: django, Howtos, Python
:tags: add_view, django admin, django form, Python

While i was working on the project `onspot\_v2`_, i came across with a
specific need. `onspot\_v2`_ makes use of the django admin interface for
data entry. When employees are entering data, 'branch' field in the form
will get populated automatically as per the branch of the employee. When
a manager is entering data using the form, an extra field should appear
to select the 'branch' instead of automatically populating. Googling
didn't help much. Finally i thought of overriding the
`ModelAdmin.add\_view()`_ method which is invoked when you try to add an
entry using the admin. I changed the editable property of the field
'branch' inside after checking the request.user and it worked out. Part
of my code in admin.py [sourcecode language="python"] from
django.contrib import admin from books.models import Agent, PolicyIssue
class PolicyIssueAdmin(admin.ModelAdmin): def add\_view(self, request,
form\_url='', extra\_context=None): if
request.user.get\_profile().is\_employee:
self.model.branch.field.editable = False else:
self.model.branch.field.editable = True return super(PolicyIssueAdmin,
self).add\_view(request, form\_url) admin.site.register(PolicyIssue,
PolicyIssueAdmin) [/sourcecode]

.. _onspot\_v2: https://github.com/ragsagar/onspot_v2
.. _ModelAdmin.add\_view(): https://docs.djangoproject.com/en/dev/ref/contrib/admin/#django.contrib.admin.ModelAdmin.add_view
