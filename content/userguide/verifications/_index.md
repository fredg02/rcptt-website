---
title: Verifications
slug: verifications
layout: list
sidebar: userguide
menu:
  sidebar:
      identifier: verifications
      parent: userguide
---

A good functional test can be represented like this:

![](screenshot-verification-scheme-1.png)

Therefore, a test case takes an system under test in some well-defined state, performs some actions, which transfer a system into another state, and
 then verifies that the final state is correct.

Thus, in a test case we need to specify the following:
- Initial state
- Actions to perform
- Expected final state

Since the very beginning RCPTT had support for declarative description of an initial application state via contexts, and imperative 
scripting language describing user actions, but there were no efficient way to verify a final state of an application - assertion 
statements in scipt look very bulky and not very readable, they cannot be reused and it might take way too long to add assertions 
for all aspects we want to check.

So we are filling this missing gap and introducing verifications - declarative reusable descriptions of various aspects 
of an application state, and finally RCPTT test case description perfectly fits a picture from a beginning of this post:

![](screenshot-verification-scheme-2.png)

During setup of inital state, it does not make sense to describe it completely - we need to describe and ensure only parts of a state which are 
relevant to our actions. For instance, if we are testing About dialog, we do not care about projects in workspace or open views, and if we are 
testing Package Explorer view, we don't care about Java compiler settings.

Same with a final state - it makes sense to check only those aspects of an application state, which supposed to be affected by performed 
actions (or those aspects which should not be affected, but in theory might be affected because of bugs).

Though both contexts and verifications are about a state, there is a couple of important differences between them:
- When context fails (i.e. we could not bring an application workspace into expected state), execution is immediately interrupted. 
However if a verification fails, it makes sense to run other verifications too. Of course a test case is considered failing even if one 
verification fails, but running all of them allows to collect more information about what is broken and what is working.
- Context always specify an 'absolute' state, but during verification, for some aspects it matters to operate on a state delta - 
the difference between initial and final states.

Currently released version contains four kinds of verifications:
- **Text verification**. Verifies that given widget contains expected text with (optionally) expected styles. 
Thus, it is extremely easy to verify that source code is highlighted correctly, or verify that newly created Java class has correct contents.
- **Execution time verification**. Makes sure that a test case executes no longer than specified amount of time. This verification can be considered 
as a constraint on a state change of a system clock.
- **Error Log verification**. Allows to verify the Error Log changes during a test case execution. Verification supports include/exclude rules, 
error types, regular expressions, etc.
- **Tree/Table verification**. Allows you to check a state of a tree/table including it's children, icons, etc.

