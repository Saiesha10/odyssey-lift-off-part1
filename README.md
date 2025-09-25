# Odyssey Lift-off I: Basics

#GraphQL (from Apollo Lift-off I)

What is GraphQL?

* A **query language** for APIs and a **runtime** for executing queries.
* Lets clients ask for **exactly the data they need** (no over-fetching, no under-fetching).
* Alternative to REST:

  * REST: multiple endpoints (`/users`, `/users/:id/posts`…).
  * GraphQL: single endpoint, query defines shape of data.
* Strongly typed: schema describes data types and relationships.

Schema-first development

* **Schema = contract** between client and server.
* Defined in **SDL (Schema Definition Language)**.
* Process:

  1. Identify what data/features the client needs.
  2. Define schema in SDL.
  3. Implement resolvers in server.
  4. Query schema from client.
* Allows **parallel development**: client can use mocks before backend is ready.


SDL (Schema Definition Language)

* Used to describe types and relationships.
* **Type system building blocks**:

  * **Scalars:** `String`, `Int`, `Float`, `Boolean`, `ID`.
  * **Objects:** `type Book { id: ID! title: String! author: String! }`.
  * **Lists:** `[Book!]!` = list of non-null books, list itself non-null.
  * **Non-null:** `!` marks required fields.
* **Root types:**

  * `type Query { ... }` — read operations.
  * `type Mutation { ... }` — write operations (insert/update/delete).
  * (later) `type Subscription { ... }` — real-time updates.


Queries

* Entry point for fetching data.
* Syntax matches schema types:

```graphql
query GetBooks {
  books {
    id
    title
    author
  }
}
```

* You only get fields you explicitly ask for.
* Nested queries follow type relationships.

Mocks

* Before backend logic, Apollo Server can generate **mock data** from schema.
* Helps test queries, explore schema, and unblock frontend.
* Mock resolvers can be customized later.

Resolvers

* Functions that resolve values for a type’s fields.
* Signature: `(parent, args, context, info) => data`.
* Example:

```js
Query: {
  book: (parent, args, context) => findBookById(args.id);
}
```

* Connects schema to actual data sources (DB, REST, etc.).

 Apollo Explorer

* GraphQL **IDE** for writing and running queries/mutations.
* Supports:

  * Query building with schema hints/autocomplete.
  * Viewing response structure.
  * Documentation explorer (schema reference).
* Encourages **contract testing** of schema.

Apollo Client basics

* **Client library** for consuming GraphQL APIs in UI frameworks.
* Core concepts:

  * Define query with `gql`.
  * Use hooks (`useQuery`) to fetch data.
  * Automatic caching of results.
* Query example:

```js
const { loading, error, data } = useQuery(GET_BOOKS);
```

* Handles loading, error, and success states.



Significance of GraphQL

  Fetch multiple resources in one query.
 Shape response exactly as needed.
 Strongly typed schema = self-documenting API.
Tools like Explorer give instant visibility.
  Scales well with complex frontends.


