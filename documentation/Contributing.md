How To contribute to AOKP
===

Writing a professional commit message
---

A well formatted, clean, descriptive commit message makes everyone so very happy. Linus Torvalds best explains a good commit message, so no need to reinvent the wheel.

```
Also, please write good git commit messages.  A good commit message
looks like this:

    Header line: explain the commit in one line (use the imperative)

    Body of commit message is a few lines of text, explaining things
    in more detail, possibly giving some background about the issue
    being fixed, etc etc.

    The body of the commit message can be several paragraphs, and
    please do proper word-wrap and keep columns shorter than about
    74 characters or so. That way "git log" will show things
    nicely even when it's indented.

    Make sure you explain your solution and why you're doing what you're
    doing, as opposed to describing what you're doing. Reviewers and your
    future self can read the patch, but might not understand why a
    particular solution was implemented.

    Reported-by: whoever-reported-it
    Signed-off-by: Your Name <youremail@yourhost.com>

where that header line really should be meaningful, and really should be
just one line.  That header line is what is shown by tools like gitk and
shortlog, and should summarize the change in one readable line of text,
independently of the longer explanation. Please use verbs in the
imperative in the commit message, as in "Fix bug that...", "Add
file/feature ...", or "Make Subsurface..."
```
[-Source](https://github.com/torvalds/subsurface/blob/master/README)

Several other guidelines that are good to follow can be found [here](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html), but the gist of it is as follows-
- Header line of 50 characters or less
- A blank line between the header line and body of the commit
- Body text should wrap at 72 characters

***

Pushing a new patch to AOKP's gerrit instance
---

##### *Note: for the purpose of these examples, we're assuming that you're using the .gitconfCDig included in the examples directory of this repository.*

#### Push a patch for public review
```shell
git push gerrit:<gerrit/project> HEAD:refs/for/kitkat
```
or
```shell
pspush for
```

#### Push a patch for private review
```shell
git push gerrit:<gerrit/project> HEAD:refs/drafts/kitkat
```
or
```shell
pspush drafts
```

##### *Note: you will have to push to drafts with each updated patch set or it will be published publicly. repo upload will also make the patch public.*

One can also push directly through review, but you need special permissions to do that, so for the sake of the general public, this will be skipped.

Pushing a new revision of an existing patch to AOKP's gerrit instance
---

Pushing a new patch set to gerrit on an existing patch is essentially the same as patching a new patch, however, there are a couple of stipulations.
- When rebasing a patch manually (patch contains no actual code changes) you must modify the commit message, otherwise gerrit will see no changes on the patch and refuse the submission. Adding a line with *Patch Set 2: Rebased* is sufficient enough to push the change to review.
- You need to make sure the commit message contains the same Commit ID as the original patch. The Commit ID also be on the last group of lines of the commit message. For example
```
Change-Id: Id7b4541fe13ba9c07575190dc34a1a02314ab6b6
Signed-off-by: JohnDoe <JohnDoe@fuu.bar>
```
Then push to gerrit as explained above.

***

Reviewing code on AOKP's instance
---

Once the code is pushed to gerrit, the next step is the review process. Gerrit is a powerful code review and history searching tool. However, the most common tasks are easy to notice and self explanatory. You can view code submissions, view diffs of the patches, cherry-pick to test and review the code, and much more. For a the full documentation look [here](http://gerrit.aokp.co/Documentation/index.html), but we will highlight some key features here.

In the *Reply...* box in the upper middle of the screen you will see several options, most should be self explanatory.
- An empty box for leaving comments (any inline comments will show up here as well)
- Code-Review-
  - -1 This means there is something wrong with the code, coding style (doesn't follow guidelines), or you have an issue with the feature it implements.
  - 0  No opinion on the code itself.
  - +1 The coding style looks good to you and you see no reason why the code shouldn't be merged on looks/theory alone.
- Verified
  - -1 The code breaks building of the package it modifies
  - 0  Not personally verified by you
  - +1 Code builds for you.
- Post - post your comments and review.
- Cancel - Cancel your review of the submission.

Next to that you will see the Change Number. You can cherry-pick via the Change Number, more on that in a minute.

After the Change Number you will see the status of the patch.
- Ready to Submit
- Needs Code-Review
- Merged
- Abandoned

To the right you will find a dropdown to switch between the different patch sets of the commit. Unless you're trying to debug something, it's best to always test the latest patch set in the review.

And at the very right you will find a *Downloads* dropdown. This is another way to easily test patches.

#### Cherry-picking patches for code review

As you can see from the *Downloads* dropdown in a patches review page on gerrit, there are multiple ways getting the submitted code imported into your base. Cherry-picking is the one we will focus on, check the full gerrit documentation for further reading.

The first way of cherry picking code is via the *Downloads* dropdown. Simply highlight the command next to the Cherry Pick option, paste it into your shell, click enter and unless there are merge errors, that is that.

The second way is to use the pstest function. With it, you just need to run pstest with the Change Number pointed out earlier. For example
```shell
pstest 11111
```
pstest will automatically find the latest patch set with that Change Number and cherry pick it to the repository.

##### *Note: in both methods listed above you must be cd'd into the repository the patch is modifying.*

#### Merge Conflicts

More on this to come. They could just need rebasing, it could be a bad patch. But it needs fixing. Conflicts are separated by <<< and >>> and files that have conflicts are listed in git status and git diff.