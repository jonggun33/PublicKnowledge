# GTD (Get Things Done) via Notion

Around year 2019, I became very interested in the memo app, Notion, and converted my scattered writings into a heap of Notion pages. 

In the course of over one year of trying to do everything with it, the cons of the tool got apparent, eventually forcing me to abandon it for conglomerate of (GitHub, OneNote, Apple Note).

Last Week, Youtube recommended GTD implemented with Notion, which re-sparked my interest not only in Notion but also in the GTD. 

I decided to give it a try mainly after watching Khe Hy's hour-long introduction on both subject (https://www.youtube.com/watch?v=4YspgkLRsrs).

This is to share the essense of GTD that I coudl grasp from it.

## What is GTD?

The GTD is a method for capturing to-do list and putting them in a system in which you are enforced to revisit them with certain frequency eventually letting you tick out the majority of them.

It dictates 5 steps for doding so:

. Capture
. Clarify
. Organize
. Review
. Engage

Capture:: is for catching any idea occurs to you, GTD preaches unless you materialize them in any form, your brain spends some amount of energy to keep them in it, inhibiting occuring of other idea
clarify:: is for making the to-do item accurate. If you captured the idea as "bookmark", you should clarify it as "purge unneeded bookmarks"
organize:: is assigning to-do item with attributes such as Deadline, Priority, Context, Project. The context is related place or people or device. "Minimal Life" can be a good candidate for simplifying your bookmarks.
review:: The project should have the review frequency forcing you to review action items assigned to the project
engage:: is process of performing the action items and reviewing the project status

## Notion for GTD
Two tables and two pages are minimum requirements for managing GTD based to-do in my opinion:

### Task Table
Requires following columns:

Name:: 
Done:: 
Deadline::
HighProority::
Context::
Project:: is a 'Relation' type that specifies the project name from the Project Table

### Project Table
Requires following columns:

Name:: of the project
Review Frequncy:: in days
Last Review:: 
Next Review:: is automatically calculated from Review Frequency and Last Review
Overdue:: is automatically determined by comparing the Next Review Data and today's date

### Capture Page
Is a view of Task table with filter that shows only tasks that are not Done and not assigned to a project.

### Dashboard Page
Shows proejects that are overdue its reviw
