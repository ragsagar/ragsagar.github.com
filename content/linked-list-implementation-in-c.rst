Linked list implementation in C
###############################
:date: 2009-11-26 18:46
:category: My_Works, Scripts
:tags: C, data structures, linked list

Just thought of sharing the code i written to learn linked list
implementation the day before my data structures model practical exam.
[sourcecode language="python"] /\* \* linkedlist.c \* \* Copyright 2009
Rag Sagar.V <ragsagar@gmail.com> \* \* This program is free software;
you can redistribute it and/or modify \* it under the terms of the GNU
General Public License as published by \* the Free Software Foundation;
either version 2 of the License, or \* (at your option) any later
version. \* \* This program is distributed in the hope that it will be
useful, \* but WITHOUT ANY WARRANTY; without even the implied warranty
of \* MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the \*
GNU General Public License for more details. \* \* You should have
received a copy of the GNU General Public License \* along with this
program; if not, write to the Free Software \* Foundation, Inc., 51
Franklin Street, Fifth Floor, Boston, \* MA 02110-1301, USA. \*/
#include <stdio.h> #include <stdlib.h> typedef struct list { int data;
struct list \*next; }LIST; LIST \*ptr,\*temp,\*start=NULL; void
insert\_after(int ,int ); void remove\_item(int ); void display(void);
int count=0; int main() { int item,opt,dat; system("clear"); ptr=NULL;
/\* printf("%d",sizeof(LIST)); \*/ do { printf("\\n########## MENU
##########\\n"); printf("1.Insert\\n2.Remove\\n3.Display\\n4.Exit\\n");
printf("Enter your option : "); scanf("%d",&opt); switch(opt) { case 1:
printf("Enter the data to insert "); scanf("%d",&item); if(count==0) {
ptr = (LIST \*)malloc(sizeof(LIST)); ptr->next = NULL; ptr->data = item;
start = ptr; } else { printf("Enter the item after which you have to
insert new element : "); scanf("%d",&dat); insert\_after(dat,item); }
count++; break; case 2: if(count==0) { printf("\\nList is empty\\n");
break; } printf("Enter the item to remove : "); scanf("%d",&item);
remove\_item(item); count--; break; case 3: if(count==0) {
printf("\\nList is empty\\n"); break; } else { printf("List elements are
\\n"); display(); } break; case 4: break; } }while(opt!=4); return 0; }
void insert\_after(int data, int item) { LIST \*tmp; temp=(LIST
\*)malloc(sizeof(LIST)); temp->data=item; ptr=start; while(ptr!=NULL) {
if(ptr->data==data) { tmp=ptr->next; ptr->next=temp; temp->next=tmp;
break; } ptr=ptr->next; } } void remove\_item(int item) { ptr=start;
if(ptr->data == item) { start = ptr->next; free(ptr); }
while(ptr->next!=NULL) { if((ptr->next)->data==item) { temp=ptr->next;
ptr->next=(ptr->next)->next; free(temp); break; } ptr=ptr->next; } }
void display() { ptr = start; while(ptr!=NULL) { printf("%d ->
",ptr->data); ptr=ptr->next; } } [/sourcecode]
