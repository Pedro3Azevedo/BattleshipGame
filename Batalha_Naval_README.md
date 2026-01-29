# ⚓ Batalha Naval - Distributed Computing Battle Ship Game

A multiplayer online Battleship game implementing distributed computing infrastructure with TCP/IP networking, XML communication, and web-based gameplay using JSP and Servlets.

**Course**: Infraestruturas Computacionais Distribuídas (IECD) - Distributed Computing Infrastructure  
**Institution**: Instituto Superior de Engenharia de Lisboa (ISEC)  
**Degree**: Licenciatura em Engenharia Informática e Multimédia (Informatics Engineering & Multimedia)  
**Authors**: Pedro Azevedo (A47094) & Ricardo Pedro (A48960)  
**Instructor**: Engenheiro Porfírio Filipe  
**Date Completed**: June 26, 2022

---

## 📋 Project Overview

**Batalha Naval** (Naval Battle/Battleship) is a comprehensive distributed computing project implementing a multiplayer online Battleship game across two development phases:

- **Phase 1**: Text-based command-line client with core game logic
- **Phase 2**: Web-based interface using JSP and Servlets with enhanced features

The project demonstrates key concepts in distributed systems: TCP/IP networking, client-server architecture, concurrent programming with Threads, XML-based communication protocols, and web technologies.

### Project Vision
Create a secure, scalable multiplayer gaming platform where players can register accounts, manage profiles, compete in real-time Battleship games, and track statistics across a global leaderboard.

---

## 🎯 Project Objectives

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

## 🏗️ Architecture

### System Architecture

```
┌────────────────────────────────────────────────────────────┐
│              CLIENT APPLICATIONS                           │
├────────────────────────────────────────────────────────────┤
│ • Text Client (Console)          • Web Client (JSP)        │
│   (Part 1)                         (Part 2)                │
│   - CommandLine Interface          - Browser Interface     │
│   - Direct TCP Connection          - HTTP Requests         │
│   - Menu-based Navigation          - Form-based Input      │
└────────────────┬────────────────────────────────────┬──────┘
                 │                                    │
                 │   TCP/IP Socket Connection        │ HTTP
                 │   Port: 5025                       │ (via Servlets)
                 │   Protocol: TCP (Reliable)        │
                 │                                    │
    ┌────────────▼────────────────────────────────────▼──────┐
    │                  JAVA SERVER                            │
    ├──────────────────────────────────────────────────────────┤
    │                                                          │
    │ ┌────────────────────────────────────────────────────┐  │
    │ │  SERVER ENGINE                                     │  │
    │ │  • ServerSocket (TCP Listener)                     │  │
    │ │  • Thread Pool for Client Connections            │  │
    │ │  • Thread per Game Instance                       │  │
    │ ├────────────────────────────────────────────────────┤  │
    │ │  GAME LOGIC LAYER                                  │  │
    │ │  • Jogo (Game Class)                              │  │
    │ │  • Jogador (Player Class)                          │  │
    │ │  • Casa (Board Cell Class)                         │  │
    │ │  • Barco (Ship Class)                              │  │
    │ ├────────────────────────────────────────────────────┤  │
    │ │  DATA MANAGEMENT                                   │  │
    │ │  • XML File Storage (Per Player Account)           │  │
    │ │  • Profile Images (images/ directory)              │  │
    │ │  • Rankings (ranking.xml)                          │  │
    │ │  • Player Availability List                        │  │
    │ ├────────────────────────────────────────────────────┤  │
    │ │  COMMUNICATION LAYER                               │  │
    │ │  • XML Message Creation & Parsing                  │  │
    │ │  • XSD Validation (Protocol Enforcement)           │  │
    │ │  • BufferedReader/PrintWriter Streams             │  │
    │ └────────────────────────────────────────────────────┘  │
    │                                                          │
    └──────────────────────────────────────────────────────────┘
                 │
                 ▼
    ┌────────────────────────────────┐
    │  PERSISTENT STORAGE            │
    ├────────────────────────────────┤
    │ • accounts/ (Player XML files)  │
    │ • images/ (Profile images)      │
    │ • ranking.xml                   │
    │ • jogadoresDisponiveis.txt      │
    └────────────────────────────────┘
```

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

## 🛠️ Technology Stack

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

## 💾 Data Structure & Storage

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

## 🎮 Game Features & Mechanics

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

## 📊 Communication Protocol

### XML-Based Message Protocol

**Account Creation/Login (protocolo.xsd)**
```xml
<protocolo>
    <conta>
        <nickname>player1</nickname>
        <password>pass123</password>
        <dataNascimento>1995-05-15</dataNascimento>
        <corPreferida>#FF5733</corPreferida>
    </conta>
</protocolo>
```

**Menu Commands (protocolo.xsd)**
```xml
<protocolo>
    <menu>
        <!-- Options: novoJogo, editarPerfil, ranking, sair -->
        <novoJogo>
            <!-- Options: jogadorAleatorio, criarJogoPrivado, escolherJogador -->
            <jogadorAleatorio/>
        </novoJogo>
    </menu>
</protocolo>
```

