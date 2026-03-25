Release type: patch

Fix `Annotated` metadata being lost on optional union types

When using `Annotated[A | B | None, strawberry.union("MyUnion")]`,
the custom union name and other metadata would be dropped during `None` stripping, causing the schema to fall back to an auto-generated name
(e.g. "AB" instead of "MyUnion").
