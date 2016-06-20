Migrating to Github from git@code
---------------------------------

Notes initially written by Tom Lea (kudos):
Mark git@code repo as readonly:

    ssh git@code
    cd reevoomark3.git
    mv hooks/update{,.old}
    vim hooks/update

Enter something like this, the important thing is to `exit 1` at the end:

    #!/bin/sh
    echo "ERROR: This repo has moved to github" >&2
    echo "Please update your remote to one of the following:" >&2
    echo " git@github.com:reevoo/mark.git" >&2
    echo " https://github.com/reevoo/mark.git" >&2
    exit 1

Make sure you make the file executable:

    chmod +x hooks/update

Now try and push an empty commit and ensure it fails.

Sync github with git@code:

    #Assumes origin=>git@code and github=>the guhub repo.
    git fetch && git branch -r | grep origin | sed 's/.*origin\///' | while read b; do git push github origin/$b:refs/heads/$b; done

This may take bloody ages!

Give it time. Do not panic. Do not pass go. Do go for a fag/coffee break. Collect £200 if you have the opportunity, we're not running a charity here!

Once it's completed, and only once it's completed, change your origin to the github repo.

Now change the cap scripts something like this: 

    https://github.com/reevoo/mark/commit/93d83c5133e24824b8175472b96deb9498675c58

Commit this, and push it, verifying it ends up on github.

Try deploying. It may well fail with this error: Could not parse object '93d83c51some00sha00bolocks8675c58'

This is probably because the cached copy of the repo on the host is still referencing git@code.

Do the following to fix it:

    cap invoke COMMAND="rm -Rf /apps/mark/shared/cached-copy"

(obviously you will need to change mark for something else).

Deploy again.

FGJ Syncing:

On git@code:

    GIT_DIR=~/revieworld.git git remote add --mirror github git@github.com:reevoo/revieworld.git

Add droids to the teams for your new repo at:
Github > Repository > Settings > Teams

Notify the team to update the remotes in the local repositories.
