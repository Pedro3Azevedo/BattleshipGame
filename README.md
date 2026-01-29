# Batalha Naval - Distributed Computing Battle Ship Game

A multiplayer online Battleship game implementing distributed computing infrastructure with TCP/IP networking, XML communication, and web-based gameplay using JSP and Servlets.

**Course**: Infraestruturas Computacionais Distribuídas (IECD) - Distributed Computing Infrastructure  
**Institution**: Instituto Superior de Engenharia de Lisboa (ISEL)  
**Degree**: Licenciatura em Engenharia Informática e Multimédia (Informatics & Multimedia Engineering)  
**Authors**: Pedro Azevedo (A47094) & Ricardo Pedro (A48960)  
**Instructor**: Engenheiro Porfírio Filipe  
**Date Completed**: June 26, 2022

---

## Project Overview

**Batalha Naval** (Battleship) is a comprehensive distributed computing project implementing a multiplayer online Battleship game across two development phases:

- **Phase 1**: Text-based command-line client with core game logic
- **Phase 2**: Web-based interface using JSP and Servlets with enhanced features

The project demonstrates key concepts in distributed systems: TCP/IP networking, client-server architecture, concurrent programming with Threads, XML-based communication protocols, and web technologies.

### Project Vision
Create a secure, scalable multiplayer gaming platform where players can register accounts, manage profiles, compete in real-time Battleship games, and track statistics across a global leaderboard.

---

## Project Objectives

### Part 1: Text-Based Implementation
1. Implement core Battleship game logic
2. Establish TCP/IP client-server communication
3. Handle concurrent multiple game sessions with Threads
4. Implement user account management (registration, login)
5. Validate data exchange using XML and XSD schemas

### Part 2: Web-Based Implementation
1. Expand to web interface using JSP and Servlets
2. Implement user profile management (profile pictures, preferences)
3. Create dynamic leaderboard system
4. Add player search and private game rooms
5. Implement game session management via web
6. Add auto-complete player search functionality
7. Enforce 30-second move time limit per turn

---

## Architecture


### Component Diagram

```
SERVER COMPONENTS:

Servidor.java (Main Server)
├─ ServerSocket (Port 5025, TCP)
├─ Connection Handler (per client)
│  ├─ Menu Thread
│  └─ Game Thread
└─ Data Management
   ├─ Account Files (XML)
   ├─ Image Storage
   ├─ Rankings
   └─ Game Sessions

Cliente.java (Text Client)
├─ Socket Connection
├─ User Interface (Console)
├─ Game State Tracking
└─ Message Handler

JogoServlet & ProfileServlet (Web)
├─ Request Handling
├─ JSP Integration
├─ File Upload/Download
└─ Session Management

Game Engine:
├─ Jogo.java (Game Controller)
│  ├─ Game State Management
│  ├─ Turn Management
│  ├─ Win Condition Detection
│  └─ Scoring
├─ Jogador.java (Player)
│  ├─ Board Management
│  ├─ Ship Placement
│  ├─ Move History
│  └─ Statistics
├─ Casa.java (Cell)
│  ├─ State Management (Hidden/Water/Hit/Destroyed)
│  └─ Visibility Control
└─ Barco.java (Ship)
   ├─ Position & Orientation
   └─ Damage Tracking

Data & Validation:
├─ XmlDoc.java
│  ├─ XML Creation
│  ├─ XML Parsing
│  ├─ XSD Validation
│  └─ String Manipulation
└─ XSD Schema Files
   ├─ protocolo.xsd (Account & Menu Protocol)
   ├─ jogada.xsd (Move Protocol)
   └─ tabuleiro.xsd (Board State)
```

---

## Technology Stack

### Core Technologies

**Programming Language**
- Java (OOP, Concurrency with Threads)

**Networking**
- TCP/IP Protocol (Reliable, ordered, connection-based)
- ServerSocket & Socket (java.net package)
- BufferedReader & PrintWriter (Stream-based communication)

**Data Format & Validation**
- XML (Extensible Markup Language)
- XSD (XML Schema Definition) for validation
- Serialization/Deserialization

### Web Technologies (Part 2)

**Server-Side**
- JSP (JavaServer Pages) - Dynamic page generation
- Servlets - HTTP request handlers
- Tomcat Server (Application server)

**Client-Side**
- HTML (Form elements, Page structure)
- JavaScript (Timer implementation, form validation)
- CSS (Styling - implicit in JSP)

**Protocols**
- HTTP (HyperText Transfer Protocol)
- POST method (Secure password transmission)
- GET method (data retrieval)

### File System
- XML files (Player accounts and data storage)
- Text files (Player availability list)
- Image files (Profile pictures - JPEG/PNG)

