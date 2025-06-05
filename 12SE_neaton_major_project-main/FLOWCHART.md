# NBA Player Stat Viewer & Simulator - Flowchart

```mermaid
flowchart TD
    %% Start
    Start([Start]) --> Home[Home Page]
    
    %% Main Navigation
    Home -->|View Players| PlayerList[Player List]
    Home -->|Compare Players| Compare[Compare Players]
    Home -->|Simulate Game| Simulate[Simulate Game]
    
    %% Player List Flow
    PlayerList --> PlayerDetails[Player Details]
    PlayerDetails -->|Back| PlayerList
    
    %% Comparison Flow
    Compare --> SelectPlayers[Select Two Players]
    SelectPlayers --> Comparison[View Comparison]
    Comparison -->|Back| Compare
    
    %% Simulation Flow
    Simulate --> SelectPlayersSim[Select Players & Settings]
    SelectPlayersSim --> RunSimulation[Run Simulation]
    RunSimulation -->|Generate Play-by-Play| SimulationEngine[Simulation Engine]
    SimulationEngine -->|Enhance with AI| AI[Gemini AI]
    AI -->|Enhanced Commentary| SimulationResults[View Results]
    SimulationResults -->|Back| Simulate
    
    %% Data Flow
    subgraph Data
        Players[(Players Database)]
        Cache[(AI Cache)]
    end
    
    %% Data Access
    PlayerList <--> Players
    PlayerDetails <--> Players
    SelectPlayers <--> Players
    SelectPlayersSim <--> Players
    SimulationEngine <--> Players
    AI <--> Cache
    
    %% Styling
    classDef startend fill:#f9f,stroke:#333,stroke-width:2px;
    classDef process fill:#bbf,stroke:#333,stroke-width:2px;
    classDef data fill:#bfb,stroke:#333,stroke-width:2px;
    classDef external fill:#f96,stroke:#333,stroke-width:2px;
    
    class Start,SimulationResults startend;
    class Home,PlayerList,PlayerDetails,Compare,SelectPlayers,Comparison,Simulate,SelectPlayersSim,RunSimulation,SimulationEngine process;
    class Players,Data,Cache data;
    class AI external;
```

## Flowchart Explanation

### Main Navigation Paths
1. **View Players**
   - Browse the complete list of NBA players
   - View detailed statistics for any player

2. **Compare Players**
   - Select two players for side-by-side comparison
   - View statistical comparison

3. **Simulate Game**
   - Choose two players to face off
   - Configure game settings
   - Run the simulation
   - View detailed results with AI-enhanced commentary

### Data Flow
- All player data is stored in the Players Database (players.json)
- AI-generated content is cached to improve performance
- The simulation engine processes player statistics to generate realistic game outcomes

### Key Features
- Clean, intuitive navigation
- Responsive design for all devices
- Realistic basketball simulation
- AI-enhanced game commentary
- Performance-optimized with caching
