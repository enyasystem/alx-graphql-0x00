# GraphQL Episode Queries - Task 2

## Objective
Write a GraphQL query to retrieve specific episode information using their ID from the Rick and Morty API.

## API Endpoint
`https://rickandmortyapi.com/graphql`

## Query Structure
The following GraphQL query is used to fetch episode details:

```graphql
query {
  episode(id: ID!) {
    id
    name
    air_date
    episode
  }
}
```

## Files

### Query Files
- `episode-id-1.graphql` - Query to fetch episode with ID 1 (Pilot - S01E01)
- `episode-id-2.graphql` - Query to fetch episode with ID 2 (Lawnmower Dog - S01E02)
- `episode-id-3.graphql` - Query to fetch episode with ID 3 (Anatomy Park - S01E03)
- `episode-id-4.graphql` - Query to fetch episode with ID 4 (M. Night Shaym-Aliens! - S01E04)

### Output Files
- `episode-id-1-output.json` - JSON response for episode ID 1
- `episode-id-2-output.json` - JSON response for episode ID 2
- `episode-id-3-output.json` - JSON response for episode ID 3
- `episode-id-4-output.json` - JSON response for episode ID 4

## Query Details

### Key Fields Requested
- **id**: The unique identifier of the episode
- **name**: The episode's title
- **air_date**: The date the episode aired on TV
- **episode**: The episode code (e.g., S01E01 for Season 1, Episode 1)

## How to Execute

### Using cURL
```bash
curl -X POST https://rickandmortyapi.com/graphql \
  -H "Content-Type: application/json" \
  -d '{"query": "query { episode(id: 1) { id name air_date episode } }"}'
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
  query GetEpisode($id: ID!) {
    episode(id: $id) {
      id
      name
      air_date
      episode
    }
  }
`;

client.query({ query: QUERY, variables: { id: 1 } })
  .then(result => console.log(result.data));
```

## Learning Outcomes
By completing this task, you will understand:
- How to construct GraphQL queries for different data types (not just characters)
- How to use ID arguments to fetch specific resources
- How to request fields from different types in the GraphQL schema
- The structure of the Rick and Morty API's Episode type
- How to work with date-formatted fields in GraphQL responses

## Sample Output
```json
{
  "data": {
    "episode": {
      "id": "1",
      "name": "Pilot",
      "air_date": "December 2, 2013",
      "episode": "S01E01"
    }
  }
}
```

## Rick and Morty Episodes Overview
The Rick and Morty API contains data for all episodes across multiple seasons:

- **Season 1**: 11 episodes (S01E01 - S01E11)
- **Season 2**: 10 episodes (S02E01 - S02E10)
- **Season 3**: 10 episodes (S03E01 - S03E10)
- **Season 4**: 10 episodes (S04E01 - S04E10)
- **Season 5**: 10 episodes (S05E01 - S05E10)
- **Season 6**: 10 episodes (S06E01 - S06E10)
- Plus additional seasons and special episodes

Total: Hundreds of episodes available

## Episode Field Explanations

### id
Unique numeric identifier for the episode in the database. Used as the primary key for lookups.

### name
The human-readable title of the episode (e.g., "Pilot", "Lawnmower Dog").

### air_date
The date the episode originally aired on television. Format: "Month Day, Year" (e.g., "December 2, 2013").

### episode
The episode code in TV notation (SXXEXX format):
- **S** = Season (numbered starting from 01)
- **E** = Episode (numbered starting from 01)
- Example: S01E01 means Season 1, Episode 1

## Practical Use Cases

This query type is useful for:
1. **Episode Details Page**: Display specific episode information on a show details page
2. **Episode Lookup**: Search for episodes by ID
3. **Episode Browser**: Create a browsable guide to all episodes
4. **Data Linking**: Link character appearances to specific episodes
5. **Show Statistics**: Analyze episode air dates and distribution

## Notes
- The Rick and Morty API is publicly available and requires no authentication
- IDs are strings in GraphQL responses but correspond to episode numbers
- Each episode is associated with one or more characters (in other queries)
- Air dates are provided as human-readable strings
- Episode codes follow the standard TV industry notation (SXXEXX)

## Next Steps
These episode queries can be combined with:
- Character queries to find which characters appear in specific episodes
- Episode list queries to paginate through all available episodes
- React components to display episode information in a user interface