---

##  Data Structure & Storage

### Player Account Structure (XML Format)

```xml
<?xml version="1.0"?>
<jogador>
    <nickname>PlayerName</nickname>
    <password>HashedPassword</password>
    <dataNascimento>1995-05-15</dataNascimento>
    <corPreferida>#FF5733</corPreferida>
    <imagem>playerName.jpg</imagem>
    
    <!-- Game Statistics -->
    <estatisticas>
        <numeroVitorias>15</numeroVitorias>
        <numeroJogos>42</numeroJogos>
        <tempoTotalJogo>3600</tempoTotalJogo>
        <tempoMedioPorJogo>85.71</tempoMedioPorJogo>
    </estatisticas>
</jogador>
```

### Board State (Casa - Cell)

**States**:
- **Escondido** (Hidden) - Unrevealed ship location (shown to owner only)
- **Água** (Water) - Empty cell
- **Arder** (Burning) - Ship cell hit but not destroyed
- **Destruído** (Destroyed) - Ship cell hit and destroyed
- **Arder** → Visual: Orange color/symbol

**Visibility Control**:
- **Owner's View**: Shows all states (includes hidden ships)
- **Opponent's View**: Only shows hits (Arder, Destruído) and misses (Água)

### Game Statistics Tracking

**Per Player**:
- Total victories
- Total games played
- Total game time (milliseconds)
- Average time per move

**Leaderboard Criteria**:
1. **Primary Sort**: Number of victories (descending)
2. **Tiebreaker**: Average time per game (ascending - faster is better)

---

## Game Features & Mechanics

### Account Management

**Registration**
- Choose unique nickname (3-15 characters)
- Set password (5-15 characters)
- Select birth date
- Choose preferred color
- Upload profile image

**Login**
- Username/password authentication
- Session persistence (HTTP sessions)
- Logout option

**Profile Management**
- Change password
- Update profile image
- Modify preferred color
- View game statistics
- See average game time

### Game Modes

**1. Private Games**
- Host creates private game room
- Search for specific player by name
- Auto-complete player name suggestion
- Join specific player's game
- Private game queue management

**2. Random/Public Games**
- Queue for matchmaking
- Automatically paired with available player
- Fair game distribution
- Concurrent game support

### Game Mechanics

**Setup Phase**
- 10 ships placed randomly on board
- Ship placement hidden from opponent
- Random first player selection
- Boards initialized (10×10 grid)

**Move Phase**
- Player selects target cell (A-J, 0-9)
- 30-second time limit per move
- Auto-submit null move if time expires
- Server validates move legality
- Board updates in real-time

**Board States During Game**
- **Hidden State** (Player owns): Shows ship locations
- **Visible State** (Opponent sees): Only shows hits/misses
- Visual indicators:
  - Gray/Symbol: Intact ship
  - Orange/Symbol: Hit ship
  - Red/Symbol: Destroyed ship
  - Blue/X: Miss

**Win Condition**
- Destroy all opponent's ships
- Victory awarded
- Statistics updated
- Return to main menu
- Start new game session

### Leaderboard

**Top 10 Display**
- Ranked by number of victories
- Shows player profile image
- Displays average game time
- Tiebreaker applied when needed
- Updated after each game
- Persisted to ranking.xml

---

## Communication Protocol

### XML-Based Message Protocol

**Validation**
- All XML validated against XSD schemas
- Schema enforcement ensures data integrity
- Invalid messages rejected server-side
- Type checking at compile-time

---

## User Interface Flows

### Text Client Flow (Part 1)

```
Server Start
    ↓
Waiting for Client Connection
    ↓
Client Connects
    ├─ Register Account
    │  ├─ Enter nickname (3-15 chars)
    │  ├─ Enter password (5-15 chars)
    │  ├─ Choose DOB & Color
    │  └─ Upload image
    │
    └─ Login with Credentials
        │
        ▼
    ┌─────────────────────┐
    │   MAIN MENU         │
    ├─────────────────────┤
    │ 1. Play Game        │
    │ 2. Edit Profile     │
    │ 3. View Ranking     │
    │ 4. Logout           │
    └─────────────────────┘
        │
        ├─ [Play Game]
        │   ├─ Search for opponent
        │   └─ Start game → Gameplay
        │
        ├─ [Edit Profile]
        │   └─ Update password/preferences
        │
        ├─ [View Ranking]
        │   └─ See top 10 players
        │
        └─ [Logout]
            └─ Disconnect
```

### Web Client Flow (Part 2)

