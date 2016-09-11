# Terminating statements

A terminating statement is one of the following:

  1. A "return" or "goto" statement.
  2. A call to the built-in function panic.
  3. A block in which the statement list ends in a terminating statement.
  4. An "if" statement in which:
    * the "else" branch is present, and
    * both branches are terminating statements.
  5. A "for" statement in which:
    * there are no "break" statements referring to the "for" statement, and
    * the loop condition is absent.
  6. A "switch" statement in which:
    * there are no "break" statements referring to the "switch" statement,
    * there is a default case, and
    * the statement lists in each case, including the default, end in a terminating statement, or a possibly labeled "fallthrough" statement.
  7. A "select" statement in which:
    * there are no "break" statements referring to the "select" statement, and
    * the statement lists in each case, including the default if present, end in a terminating statement.
  8. A labeled statement labeling a terminating statement.

All other statements are not terminating.

A statement list ends in a terminating statement if the list is not empty and its final non-empty statement is terminating.