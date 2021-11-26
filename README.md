# Lab 3 - Hunting production bugs
![sherlock](./docs/sherlock.jpeg)
(Photo by [Ian Dooley](https://unsplash.com/@sadswim?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/pipe?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText))

Debugging comes in two different shapes:
- It's either the day-to-day activities that gets done during regular development, in isolated topic branches, where bugs are found and fixed instantly, before being integrated in the general code base...
- ...or it's the more high-octane work related to ironing out bugs that have snuck all the way into production.

The latter generally calls for more of a Sherlock Holmes approach in order to both identify and fix the issue; after all, it’s made it all the way to production!

In this exercise we'll be focusing on the latter of the two, and see how `bisect` can be used to identify in which commit a bug was originally introduced. We'll finish of by looking at how a fix then can be integrated and published to production.

## Purpose & Goal
- Get comfortable running and verifying code changes from any commit, and hence work in **_"detached HEAD"_** state.
- Understand how `bisect` works, and know when to use it
- Learn how hotfixes can be systematically published to production

## Expectations
- Work in pairs
- For actions/operations performed on one computer – pair program!

## The assignment
The `main` branch in [this][1] repository contains a bug that's also made it all the way into production. The product owner in your team wants to know for how long this issue have been present in the live environment, and obviously want a fix for it as soon as possible.

Your task is to:
- [ ] Identify when (i.e. from which commit) the bug was first introduced, and single out who created it
- [ ] Figure out which release it was part of
- [ ] Create a fix
- [ ] Publish a new release

### Identifying the culprit
1. Fork and clone [this][1] repo and checkout the `main` branch
1. Launch [src/index.html](./src/index.html) in your browser
1. Verify the bug by hovering the main CTA button (notice how it disappears – it should not happen!)

The product owner tells you that she is certain that the bug was not present in the `v1.0` release.
1. Verify her statement by checking out the `v1.0` release locally. Is the hover state working as expected? (E.g. the CTA button does not disappear)

With two commits identified, one working and one broken, you are now ready to start the bisecting process in order to figure out when the bug was introduced.
1. Tell Git about your newfound information to kickstart the bisecting process.
  ```
  $ git bisect start
  $ git bisect bad main
  $ git bisect good v1.0
  ```
  Above commands allows Git to guide you thorough the rest of the process, taking the shortest path possible.

1. If you don't already have `gitk` running, launch it now and see if you can find the "good" and "bad" commits annotated.

1. ❓ Where is `HEAD` right now and what state is it in?

1. Verify whether or not the "hover"-bug is present, annotate the commit using `$ git bisect good` or `bad` depending on the outcome. Repeat this step until no more revisions are left to verify, keep refreshing the `gitk` window to keep track of your progress visually.

1. With the offending commit identified, finish the bisecting process but stay on the identified commit.
  ```
  $ git bisect reset bisect/bad
  ```

1. Verify that you are now still on the desired commit, and that the bisecting process has been aborted; use `gitk` or `$ git status`

- ❓ Who created the offending commit?
- ❓ In which release was the bug introduced?

Congratulations, you have now completed the first part of this assignment! 🎉

### Creating the fix
With the offending commit identified let's create a fix for it.

1. Start by verifying your current state:
  ```
  $ git status
  HEAD detached at 52252f0
  nothing to commit, working tree clean
  ```
  Your status output should look like above.

1. Create a new branch from where you're at and switch to it, make sure to call it something meaningful.

1. Now scrutinize the commit's patch in order to figure out what's causing the problem. With the bug identified, create a fix for it and commit it to your branch. Make sure to verify the hover state is now working as expected.

Congratulations, you have now completed the second part of this assignment! 🎉

### Publishing the release
With the bug both identified and fixed, it's time to decide how it should be integrated with the `main` branch and finally released.

Depending on the workflow your project is using, there are three common options:
- [Merge](https://git-scm.com/docs/git-merge) your branch straight into `main`
- [Rebase](https://git-scm.com/docs/git-rebase) your branch onto `main` before merging it in
- [Cherry-pick](https://git-scm.com/docs/git-cherry-pick) your changes into `main`

1. Use which ever option you'd like to integrate your fix.
1. Once done, tag your `main` branch with a suitable version (to "trigger" a new release)

❓ How do the three options differ? Given your history, draw the three alternatives (using pen and paper) to showcase how they would play out in your particular case.

Congratulations, you have now completed the final part of this assignment! 🎉

[1]: https://repo "repo"
