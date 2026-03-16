Release type: patch

Fix #3993: Optional Union fails to set correct name/description

### Description
Fixes the issue where the optional union type definition would ignore annotation metadata added with typing.Annotated without breaking functionality elsewhere.

Checking the code example in the page of the corresponding issue, now it's possible to see the correct definition by checking schema introspection in gql client (will correctly show u as "C" type instead of the incorrect "AB" it used to show):

```python
import strawberry
from typing import Annotated
from fastapi import FastAPI
from strawberry.fastapi import GraphQLRouter


@strawberry.type
class A:
    a: str


@strawberry.type
class B:
    b: str


@strawberry.type
class Query:
    u: Annotated[A | B | None, strawberry.union("C")]


schema = strawberry.Schema(query=Query)
app = FastAPI()
graphql_app = GraphQLRouter(schema)
app.include_router(graphql_app, prefix="/graphql")
```

### Migration guide
No migration required.

### Types of Changes
- [ ] Core
- [x] Bugfix
- [ ] New feature
- [ ] Enhancement/optimization
- [ ] Documentation

### Checklist
- [x] My code follows the code style of this project.
- [ ] My change requires a change to the documentation.
- [ ] I have updated the documentation accordingly.
- [x] I have read the CONTRIBUTING document.
- [x] I have added tests to cover my changes.
- [x] I have tested the changes and verified that they work and don't break anything (as well as I can manage).
