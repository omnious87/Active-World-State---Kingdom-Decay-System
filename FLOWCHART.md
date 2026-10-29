    %% Global Server Logic
    subgraph ServerCycle["Daily Server Reset Check"]
        SR[Server Reset Processing] -->|Check Daily Kills| DC{Kill Goal Met?}
        DC -->|Yes| RNC[Reset Neglect Counter to 0]
        DC -->|No| INC[Consecutive Neglect Counter +1]
    end

    %% Dungeon & Field States
    subgraph DungeonField["Dungeon & Field Cascade"]
        INC --> NC{Neglect Counter >= Threshold?}
        NC -->|No| NormalDungeon[Dungeon: Normal State]
        NC -->|Yes (e.g., 7 Days)| FullNeglect[Dungeon: Full Neglect]

        FullNeglect -->|Immediate Spawn Table Change| OverflowField[Field: Overflow State]
        OverflowField -->|Visual Indicator| Skybox1[Skybox Changes to Overflow]
        OverflowField -->|Spawn mechanics| EliteMonster[Spawn No-Loot/No-EXP Key Elite]

        EliteMonster -->|Defeated| RecoverField[Field Recovered -> State Normal]
        
        OverflowField --> OF_Check{Neglect >= Threshold?\ne.g., 3 Days}
        OF_Check -->|Yes| PropagateField[Propagate Overflow to Adjacent Fields]
    end

    %% Settlement States
    subgraph SettlementCascade["Settlement System"]
        PropagateField -->|Adjacent Field Overflow| ChaosState[Settlement: Chaos State]
        ChaosState --> ChaosEffects["- New NPC Dialogues\n- Inflated Prices (+200%)"]
        
        PropagateField -->|Field Neglected 3 Days| CollapseState[Settlement: Collapse State]
        CollapseState --> CollapseEffects["- De-spawn NPCs\n- Skybox Changes"]
    end

    %% Kingdom Level Event
    subgraph KingdomEvent["Kingdom Collapse Mechanic"]
        CollapseState --> KC_Check{Collapsed Area >= 50%?}
        KC_Check -->|Yes| KingdomCollapse[Kingdom Collapse State]
        
        KingdomCollapse --> SpeedUp[Propagation Speed: 3 Days -> 1 Day]
        KingdomCollapse --> MassCascade[Force Adjacent Fields/Settlements into Overflow/Collapse]
        
        KingdomCollapse --> TugOfWar{Recovered Area >= 50%?}
        TugOfWar -->|Yes| GlobalReset[Global Reset: All Fields/Settlements Normal, Dungeon Counters Reset]
    end

    %% Isolated Systems
    subgraph SpecialRules["Special Mechanics & Exclusions"]
        SafeHaven[Safe Haven Area: Guild HQ & Surrounding Fields] ---|Immune to Overflow| TotalCollapse[Fallback Base on Total Server Collapse]
        
        NewContent[New Dungeon Update] --> FrozenCounter[Counter Frozen / NPCs Guard Entrance]
        FrozenCounter --> HandoverCheck{X Unique Players Reach F3?}
        HandoverCheck -->|Yes| DeSpawnNPCs[NPCs De-spawn -> Counter Activates]
    End
