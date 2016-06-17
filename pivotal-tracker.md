Pivotal Tracker Process
=======================

From this point on I shall use the terms card and story interchangeably. I may also use do the same with Requester and Card owner. 

Story creation should be possible by anyone with access to PT. Those cards unless either pre-agreed by the PO or part of an existing story in play, should be placed in the 'icebox', where they shall be prioritized by a PO, me or a team lead.

Order position denotes priority. So most important at the top, least at the bottom.

The person who owns the card should mark themselves as the "Requester" while the person who is currently working on it should be marked as the owner.

An example:

Sandra writes a story requesting a feature for Auto
---------------------------------------------------
* She clicks the 'Add story' button
* Adds a summary title for the feature
* You can mark the card as either a story, bug or chore. In this case she'll mark it as a story
* She then fills out a more detailed description, any acceptance criteria and adds 'labels' aka tags
* In the case of tags, rather than going silly and twitterish such as #ZOMGILOVEKITTENSFOREEVVVAAAA!!! I'd prefer it if people use the tags as themes. You can have multiple themes, but try and keep them lower case, consistent and if possible ones that already exist. Examples are 'kuoni', 'auto', 'redux vetting', 'staged', 'deployed' etc you get the idea.
* Once this is done she clicks save

At some point the story is prioritized in the icebox and then moved to 'current' for the current iteration. Before it's put into current, it should be estimated. I've left the estimation measure as being Fibonacci as it's served me well it the past. This estimation can be refined later.

Rowland picks this up
---------------------
* He walks over to the requester (card owner) where a discussion occurs
* They go over the details of the story and refine the acceptance criteria
* The details of this conversation then go into Pivotal Tracker as either extras into the description or comments. I'll leave it up to your judgement. Just be aware that if you update the description it might not be evident to someone that any change has occurred.
* The recording of offline conversations is just as important as the ones that occur online and prevents the situation where only a single person is able to fulfill the story
* As a side note for the engineers, PT integrates with Github so if you format your commit messages correctly it should appear as a comment in the story
* Finally Rowland breaks the solution down into other tasks or if the story is an 'Epic' creates other stories. 

Working on the story...
-----------------------
* Rowland clicks 'Start' and begins working on the solution
* Once he's finished, he then clicks 'Finished. If possible he deploys it to staging, tags the story with "staged" and then updates the status as 'Delivered'
* It's at this point that Sandra (the story owner)  checks the story on staging and either accepts or rejects said story. If she rejects, she should update the comments with the reasons why
* If the story is accepted, Rowland will then send a pull request for his topic branch to be merged into master where another happy engineer reviews and merges

Finally
-------
* Rowland updates the story and replaces the 'staged' tag with 'deployed' once the story is on production ( might see if we can automate this via the PT api)
* Profit - kerching, dolla dolla bill ya'll
