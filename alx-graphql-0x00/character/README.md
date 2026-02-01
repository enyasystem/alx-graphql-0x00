# GraphQL Character Queries - alx-graphql-0x00

## Project Overview

This directory contains GraphQL queries for the Rick and Morty API explorer, demonstrating fundamental GraphQL concepts including single queries, pagination, and filtering.

---

## Task 0: Write a Query to Get a Specific Character by ID

### Objective
Retrieve a specific character's information using their ID from the Rick and Morty GraphQL API.

### API Endpoint
`https://rickandmortyapi.com/graphql`

### Query Structure
```graphql
query {
  character(id: ID!) {
    id
    name
    status
    species
    type
    gender
  }
}
```

### Files

#### Query Files
- `character-id-1.graphql` - Query for character with ID 1 (Rick Sanchez)
- `character-id-2.graphql` - Query for character with ID 2 (Morty Smith)
- `character-id-3.graphql` - Query for character with ID 3 (Summer Smith)
- `character-id-4.graphql` - Query for character with ID 4 (Beth Smith)

#### Output Files
- `character-id-1-output.json` through `character-id-4-output.json` - JSON responses from API

### Query Details

#### Fields Requested
- **id**: Unique identifier of the character
- **name**: Character's name
- **status**: Current status (Alive, Dead, or unknown)
- **species**: Character's species
- **type**: Character's type or subtype
- **gender**: Character's gender (Male, Female, or unknown)

### Sample Output
```json
{
  "data": {
    "character": {
      "id": "1",
      "name": "Rick Sanchez",
      "status": "Alive",
      "species": "Human",
      "type": "",
      "gender": "Male"
    }
  }
}
```

### How to Execute

#### Using cURL
```bash
curl -X POST https://rickandmortyapi.com/graphql \
  -H "Content-Type: application/json" \
  -d '{"query": "query { character(id: 1) { id name status species type gender } }"}'
```

#### Using Node.js with Apollo Client
```javascript
import { ApolloClient, InMemoryCache, HttpLink, gql } from '@apollo/client';

const client = new ApolloClient({
  link: new HttpLink({
    uri: 'https://rickandmortyapi.com/graphql',
  }),
  cache: new InMemoryCache(),
});

const QUERY = gql`
  query GetCharacter($id: ID!) {
    character(id: $id) {
      id
      name
      status
      species
      type
      gender
    }
  }
`;

client.query({ query: QUERY, variables: { id: 1 } })
  .then(result => console.log(result.data));
```

### Key Concepts
- **Arguments**: Using `id: ID!` to specify which character to fetch
- **Field Selection**: Requesting only the fields needed (avoiding over-fetching)
- **Single Item Query**: Fetching one resource by its ID

---

## Task 1: Write a Query to Get a List of All Characters

### Objective
Create a GraphQL query to retrieve a paginated list of all characters from the Rick and Morty API.

### Query Structure
```graphql
query {
  characters(page: Int) {
    info {
      count
      pages
      next
      prev
    }
    results {
      id
      name
      status
      image
    }
  }
}
```

### Files

#### Query Files
- `characters-page-1.graphql` - Query for first page of characters
- `characters-page-2.graphql` - Query for second page of characters
- `characters-page-3.graphql` - Query for third page of characters
- `characters-page-4.graphql` - Query for fourth page of characters

#### Output Files
- `characters-page-1-output.json` through `characters-page-4-output.json` - JSON responses from API

### Query Details

#### Info Fields (Pagination Metadata)
- **count**: Total number of characters in the API
- **pages**: Total number of pages available
- **next**: Page number of the next page (or null if on last page)
- **prev**: Page number of the previous page (or null if on first page)

#### Results Fields (Character Data)
- **id**: Unique identifier of the character
- **name**: Character's name
- **status**: Current status (Alive, Dead, or unknown)
- **image**: URL to character's avatar image

### Sample Output (First 3 Characters from Page 1)
```json
{
  "data": {
    "characters": {
      "info": {
        "count": 826,
        "pages": 42,
        "next": 2,
        "prev": null
      },
      "results": [
        {
          "id": "1",
          "name": "Rick Sanchez",
          "status": "Alive",
          "image": "https://rickandmortyapi.com/api/character/avatar/1.jpeg"
        },
        {
          "id": "2",
          "name": "Morty Smith",
          "status": "Alive",
          "image": "https://rickandmortyapi.com/api/character/avatar/2.jpeg"
        },
        {
          "id": "3",
          "name": "Summer Smith",
          "status": "Alive",
          "image": "https://rickandmortyapi.com/api/character/avatar/3.jpeg"
        }
      ]
    }
  }
}
```

### How to Execute

#### Using cURL
```bash
curl -X POST https://rickandmortyapi.com/graphql \
  -H "Content-Type: application/json" \
  -d '{"query": "query { characters(page: 1) { info { count pages next prev } results { id name status image } } }"}'
```

#### Using Node.js with Apollo Client
```javascript
import { ApolloClient, InMemoryCache, HttpLink, gql } from '@apollo/client';

const client = new ApolloClient({
  link: new HttpLink({
    uri: 'https://rickandmortyapi.com/graphql',
  }),
  cache: new InMemoryCache(),
});

const QUERY = gql`
  query GetCharacterList($page: Int!) {
    characters(page: $page) {
      info {
        count
        pages
        next
        prev
      }
      results {
        id
        name
        status
        image
      }
    }
  }
`;

client.query({ query: QUERY, variables: { page: 1 } })
  .then(result => console.log(result.data));
```

### Key Concepts
- **Pagination**: Using the `page` argument to navigate through large datasets
- **Nested Fields**: Querying both metadata (info) and actual data (results) in one request
- **List Queries**: Fetching multiple resources and their collection metadata
- **Default Sorting**: Characters are returned in ID order

### Pagination Details
- The Rick and Morty API has **826 characters** total
- Characters are paginated with **20 characters per page**
- Total of **42 pages** available
- Use the `next` and `prev` fields to navigate

---

## Learning Outcomes

By completing these tasks, you will understand:
- ✅ How to construct precise GraphQL queries
- ✅ How to use arguments to filter results (single vs. paginated)
- ✅ How to request only specific fields needed (avoiding over-fetching)
- ✅ The difference between single-item queries and list queries
- ✅ How pagination works in GraphQL APIs
- ✅ How to work with nested field selections
- ✅ How to work with the Rick and Morty GraphQL API

## Notes
- The Rick and Morty API is publicly available and requires no authentication
- IDs are returned as strings in GraphQL
- Each page returns up to 20 characters
- The `image` field contains direct URLs to character avatars (20x20px to 200x200px versions available)

## Next Steps
These fundamental queries form the basis for:
- More complex queries with filtering (species, status, etc.)
- Combining multiple queries in a single request
- Integrating with React components using Apollo Client
- Building a full-featured character browser application
