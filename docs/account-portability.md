# Working with other accounts

Postiz support depends on the connected integrations visible in the current workspace.

## Same workspace

If another account is already connected in the same Postiz workspace:

- list integrations
- choose the integration by `identifier`
- create the post with that integration ID

## Different workspace

If the other account lives in a different Postiz workspace:

- use the workspace’s API key or CLI auth context
- verify `is-connected`
- list integrations again
- do not reuse IDs from the first workspace without checking

## Rule of thumb

**IDs are disposable, identifiers are portable, and verification is mandatory.**
