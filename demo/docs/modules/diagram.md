# Diagrams

A comprehensive showcase of Mermaid.js diagram types.

## Flowchart

Workflows with different node shapes and connections.

```mermaid
flowchart LR
    A[Start] --> B{Decision}
    B -->|Yes| C[Process]
    B -->|No| D[End]
    C --> E((Circle))
    E --> F[(Database)]
    F --> G{{Hexagon}}
    G --> D
```

## Sequence Diagram

Interactions between actors over time.

```mermaid
sequenceDiagram
    autonumber
    participant C as Client
    participant S as Server
    participant D as Database

    C->>+S: Request
    S->>+D: Query
    D-->>-S: Results
    S-->>-C: Response

    loop Health Check
        S->>S: Check status
    end

    alt Success
        S->>C: 200 OK
    else Error
        S->>C: 500 Error
    end
```

## Class Diagram

Object-oriented structure and relationships.

```mermaid
classDiagram
    class Animal {
        +String name
        +int age
        +makeSound()
    }
    class Dog {
        +String breed
        +bark()
    }
    class Cat {
        +bool indoor
        +meow()
    }

    Animal <|-- Dog
    Animal <|-- Cat
    Owner "1" --> "*" Animal : owns
```

## State Diagram

System states and transitions.

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Processing : submit
    Processing --> Success : complete
    Processing --> Failed : error
    Success --> [*]
    Failed --> Idle : retry
    Failed --> [*] : cancel
