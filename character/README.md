# GraphQL Character Queries - Task 0

## Objective
Write a GraphQL query to retrieve specific character information using their ID from the Rick and Morty API.

## API Endpoint
`https://rickandmortyapi.com/graphql`

## Query Structure
The following GraphQL query is used to fetch character details:

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

## Files

### Query Files
- `character-id-1.graphql` - Query to fetch character with ID 1 (Rick Sanchez)
- `character-id-2.graphql` - Query to fetch character with ID 2 (Morty Smith)
- `character-id-3.graphql` - Query to fetch character with ID 3 (Summer Smith)
- `character-id-4.graphql` - Query to fetch character with ID 4 (Jerry Smith)

### Output Files
- `character-id-1-output.json` - JSON response for character ID 1
- `character-id-2-output.json` - JSON response for character ID 2
- `character-id-3-output.json` - JSON response for character ID 3
- `character-id-4-output.json` - JSON response for character ID 4

## Query Details

### Key Fields Requested
- **id**: The unique identifier of the character
- **name**: The character's name
- **status**: The character's current status (Alive, Dead, or unknown)
- **species**: The character's species
- **type**: The character's type (or subtype)
- **gender**: The character's gender (Male, Female, or unknown)

## How to Execute

### Using cURL
```bash
curl -X POST https://rickandmortyapi.com/graphql \
  -H "Content-Type: application/json" \
  -d '{"query": "query { character(id: 1) { id name status species type gender } }"}'
```

### Using Node.js with Apollo Client
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

## Learning Outcomes
By completing this task, you will understand:
- How to construct precise GraphQL queries
- How to use arguments (like `id`) to filter results
- How to request only specific fields needed (avoiding over-fetching)
- The difference between single item queries and list queries
- How to work with the Rick and Morty GraphQL API

## Sample Output
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

## Notes
- The Rick and Morty API is publicly available and requires no authentication
- IDs are strings in GraphQL but correspond to character identifiers
- Some fields may be empty (e.g., `type` field for Rick is empty)
- This is the foundation for more complex queries in subsequent tasks