**Move Command (jogada.xsd)**
```xml
<protocolo>
    <jogo>
        <jogada>
            <casa>A5</casa>  <!-- Coordinates A-J, 0-9 -->
        </jogada>
    </jogo>
</protocolo>
```

**Board State (tabuleiro.xsd)**
```xml
<protocolo>
    <jogo>
        <tabuleiro>
            <casa coordenada="00">█</casa>  <!-- Gray: intact ship -->
            <casa coordenada="01">X</casa>  <!-- Blue: miss -->
            <casa coordenada="02">🔥</casa> <!-- Orange: hit -->
            <casa coordenada="03">🔴</casa> <!-- Red: destroyed -->
        </tabuleiro>
    </jogo>
</protocolo>
```

**Validation**
- All XML validated against XSD schemas
- Schema enforcement ensures data integrity
- Invalid messages rejected server-side
- Type checking at compile-time

---

## 📱 User Interface Flows

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

---

## 🎯 Key Implementation Details

### TCP Connection Setup

```java
// Server Side
ServerSocket serverSocket = new ServerSocket(DEFAULT_PORT);
Socket newSock = serverSocket.accept(); // Wait for client

// Client Side
Socket socket = new Socket(DEFAULT_HOST, DEFAULT_PORT);
BufferedReader is = new BufferedReader(
    new InputStreamReader(socket.getInputStream()));
PrintWriter os = new PrintWriter(
    socket.getOutputStream(), true);
```

### Thread-Based Concurrency

**Server Threading Model**:
1. Main thread listens for client connections
2. New thread created per client connection
3. Handles menu operations in client-dedicated thread
4. Game thread created per game instance
5. Multiple games can run concurrently

```java
for each client connection:
    create Thread for Menu Operations
    for each game:
        create Thread for Game Execution
```

### XML Message Handling

**Creation**:
```java
String xml = xmlDoc.createAccountXML(nickname, password, dob, color);
```

**Validation**:
```java
boolean valid = xmlDoc.validateXML(xml, "protocolo.xsd");
```

**Parsing**:
```java
String value = xmlDoc.getNodeValue(xml, "nickname");
```

### File Upload/Download (Web)

**Profile Image Upload**:
- FileUpload Servlet handles HTTP file uploads
- Images stored in `images/` directory
- Filename based on username
- Referenced in player XML file

**Profile Image Display**:
- Retrieved from `images/` directory
- Displayed in profile and ranking pages
- Served via download Servlet

### Game State Persistence

**Per-Game State**:
- Maintained in memory during gameplay
- Board states synchronized via XML
- Game statistics updated post-game
- Player XML files updated with new stats

**Post-Game Update**:
```
Game Ends
    ↓
Increment game count
    ↓
Award victory to winner
    ↓
Add move times to total
    ↓
Calculate new average time
    ↓
Update ranking.xml
    ↓
Return players to menu
```

---

## 📈 Features Implementation

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

## 🔐 Security Considerations

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

### Security Limitations

⚠ Password storage (consider hashing in production)  
⚠ No encryption for network transmission  
⚠ File-based storage (not scalable)  
⚠ Limited session timeout handling  

---

## 🚀 Installation & Execution

### Prerequisites

- Java JDK 8 or higher
- Apache Tomcat (for Part 2)
- Text editor or IDE

### Part 1: Text Client Setup

```bash
# Compile server
javac Servidor.java

# Compile client
javac Cliente.java

# Start server (Terminal 1)
java Servidor

# Start client(s) (Terminal 2, 3, ...)
java Cliente
```

### Part 2: Web Client Setup

```bash
# Deploy to Tomcat
cp -r webapp/* $TOMCAT_HOME/webapps/batalha-naval/

# Start Tomcat
cd $TOMCAT_HOME/bin
./startup.sh

# Access application
http://localhost:8080/batalha-naval/
```

---

## 📚 Key Files & Structure

```
Batalha Naval Project/
│
├── Source Code
│   ├── Servidor.java           # Main server
│   ├── Cliente.java            # Text client
│   ├── JogoServlet.java        # Game request handler
│   ├── ProfileServlet.java     # Profile request handler
│   ├── FileUpload.java         # Image upload handler
│   │
│   ├── Game Logic
│   ├── Jogo.java               # Game controller
│   ├── Jogador.java            # Player class
│   ├── Casa.java               # Board cell
│   ├── Barco.java              # Ship class
│   │
│   └── Utilities
│       └── XmlDoc.java         # XML operations
│
├── Web Content (JSP)
│   ├── index.jsp               # Login/register page
│   ├── menu.jsp                # Main menu
│   ├── perfil.jsp              # Profile management
│   ├── ranking.jsp             # Leaderboard
│   └── jogo.jsp                # Game interface
│
├── Configuration
│   ├── web.xml                 # Servlet mappings
│   ├── tomcat-users.xml        # Tomcat users
│   └── server.xml              # Server config
│
├── Schemas (XSD)
│   ├── protocolo.xsd           # Account & menu protocol
│   ├── jogada.xsd              # Move protocol
│   └── tabuleiro.xsd           # Board state
│
└── Data Storage
    ├── accounts/               # Player account files (XML)
    ├── images/                 # Profile images
    ├── ranking.xml             # Top 10 ranking
    └── jogadoresDisponiveis.txt # Available private games
```