```
Browser Accesses Web Server
    ↓
index.jsp (Login/Register)
    ├─ Register Page
    │  ├─ Forms: nickname, password, DOB, color
    │  ├─ Image upload (FileUpload Servlet)
    │  └─ Account created (accounts/username.xml)
    │
    └─ Login Page
        ├─ Email & password
        └─ Redirect to menu.jsp
        │
        ▼
    ┌──────────────────────┐
    │   MENU.JSP           │
    ├──────────────────────┤
    │ • Profil.jsp         │
    │ • Ranking.jsp        │
    │ • Jogo.jsp (Menu)    │
    │ • Logout             │
    └──────────────────────┘
        │
        ├─ [Profil.jsp]
        │  ├─ Display player info
        │  ├─ Change password
        │  ├─ Update image
        │  ├─ Modify color
        │  └─ Show statistics
        │
        ├─ [Ranking.jsp]
        │  ├─ Top 10 players
        │  ├─ Victories count
        │  ├─ Average time
        │  └─ Profile images
        │
        ├─ [Jogo.jsp - Game Menu]
        │  ├─ Create private room
        │  ├─ Search player (AutoComplete)
        │  ├─ Join private game
        │  └─ Random game
        │
        └─ [Jogo.jsp - Gameplay]
           ├─ Display boards
           ├─ Select target cell
           ├─ 30-second timer
           ├─ Submit move
           ├─ View results
           └─ Game over → return to menu
```


## Features Implementation

### Part 1: Core Features (Text Client)

✅ **Account Management**
- Registration with unique nickname validation
- Secure login authentication
- Account persistence (XML files)

✅ **Game Engine**
- Random ship placement
- Turn-based gameplay
- Move validation
- Ship damage tracking
- Win condition detection

✅ **Concurrent Gaming**
- Multiple simultaneous games
- Thread per game instance
- Thread-safe operations

✅ **Communication Protocol**
- XML message format
- XSD schema validation
- TCP/IP reliability

### Part 2: Enhanced Features (Web Client)

✅ All Part 1 Features Plus:

✅ **Web Interface**
- JSP pages for all functionality
- HTML forms for user input
- Servlet-based request handling
- Session management

✅ **Profile Management**
- Profile image upload/download
- Birth date tracking
- Color preference storage
- Statistics display

✅ **Leaderboard System**
- Top 10 player ranking
- Victory-based ordering
- Average time tiebreaker
- Profile image display
- Real-time updates

✅ **Advanced Game Features**
- Private game rooms
- Player search with AutoComplete
- Random game matchmaking
- 30-second move timer
- Real-time board updates

✅ **Data Persistence**
- XML-based account storage
- Image file management
- Ranking persistence
- Game statistics tracking

---

## Security Considerations

### Design Decisions

**Server-Side Game Logic**
- All game logic executes on server
- Clients cannot manipulate game state
- Prevents cheating through client modification

**Data Validation**
- XSD schema enforces message structure
- Type checking prevents injection attacks
- Invalid messages rejected server-side

**Password Handling**
- Form method: POST (not GET)
- Prevents password exposure in URL
- Session-based authentication

**XML Validation**
- All incoming XML validated against XSD
- Strict schema enforcement
- Malformed messages rejected



##  Learning Outcomes

Upon completing this project, developers gain expertise in:

✅ **Distributed Systems Concepts**
- Client-server architecture
- Concurrent programming with Threads
- TCP/IP network programming
- Request-response communication patterns

✅ **Network Programming**
- Socket creation and management
- Stream-based communication
- Connection lifecycle (handshake, data exchange, closure)
- Buffered I/O operations

✅ **Data Interchange Standards**
- XML document creation and parsing
- XSD schema definition and validation
- Data serialization

✅ **Web Technologies**
- JavaServer Pages (JSP)
- Servlets and HTTP request handling
- HTML forms and form submission
- JavaScript for client-side logic
- Session management

✅ **Game Development**
- Game state management
- Turn-based game mechanics
- Player interaction handling
- Score/ranking systems

✅ **Software Engineering**
- Object-oriented design
- Separation of concerns
- Component reusability
- Error handling and validation

---

## Conclusion

**Batalha Naval** successfully demonstrates distributed computing principles through a complete multiplayer game implementation. The project effectively integrates:

- **Networking**: TCP/IP client-server communication
- **Concurrency**: Thread-based multiplayer support
- **Data Exchange**: XML with XSD validation
- **Web Technologies**: JSP, Servlets, HTML, JavaScript
- **Software Engineering**: Object-oriented design and architecture

The two-phase development approach shows both console-based and web-based implementations, with the second phase adding significant features like profile management, leaderboards, and advanced game modes.

While certain aspects (file-based storage, security) could be improved for production use, the project successfully achieves its educational objectives and provides a solid foundation for a distributed gaming platform.

