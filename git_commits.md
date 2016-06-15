# Firstly, sorry...

There's been a bit of confusion about what I've meant when I've asked people to squash commits in Pull Requests. Apologies for this, it's purely me not explaining it well, so thought I'd pop an email in to clarify what I mean.

Basically, what we need to be going for is having a clean commit history.  Every commit in our git history should be small, focussed and meaningful.  So when I say "squash", I do not mean we should only ever have a single commit per pull request.  Squashing commits is all about curating a clean git history, and is intimately tied to writing good commit messages.

Also, sorry about the preachy nature of this email; but we need guidelines on how to do this or we'll continue to have the poor git history we have, which in my opinion is unacceptable given the ratio of developers to volume of code.  If you disagree with any of this, then do speak to me about it - let's talk about it and discuss it and come to a compromise we can all live with :).  Similarly, apologies if preaching to the choir...

# TL;DR

Our git history should be clean and document the changes we've made to our code. Commits should be small, focussed and meaningful.  When asked to squash commits in a PR, this just means getting rid of "Fix specs", "WIP", "I think this will work...", etc so the git history on master is clean.  A notable exception is rubocop fixes on older apps, further guidance in the TL bit.

Remember: the purpose of a commit is to help you understand the change introduced by that commit. The code should give you the how it does it, the message should give you the why you're doing it for when you come back to it in a year's time (or your colleague looks at it tomorrow).

# What is a commit for?

In a word: documentation.  Our git history is the story of how our code changes and evolves over time.  It is used for investigating issues, debugging problems, extending existing code and writing new code.  So, you know, everything we do!

# Who is a commit for?

Not you, not now.  Commits are for other people (including future you!).  No matter how obvious you think the change is, remember that you'll be looking at this without any sort of context in a year's time, and the person maintaining this code long after you've moved onto some other, less awesome, place isn't going to be able to ask you what the hell this thing is about.

## Why?

We're writing code in a collaborative environment, and code is hard.  Coding collaboratively is even harder!  Consequently, without the right context or a deep knowledge of the codebase, or with a whole load of noise obfuscating the critical part of a commit, it's extremely difficult to critique someone else's code.  This includes such illustrious people as:

* The person reviewing your code - you want to be nice to them so that they can give you a good quick review without lots of back and forth and your wonderful change can go live quickly.
* The person deploying your code - if someone else is deploying, they have to be able to fix it if it doesn't work as expected and you've gone to lunch.
* The person supporting your code - we have a lot of apps with a lot of complex behaviours.  The more descriptive the commit message, the easier it is to identify likely commits which broke something.  Bear in mind that the people who will fix things out of hours are currently just devops, and we have little to no context around the features you're pushing out on a daily basis.
* The person changing your code - code changes and evolves and we've all been there; what's great now isn't great in a year's time, what you think is a bug fix actually introduces another bug, etc. Being able to understand what you've done is essential for making sensible changes in the future.

Bear in mind that good commit history isn't an entirely selfless act because all of these people will at some point be you!

# Code change vs commit message

There are two parts to any commit:

1. The code change
1. The commit message

## 1. The code change

In order to be useful, a commit should encapsulate a single feature or change.  It should be:
Small - It should be easy to see fairly quickly from looking at a commit what the change introduced was.
Focussed - There should only be one thing changing in a commit, be that a new feature, fixing a bug, cleaning up rubocop, or refactoring for some specific purpose
Meaningful - As I said before, our git history is the story of how our code changes; if it's all noise that's difficult to separate from the pertinent changes then we might as well not bother with version control at all.  This is a thing I do not recommend...
Refactoring and renaming

We do this frequently and this is a good thing to do.  What we do badly is that we mix in a significant refactor of old code in the same commit as a load of new feature changes.  This makes it very difficult where we're just refactoring code (and is therefore mainly a non-functional change) and where we're actually changing the behaviour of the system.  The same goes for renaming files/classes/etc.

By encapsulating refactors and renames of old code into their own commits, it gives us a much cleaner history because we don't confuse feature changes with structural changes.

Bear in mind there's no point in having these two commits in a single PR: one that introduces some new code and one that refactors it.  From a historical context, we only care about the finished product, so these should be squashed into one.

### Rubocop and miscellaneous formatting (e.g. whitespace)

When working on something in one of our older repos, you may get a whole load of rubocop changes.  So you'll frequently find you make a one-line change, then have to make 50 other changes to make the file pass rubocop.  This should be two commits, the first one is the one-line change, the second are the 50 updates.

**Why?**

Because this is all just formatting; this isn't a functional change to the way the system behaves or runs.  With the example above, there are two problem cases if it's done in a single commit:

* If a developer git blames one of these changes which just (for example) changes single quotes to double quotes, and the commit message is something like "Ensure we do X on Y", they're going to be confused and need to read the whole commit to understand what was going on and realise you've just made a formatting change.
* If a developer git blames the one-line change, they're going to see a 51 line change.  They're then going to assume this was a big change and read the whole commit to understand what was going on and will find it difficult to separate the noisy formatting change from the one line that was important.

In both cases, the future developer has to spend more time than they should understanding the change.  If it's in two commits, they can see what's going on at a glance.

To reiterate, this mainly applies to older repos, where changing an untouched file can pull up a thousand unrelated changes.  New repos are less affected due to the fact we should be adhering to rubocop along the way!

## 2. The commit message

What is a good commit message?

There are some excellent resources on this, a few I strongly recommend reading are:

