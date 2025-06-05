# NBA Player Stat Viewer & Simulator - Class Diagram

```mermaid
classDiagram
    %% Main Application Class
    class NBAApp {
        -app: Flask
        -players: List[Player]
        +run()
        +load_players()
        +get_player(player_id)
    }

    %% Player Class
    class Player {
        -id: int
        -name: str
        -team: str
        -position: str
        -stats: Dict
        +get_stat(stat_name)
        +enhance_stats()
    }

    %% Basketball Simulator Class
    class BasketballSimulator {
        -player1: Player
        -player2: Player
        -target_score: int
        -make_it_take_it: bool
        -score: Dict[str, int]
        -possession: Player
        -game_log: List[Dict]
        +start_game()
        -simulate_possession()
        -get_shot_success_probability(offensive_player, defensive_player, shot_type)
        -generate_play_description(play_type, players, success)
        -determine_game_winner()
    }

    %% Player Enhancer Class
    class PlayerEnhancer {
        +enhance_player(player: Dict) Player
        -_calculate_scoring_efficiency(player: Dict) float
        -_estimate_usage_rate(player: Dict) float
        -_calculate_defensive_impact(player: Dict) float
        -_estimate_shot_distribution(player: Dict) Dict
    }

    %% Routes
    class Routes {
        +home()
        +list_players()
        +player_detail(player_id)
        +compare()
        +simulate()
        +api_simulate()
    }

    %% Templates
    class Templates {
        +home.html
        +players.html
        +player_detail.html
        +compare.html
        +simulate.html
        +layout.html
    }

    %% Relationships
    NBAApp "1" -- "*" Player : contains
    NBAApp "1" -- "1" Routes : uses
    Routes "1" -- "*" Templates : renders
    Routes "1" -- "1" BasketballSimulator : uses
    BasketballSimulator "1" -- "2" Player : simulates
    PlayerEnhancer "1" -- "1" Player : enhances

    %% Styling
    classDef app fill:#f9f,stroke:#333,stroke-width:2px;
    classDef model fill:#bbf,stroke:#333,stroke-width:2px;
    classDef service fill:#bfb,stroke:#333,stroke-width:2px;
    classDef view fill:#f96,stroke:#333,stroke-width:2px;
    
    class NBAApp app;
    class Player,PlayerEnhancer,BasketballSimulator model;
    class Routes service;
    class Templates view;
```

## Class Descriptions

### 1. NBAApp
- **Purpose**: Main application class that initializes and runs the Flask application
- **Key Attributes**:
  - `app`: Flask application instance
  - `players`: List of all player objects
- **Key Methods**:
  - `run()`: Starts the Flask application
  - `load_players()`: Loads player data from JSON
  - `get_player()`: Retrieves a player by ID

### 2. Player
- **Purpose**: Represents an NBA player and their statistics
- **Key Attributes**:
  - `id`: Unique player identifier
  - `name`: Player's name
  - `team`: Player's team
  - `position`: Player's position
  - `stats`: Dictionary of player statistics
- **Key Methods**:
  - `get_stat()`: Retrieves a specific statistic
  - `enhance_stats()`: Enhances base stats with derived metrics

### 3. BasketballSimulator
- **Purpose**: Handles the 1-on-1 basketball simulation logic
- **Key Attributes**:
  - `player1`, `player2`: The two players in the game
  - `target_score`: Points needed to win
  - `score`: Current score for each player
  - `possession`: Player with current possession
- **Key Methods**:
  - `start_game()`: Initializes and runs the simulation
  - `simulate_possession()`: Simulates a single possession
  - `get_shot_success_probability()`: Calculates shot success chance

### 4. PlayerEnhancer
- **Purpose**: Enhances player data with derived statistics
- **Key Methods**:
  - `enhance_player()`: Main method to enhance player data
  - `_calculate_scoring_efficiency()`: Computes player efficiency metrics
  - `_estimate_usage_rate()`: Estimates player usage rate
  - `_calculate_defensive_impact()`: Computes defensive metrics

### 5. Routes
- **Purpose**: Handles all web application routes
- **Key Methods**:
  - `home()`: Renders the home page
  - `list_players()`: Displays all players
  - `player_detail()`: Shows detailed player stats
  - `compare()`: Handles player comparison
  - `simulate()`: Manages game simulation
  - `api_simulate()`: API endpoint for simulations

### 6. Templates
- **Purpose**: Contains all HTML templates for the web interface
- **Key Templates**:
  - `layout.html`: Base template
  - `home.html`: Home page
  - `players.html`: Player listing
  - `player_detail.html`: Individual player view
  - `compare.html`: Player comparison
  - `simulate.html`: Game simulation interface

## Relationships

1. **Composition**:
   - `NBAApp` contains multiple `Player` objects
   - `BasketballSimulator` is composed with two `Player` objects

2. **Dependency**:
   - `Routes` depends on `Templates` for rendering views
   - `Routes` uses `BasketballSimulator` for game logic
   - `PlayerEnhancer` is used to enhance `Player` objects

3. **Association**:
   - `NBAApp` uses `Routes` to handle web requests
   - `BasketballSimulator` interacts with `Player` objects during simulation
