# Data Flow Diagram (DFD) - NBA Player Stat Viewer & Simulator

```mermaid
flowchart TD
    %% External Entities
    User[("User")]
    GeminiAPI[("Gemini AI API")]
    
    %% Main Processes
    subgraph "Web Application (Flask)"
        A[Home Page] -->|View Players| B[Player List]
        A -->|Compare Players| C[Comparison Tool]
        A -->|Simulate Game| D[Game Simulator]
        
        B -->|Select Player| E[Player Details]
        
        C -->|Select Two Players| F[Comparison Results]
        
        D -->|Select Players & Settings| G[Simulation Engine]
        G -->|Game Log| H[Game Results]
        H -->|Request AI Commentary| GeminiAPI
        GeminiAPI -->|Enhanced Commentary| H
    end
    
    %% Data Stores
    subgraph "Data Storage"
        P[(Players Database
        players.json)]
        CACHE[(Cached AI Responses)]
    end
    
    %% Data Flows
    User -->|HTTP Request| A
    User -->|View Player List| B
    User -->|Compare Players| C
    User -->|Start Simulation| D
    
    B <-->|Read/Display| P
    E <-->|Read/Display| P
    C <-->|Read/Compare| P
    
    G <-->|Read Player Data| P
    G <-->|Read/Write| CACHE
    
    H -->|Display Results| User
    F -->|Display Comparison| User
    
    %% Styling
    classDef external fill:#f9f,stroke:#333,stroke-width:2px;
    classDef process fill:#bbf,stroke:#333,stroke-width:2px;
    classDef datastore fill:#bfb,stroke:#333,stroke-width:2px;
    
    class User,GeminiAPI external;
    class A,B,C,D,E,F,G,H process;
    class P,CACHE datastore;
```

## Diagram Explanation

### External Entities
- **User**: Interacts with the web application through a browser
- **Gemini API**: External AI service for generating enhanced game commentary

### Main Processes
1. **Web Application (Flask)**
   - **Home Page**: Entry point with navigation options
   - **Player List**: Displays all available players
   - **Player Details**: Shows detailed statistics for a single player
   - **Comparison Tool**: Allows side-by-side comparison of two players
   - **Game Simulator**: Interface for configuring and running 1-on-1 simulations
   - **Simulation Engine**: Core logic for running basketball simulations
   - **Game Results**: Displays simulation outcomes and statistics

### Data Stores
- **Players Database (players.json)**: Stores all player statistics and information
- **Cached AI Responses**: Stores previously generated AI commentary to reduce API calls

### Data Flows
- Solid arrows represent data flow between components
- Dotted lines represent external API interactions
- Processes can read from and write to data stores as needed

### Key Interactions
1. User interactions flow through the web interface to the Flask backend
2. Player data is read from the JSON database as needed
3. Game simulations process player stats through the simulation engine
4. AI commentary is optionally generated through the Gemini API
5. Results are formatted and displayed back to the user

This diagram provides a high-level overview of how data moves through your application, from user input through processing and storage to output display.
