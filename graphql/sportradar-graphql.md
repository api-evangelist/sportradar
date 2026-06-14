# Sportradar GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Sportradar Sports Data API. Sportradar is the world's leading sports technology company, providing comprehensive sports data APIs delivering real-time scores, statistics, odds, and content for over 80 sports and 500 leagues worldwide.

The schema models the core data structures found across Sportradar's REST API surface, including sports, competitions, seasons, tournaments, matches, teams, players, statistics, odds, and real-time event data.

## Source

- Developer Portal: https://developer.sportradar.com/
- Documentation: https://developer.sportradar.com/docs/read/Home
- Getting Started: https://developer.sportradar.com/getting-started/docs/get-started

## Schema File

See `sportradar-schema.graphql` for the full type definitions.

## Key Concepts

### Sports and Competitions

The top-level hierarchy begins with `Sport`, which contains `Competition` entities representing leagues and tournaments. Each `Competition` has `Season` entries, which are then divided into `Stage`, `Round`, and `Match` entities.

### Teams and Players

`Team` types represent clubs and franchises with associated `TeamStats` and `TeamRecord` data. `Player` types carry biographical `PlayerProfile` data and sport-specific `PlayerStats`. `Lineup` and `Substitution` types model match-day squad selections.

### Match Data

`Match` is the central event entity. It carries `MatchStatus`, `MatchScore`, and `MatchOdds`. The `Timeline` and `TimelineEntry` types model the sequence of in-match events. Granular event subtypes — `GoalEvent`, `CardEvent`, and `ShotEvent` — hang off the `EventType` union.

### Odds

The `Odds` and `OddsDetails` types model pre-match and live odds. `Market` and `Outcome` represent individual betting markets and their selectable outcomes.

### Standings

`Standing` contains a list of `StandingsRow` entries that reflect league table or bracket positions at any point in a season.

### Real-Time Feeds

`DataFeed` and `DataFeedDetails` represent the push feed surface, aligning with Sportradar's HTTP chunked streaming endpoints for NFL, NBA, NHL, WNBA, and Soccer.

## Root Query Fields

| Field | Type | Description |
|---|---|---|
| sport | Sport | Fetch a single sport by ID |
| sports | [Sport] | List all available sports |
| competition | Competition | Fetch a competition by ID |
| competitions | [Competition] | List competitions, filterable by sport |
| season | Season | Fetch a season by ID |
| tournament | Tournament | Fetch a tournament by ID |
| match | Match | Fetch a match by ID |
| matches | [Match] | List matches with filters |
| team | Team | Fetch a team by ID |
| teams | [Team] | List teams |
| player | Player | Fetch a player by ID |
| players | [Player] | Search players |
| standings | Standing | Get standings for a season or competition |
| odds | Odds | Get odds for a match |
| head2head | Head2Head | Get head-to-head record between two teams |
| search | SearchQuery | Full-text search across sports entities |
| dataFeed | DataFeed | Retrieve a push data feed descriptor |

## Types Count

This schema defines 72 named GraphQL types covering the full breadth of Sportradar's sports data domain.
