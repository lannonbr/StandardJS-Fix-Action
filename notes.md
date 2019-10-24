These are some routes through the actions suite

# Failure route

```js
actions.on("PR", () => {
  runStandard();

  if (!standardPasses) {
    makeBranch();
    pushBranchToOriginRepo();
    createCommentInPR();
  }
});
```

PR Message

```
Hey, we noticed linting returned an error. A branch at `actions/standard-fix/1` was
made. you can either run `standard --fix` and do it manually or comment `/standard-fix`
to have GitHub Actions do it for you.

You can make more commits otherwise and we will keep up the standard branch updated with your changes.
```

# Manual Fix route

```js
actions.on("push to PR", () => {
  runStandard();

  if (standardPasses) {
    failedPreviously = checkForPreviousFailure();

    if (failedPreviously) {
      updateComment();
    }
  }
});
```

```
We see you fixed standard. Thanks!
```