---

## 📊 Performance Characteristics

| Aspect | Implementation |
|---|---|
| **Concurrency** | Thread per client + Thread per game |
| **Scalability** | Limited by thread pool; ~100s of concurrent games |
| **Network Protocol** | TCP/IP (connection-based, reliable) |
| **Data Format** | XML (human-readable, validated) |
| **Storage** | File-based (suitable for small deployments) |
| **Session Management** | Servlet sessions (HTTP) + custom tracking |
| **Game Timer** | JavaScript client-side + server validation |
| **Latency** | LAN suitable (may be slow over Internet) |

---

## 🎓 Learning Outcomes

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

## 🐛 Known Issues & Future Improvements

### Current Limitations

⚠ **Client Disconnection**: Opponent not notified if player disconnects mid-game  
⚠ **Server Downtime**: Game data lost if server crashes  
⚠ **File Paths**: Relative path issues with file access/storage  
⚠ **Database**: File-based storage not suitable for production scaling  
⚠ **Visual Design**: Basic UI/UX (could be enhanced)  

### Recommended Improvements

**Short-term**
- [ ] Handle client disconnection gracefully
- [ ] Implement game state recovery
- [ ] Fix relative path issues
- [ ] Enhanced error messages

**Medium-term**
- [ ] Migrate to relational database
- [ ] Implement password hashing
- [ ] Add SSL/TLS encryption
- [ ] Improve UI/UX design
- [ ] Add server-side session timeout

**Long-term**
- [ ] Implement authentication tokens
- [ ] Add database connection pooling
- [ ] Support multiple server instances (load balancing)
- [ ] Implement game statistics analytics
- [ ] Add chat/messaging between players
- [ ] Support variable board sizes/ship configurations
- [ ] Implement AI opponents

---

## 🔄 Development Phases

### Phase 1: Text-Based Implementation
**Duration**: Initial development period  
**Focus**: Core game logic, TCP networking, XML communication  
**Outcome**: Working command-line game with multiple concurrent players

### Phase 2: Web-Based Enhancement
**Duration**: Final development period  
**Focus**: JSP interface, profile management, leaderboard, advanced features  
**Outcome**: Full web application with enhanced gameplay and features

---

## 📖 Protocol Examples

### Authentication Flow

```
Client → Server: Login XML (username, password)
         ↓
Server: Validate credentials
         ↓
Server → Client: Session XML (success/failure)
         ↓
Client: Store session ID
         ↓
Client ← → Server: Authenticated messages
```

### Game Flow

```
Client 1 → Server: Request random game
Client 2 → Server: Request random game
         ↓
Server: Match players, create game thread
         ↓
Server → Both: Game start, board states
         ↓
Client 1: Send move (XML)
         ↓
Server: Validate, update board, determine result
         ↓
Server → Both: Updated boards
         ↓
Client 2: Send move
         ...repeat until win
         ↓
Server: Award victory, update statistics
         ↓
Server → Both: Game over, return to menu
```

---

## 🎯 Conclusion

**Batalha Naval** successfully demonstrates distributed computing principles through a complete multiplayer game implementation. The project effectively integrates:

- **Networking**: TCP/IP client-server communication
- **Concurrency**: Thread-based multiplayer support
- **Data Exchange**: XML with XSD validation
- **Web Technologies**: JSP, Servlets, HTML, JavaScript
- **Software Engineering**: Object-oriented design and architecture

The two-phase development approach shows both console-based and web-based implementations, with the second phase adding significant features like profile management, leaderboards, and advanced game modes.

While certain aspects (file-based storage, security) could be improved for production use, the project successfully achieves its educational objectives and provides a solid foundation for a distributed gaming platform.

---

## 👥 Team

**Team Members**:
- Pedro Azevedo (A47094)
- Ricardo Pedro (A48960)

**Instructor**: Engenheiro Porfírio Filipe  
**Course**: Infraestruturas Computacionais Distribuídas (IECD)  
**Institution**: Instituto Superior de Engenharia de Lisboa (ISEC)  

---

## 📄 License

Educational project completed as coursework for IECD at ISEC.

---

## 🔗 Related Documentation

- Course Materials: IECD - Distributed Computing Infrastructure
- Referenced Technologies: Java, TCP/IP, XML, JSP, Servlets
- Game Theory: Battleship (classic game rules)

---

**Date Completed**: June 26, 2022  
**Status**: Complete - Both phases implemented  
**Project Type**: Distributed Computing Infrastructure  
**Delivery Method**: Two-phase development (text + web)