* https://git-scm.com/docs/git-commit - see the "Discussion" section near the bottom, it's mainly just the first couple of sentences, but it's what Linus recommends!
* http://chris.beams.io/posts/git-commit/
* https://about.futurelearn.com/blog/telling-stories-with-your-git-history/
* https://about.futurelearn.com/blog/a-commit-message-from-our-repo/ - interesting bit of trivia, Mal (who wrote this commit) used to work here

The format of any message should be:

1. A meaningful first summary line of less than 50 characters.
1. In my opinion, this is a guide; 60 is fine, 70 is pushing it, 80 is way out of line. It encourages conciseness and means it's easy to skim our git history at a glance.  Remember github will shorten and hide lengthy first-lines anyway, and it's nice if we can read full lines there (and when typing "git log"...)
1. A blank line after the summary
1. A whole load more information describing the change in more detail.  A one-line commit message for a new feature is likely not enough information
  * Remember even if it's a straightforward change, more information is useful.  If the summary is "Update some gem", then use the body of the commit to explain why it needs to be updated. If you're refactoring, use the body to explain why this refactor is necessary.
  * Also remember that it's good to link to jira tickets, but don't rely on them.  There is a load of old code referencing pivotal tracker tickets that no longer exist because we've moved on to Jira.  We may move on from Jira at some point in the future, and simply referencing a ticket will be similarly useless in the future.

So don't rely on people clicking links to get context as the links may not work in the future.  On the other hand, whatever you write in your commit message will persist eternally!

### Rubocop and refactoring

Note that rubocop and whitespace changes are simple, clear and frequent enough that it's perfectly acceptable just put "Rubocop fixes" or "Whitespace changes".  Similarly, when refactoring or renaming, saying "Refactoring X" is fine but there must be a clear explanation as to why you're doing it in the commit message body.

# What is a bad commit message?

Anything that isn't a good commit message.  Here are some examples of things that should never appear on master:

| Commit Message | Reason for being bad | Notes |
|---|---|---|
| WIP | This means nothing and helps no-one    | If this appears anywhere in your commit message (except as part of another word, such as "wipe", which is in turn part of a nice full description), then this should not be on master and I'm liable to come after you with a nerf gun |
| Fix specs      | Useless information, just squash it into the change that created/broke the specs  | If on a master CI break, explain why the CI broke in this way, not the fact you've fixed it (which we can see in the code that you've made specs go green...) |
| Refactor X     | Not enough information if there's just the summary line (fine if there's a body explaining more) |Refactors can be big and critical. Tell us why you're refactoring it; what's the benefit from doing so? |
| Rename X to Y | See "Refactor X" | See "Refactor X" |
| Less magic... |Meaningless |If this is "less magic" for some other commit on a PR, squash it into that other commit. If it's old code, explain what is magic about it and why you've fixed it. |

I would go on to say that anything which only has a summary line is probably a bad commit message.  Probably, because yes, sometimes (rarely) it's blindingly obvious what the commit's doing and you can do it in 50 characters.

# Ed, you're being a dick, we know how to write git commits

Well, everyone needs a refresher once in a while!  And to be honest, we could do with the refresher... Take a look a the example of this file in filler.  By my estimation (using the criteria I've outlined in this email), about half the lines have a poor git blame history and add no value.  It didn't take me particularly long to find this, there are plenty of other examples in our codebase.

It's not all doom and gloom though, I also checked the git blame for revieworld's Review model (one of our god objects, so a much more significant file) and it only had 15% bad git history, for my version of "bad".  If you accept that summary lines can be over 50 characters, it's more like 4%, which is great!

Check out my workings if you're interested in what I think are "good" or "bad" commit messages.  Disclaimer: yes, it's subjective, but I've tried to be faithful to what I've put in this email when categorising. In some places I had to look at the commit itself to verify that the message was of no use, so feel free to check some out if you think I'm being to harsh/lenient.

# Git commits during development

When developing code, it's a very sensible practice to commit frequently.  Let's say we have a new feature: some brand new "Blog" model.  We branch off and start development, and end up with a load of commits:

1. Define new Blog model
1. Create controller for Blog with CRUD
1. Add index action for Blog
1. Added "created_by" association on Blog
1. Add show action for Blog
1. Ensure that we update User's last_blogged_at
1. Scrap created_by association, it's unnecessary
1. etc...

These are nothing like commits you'd see on master, because the the answer to these two questions is different:

* **What is the commit for?**  Checkpointing changes as development progresses.  It's useful to write some code, decide you're happy with it and create a commit.  You then have freedom to do some other stuff in an exploratory manner, knowing you can always go back to any point in time where you are confident you were on the right path.
* **Who is the commit for?**  The developer(s) writing the code right now. The commit messages may be short because you have immediate context about what it is you're doing and there is no intention that other people read these commits.
  * NOTE: I'd strongly recommend against using things like "WIP" even in this context - you may have to move off onto other work and won't be coming back to this branch for weeks, at which point you'll thank yourself for decent commit messages!
  * I actually tend to be as descriptive as possible in the body of even these commits because I find it a useful way to summarise what I've done to date, regardless of whether I'm planning on squashing down later.

These commits should be squashed down, because they contain a lot of information which isn't useful to future people looking at your code.  For example, someone may be trying to debug an issue with the Blog model in the future.  Do they care that the original developer toyed with a "created_by" association?

Well, that code never made it into master so it's extremely unlikely to be anything to do with this bug, it was merely an exploratory bit of development which got dropped.  Consequently, if a developer has to pick through dozens of commits around adding functionality that isn't even used to find the commit that's relevant to what they're actually trying to fix, they will want to fire nerf guns at you!  On the other hand, they will thank you for a single commit which represents the whole feature, because all the information is in one place (along with a nice description of the functionality in the commit message, of course)

