# Lab 3 - Hunting bugs
![sherlock](./docs/sherlock.jpeg)
(Photo by [Ian Dooley](https://unsplash.com/@sadswim?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/pipe?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText))

Debugging comes in two different shapes:
- It's either the day-to-day activities that gets done during regular development, in isolated topic branches, where bugs are found and fixed instantly, before being integrated in the general code base...
- ...or it's the more high-octane work related to ironing out bugs that have snuck all the way into production.

The latter generally calls for more of a Sherlock Holmes approach in order to both identify and fix the issue; after all, it’s made it all the way to production!

In this exercise we'll be focusing on the latter of the two, and see how `bisect` can be used to identify in which commit a bug was originally introduced. We'll finish of by looking at how a fix then can be integrated and published to production.

## Purpose & Goal
- Get comfortable running and verifying code changes from any commit, and hence work in "detached HEAD" state.
- Understand how `bisect` works, and know when to use it
- Learn how hotfixes can be systematically published to production

## Expectations
- Work in pairs
- For actions/operations performed on one computer – pair program!

## The assignment
The `main` branch in [THIS](https://repo) repository contains a bug that's also made it all the way into production. The product owner in your team wants to know for how long this issue have been present in the live environment, and obviously want a fix for it as soon as possible.

Your task is to:
- Identify when (i.e. from which commit) the bug was first introduced, and single out who created it
- Figure out which release it was part of
- Create a fix
- Publish a new release

### Identifying the culprit

### Create a fix

### Publish the release