```

## Entity Relationship Diagram

Database schema and relationships.

```mermaid
erDiagram
    USER ||--o{ ORDER : places
    USER {
        int id PK
        string email UK
        string name
    }
    ORDER ||--|{ ITEM : contains
    ORDER {
        int id PK
        int user_id FK
        date created
    }
    ITEM {
        int id PK
        string product
        int quantity
    }
```

## User Journey

User experience mapping with satisfaction scores.

```mermaid
journey
    title User Onboarding
    section Sign Up
        Visit site: 5: User
        Fill form: 3: User
        Verify email: 4: User
    section First Use
        Login: 5: User
        Tutorial: 4: User
        Create project: 3: User
    section Success
        Complete task: 5: User
```

## Gantt Chart

Project schedules and dependencies.

```mermaid
gantt
    title Project Timeline
    dateFormat YYYY-MM-DD

    section Design
        Research      :done, a1, 2024-01-01, 7d
        Wireframes    :done, a2, after a1, 5d

    section Development
        Backend       :active, b1, after a2, 14d
        Frontend      :b2, after a2, 14d

    section Launch
        Testing       :c1, after b1, 7d
        Deploy        :milestone, after c1, 0d
```

## Pie Chart

Proportional data distribution.

```mermaid
pie showData
    title Language Usage
    "JavaScript" : 40
    "Python" : 30
    "Go" : 15
    "Rust" : 10
    "Other" : 5
```

## Quadrant Chart

Two-dimensional analysis grid.

```mermaid
quadrantChart
    title Feature Priority Matrix
    x-axis Low Effort --> High Effort
    y-axis Low Impact --> High Impact
    quadrant-1 Do First
    quadrant-2 Plan
    quadrant-3 Delegate
    quadrant-4 Eliminate

    Feature A: [0.8, 0.9]
    Feature B: [0.3, 0.8]
    Feature C: [0.2, 0.3]
    Feature D: [0.7, 0.2]
```

## Requirement Diagram

> **Note:** Requires Mermaid v11.1+

System requirements and traceability.

```mermaid
requirementDiagram
    requirement UserAuth {
        id: REQ-001
        text: System shall authenticate users
        risk: medium
        verifymethod: test
    }

    functionalRequirement Login {
        id: REQ-002
        text: Users can login with email/password
        risk: low
        verifymethod: demonstration
    }

    element AuthModule {
        type: module
        docref: auth.js
    }

    UserAuth - contains -> Login
    AuthModule - satisfies -> Login
```

## GitGraph Diagram

Version control branching and merging.

```mermaid
gitGraph
    commit id: "init"
    commit id: "feat-1"
    branch develop
    checkout develop
    commit id: "dev-1"
    branch feature
    checkout feature
    commit id: "feat-a"
    commit id: "feat-b"
    checkout develop
    merge feature
    checkout main
    merge develop tag: "v1.0"
```

## C4 Diagram

Software architecture at different levels.

```mermaid
C4Context
    title System Context Diagram

    Person(user, "User", "A user of the system")
    System(web, "Web Application", "Main application")
    System_Ext(email, "Email System", "Sends emails")
    SystemDb(db, "Database", "Stores data")

    Rel(user, web, "Uses")
    Rel(web, email, "Sends emails via")
    Rel(web, db, "Reads/Writes")
```

## Mindmap

Hierarchical idea organization.

```mermaid
mindmap
    root((Central Topic))
        Branch A
            Leaf A1
            Leaf A2
        Branch B
            Leaf B1
            Sub-branch
                Detail 1
                Detail 2
        Branch C
            Leaf C1
```

## Timeline

Chronological event display.

```mermaid
timeline
    title Company History
    section Foundation
        2020 : Company founded
             : First employee hired
    section Growth
        2021 : Series A funding
        2022 : 100 employees
             : International expansion
    section Scale
        2023 : IPO
        2024 : Global leader
```

## ZenUML

> **Note:** Requires Mermaid v11.1+

Alternative sequence diagram syntax.

```mermaid
zenuml
    title Auth Flow
    Client->Server.login(credentials) {
        Server->Database.verify(credentials)
        if (valid) {
            return token
        } else {
            return error
        }
    }
```

## Sankey Diagram

Flow and quantity visualization.

```mermaid
sankey-beta
    Source A,Process X,100
    Source A,Process Y,50
    Source B,Process X,75
    Source B,Process Z,25
    Process X,Output 1,120
    Process Y,Output 1,30
    Process Y,Output 2,20
    Process Z,Output 2,25
```

## XY Chart

Line and bar chart combinations.

```mermaid
xychart-beta
    title "Monthly Sales"
    x-axis [Jan, Feb, Mar, Apr, May, Jun]
    y-axis "Revenue ($K)" 0 --> 100
    bar [30, 45, 60, 55, 70, 85]
    line [25, 40, 55, 50, 65, 80]
```

## Block Diagram

System component layouts.

```mermaid
block-beta
    columns 3
    Frontend:1 Backend:1 Database:1
    space:1 API:1 space:1

    Frontend --> API
    API --> Backend
    Backend --> Database
```

## Packet Diagram

Network packet structure.

```mermaid
packet-beta
    0-15: "Source Port"
    16-31: "Destination Port"
    32-63: "Sequence Number"
    64-95: "Acknowledgment Number"
    96-99: "Data Offset"
    100-103: "Reserved"
    104-111: "Flags"
    112-127: "Window Size"
```

## Kanban Board

Task workflow visualization.

```mermaid
kanban
    Todo
        task1[Design mockups]
        task2[Write specs]
    In Progress
        task3[Build API]
    Review
        task4[Code review]
    Done
        task5[Deploy v1]
```

## Architecture Diagram

Cloud and infrastructure layout.

```mermaid
architecture-beta
    group cloud(cloud)[Cloud]

    service web(server)[Web Server] in cloud
    service api(server)[API Server] in cloud
    service db(database)[Database] in cloud

    web:R --> L:api
    api:R --> L:db
```

## Radar Chart

> **Note:** Requires Mermaid v11.1+

Multi-dimensional comparison.

```mermaid
radar-beta
    title Skill Assessment
    axis Design, Frontend, Backend, DevOps, Communication
    curve Developer A{4, 5, 3, 2, 4}
    curve Developer B{3, 3, 5, 4, 3}
    curve Developer C{5, 2, 2, 5, 5}
```

## Treemap

Hierarchical proportional display.

```mermaid
treemap-beta
    "Engineering"
        "Frontend": 40
        "Backend": 35
        "DevOps": 25
    "Product"
        "Design": 30
        "Management": 20
    "Operations"
        "Support": 15
        "HR": 10
```
