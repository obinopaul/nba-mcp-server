[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/obinopaul-nba-mcp-server-badge.png)](https://mseep.ai/app/obinopaul-nba-mcp-server)

# NBA MCP Server

A Python server implementing Model Context Protocol (MCP) for NBA statistics and live game data.

## Overview

This server provides a set of tools for accessing NBA data through the NBA API. It serves as a bridge between applications and the NBA's data services, offering both live game information and historical statistics.

## Features

- Live game data (scoreboard, box scores, play-by-play)
- Player information and career statistics
- Team game logs and statistics
- League standings
- Game results and schedules

## Tools

### Live Game Data

- **nba_live_scoreboard**
  - Fetch today's NBA scoreboard (live or latest)
  - Returns game IDs, start times, scores, and broadcast details

- **nba_live_boxscore**
  - Fetch real-time box score for a given NBA game ID
  - Provides detailed player and team statistics

- **nba_live_play_by_play**
  - Retrieve live play-by-play actions for a specific game
  - Includes scoring plays, fouls, timeouts, and substitutions

### Player Information

- **nba_common_player_info**
  - Retrieve basic information about a player
  - Includes biographical data, height, weight, team, position

- **nba_player_career_stats**
  - Obtain a player's career statistics
  - Available in different formats (per game, totals, per 36 minutes)

- **nba_list_active_players**
  - Return a list of all currently active NBA players

- **nba_player_game_logs**
  - Obtain a player's game statistics within a specified date range

### Team Data

- **nba_team_game_logs_by_name**
  - Fetch a team's game logs using the team name
  - Avoids needing to know the team's numeric ID

- **nba_fetch_game_results**
  - Fetch game results for a given team ID and date range

- **nba_team_standings**
  - Fetch NBA team standings for a given season and season type

- **nba_team_stats_by_name**
  - Fetch team statistics using the team name
  - Supports different aggregation methods (totals, per game, etc.)

- **nba_all_teams_stats**
  - Fetch statistics for all NBA teams across multiple seasons

### Schedule Information

- **nba_list_todays_games**
  - Returns scoreboard data for any specific date

## Usage

The server is implemented using the MCP framework and can be run as a standalone service.

```python
# Start the server
python nba_server.py
# or
mcp run nba_server.py
```

### Configuration

- The server runs with a 30-second timeout for more reliable operation
- Signal handlers are implemented for graceful shutdown (Ctrl+C)

### Usage with Claude Desktop

#### Option 1: Using Docker (Recommended)

1. Clone this repository
```
git clone https://github.com/obinopaul/nba-mcp-server.git
cd nba-mcp-server
```

2. Install dependencies
```
pip install -r requirements.txt
```

3. Build the Docker image
```
docker build -t nba_mcp_server .
```

4. Run the Docker container
```
docker run -d -p 5000:5000 --name nba_mcp_server nba_mcp_server
```

5. Add this to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "nba_mcp_server": {
      "command": "docker",
      "args": [
        "exec",
        "-i",
        "nba_mcp_server",
        "python",
        "nba_server.py"
      ]
    }
  }
}
```

#### Option 2: Direct Python Execution

1. Clone this repository
```
git clone https://github.com/obinopaul/nba-mcp-server.git
cd nba-mcp-server
```

2. Create a new environment
```
conda create --name your_env_name python=3.13
conda activate your_env_name
```

3. Install dependencies
```
pip install -r requirements.txt
```

4. Run NBA mcp server on the terminal
```
mcp run nba_server.py
```

5. Add this to your `claude_desktop_config.json`, adjusting the Python path as needed:

```json
{
  "mcpServers": {
    "nba_mcp_server": {
      "command": "/path/to/your/python",
      "args": [
        "/path/to/nba_server.py"
      ]
    }
  }
}
```

After adding your chosen configuration, restart Claude Desktop to load the NBA server. You'll then be able to use all the NBA data tools in your conversations with Claude.


## Technical Details

The server is built on:
- NBA API (nba_api) Python package
- MCP for API interface
- Pydantic for input validation
- Pandas for data manipulation

## License

This MCP server is available under the MIT License.