# Terminating statements

A terminating statement is one of the following:

  1. A "[return](/Statements/return_statements.html)" or "[goto](/Statements/goto_statements.html)" statement.
  2. A call to the built-in function [panic](/Built-in%20functions/handling_panics.html).
  3. A [block](/Blocks/#Block) in which the statement list ends in a terminating statement.
  4. An ["if" statement](/Statements/if_statements.html) in which:
    * the "else" branch is present, and
    * both branches are terminating statements.
  5. A ["for" statement](/Statements/for_statements.html) in which:
    * there are no "break" statements referring to the "for" statement, and
    * the loop condition is absent.
  6. A ["switch" statement](/Statements/switch_statements.html) in which:
    * there are no "break" statements referring to the "switch" statement,
    * there is a default case, and
    * the statement lists in each case, including the default, end in a terminating statement, or a possibly labeled ["fallthrough" statement](/Statements/fallthrough_statements.html).
  7. A ["select" statement](/Statements/select_statements.html) in which:
    * there are no "break" statements referring to the "select" statement, and
    * the statement lists in each case, including the default if present, end in a terminating statement.
  8. A [labeled statement](/Statements/labeled_statements.html) labeling a terminating statement.

All other statements are not terminating.

A [statement list](/Blocks/) ends in a terminating statement if the list is not empty and its final non-empty statement is terminating.