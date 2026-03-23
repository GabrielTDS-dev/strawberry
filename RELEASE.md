Release type: patch

Fixes the issue where the optional union type definition would ignore annotation metadata added with typing.Annotated without breaking functionality elsewhere.

The change made in this bug fix ensures that the Annotated metadata is preserved when rebuilding the union type after removing None, so the correct union name is used. Checking the code example in the page of the corresponding issue, now it's possible to see the correct definition by checking schema introspection in gql client (will correctly show u as "C" type instead of the incorrect "AB" it used to show).
