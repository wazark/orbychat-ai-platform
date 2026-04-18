# 🏗️ Architecture

This document describes the system architecture of OrbyChat, focusing on scalability, modularity, and real-world production design.

---

## 🧠 High-Level Architecture

OrbyChat follows a **layered and modular architecture**, separating responsibilities across distinct components.

```text
Client (Mobile/Web)
        ↓
API Layer (Cloudflare Workers)
        ↓
Business Logic Layer
        ↓
Database Layer (PostgreSQL)
        ↓
AI Processing Layer (OpenAI)
```

---

## 🧩 Core Components
**📱 Client Layer (Frontend)**
- Built with Flutter (planned)
- Handles user interaction and UI rendering
- Communicates with backend via REST APIs
- Manages local state and session context

---

## 🌐 API Layer (Cloudflare Workers)
- Serverless architecture
- Handles incoming HTTP requests
- Routes requests to business logic
- Performs authentication checks
- Returns structured responses

**Key benefits:**

- Low latency (edge computing)
- Scalable by design
- No server management

---

## ⚙️ Business Logic Layer
- Core application logic
- Handles:
    - Chat processing
    - Thread management
    - User/project isolation
    - Validation and rules
- Orchestrates AI requests and database interactions

---

## 🗄️ Database Layer (PostgreSQL)
Structured relational model designed for scalability.

Core entities:
- User
- Project
- Thread
- Message
- AI Response
- XP / Achievements
**Design goals:**
- Data normalization
- Efficient querying
- Multi-tenant support
- Clear entity relationships

---

## 🤖 AI Processing Layer (OpenAI)
- Processes user messages
- Generates contextual responses
- Maintains conversation flow
- Supports prompt-based logic

---

## 🔐 Authentication & Session Management
The system uses a token-based authentication model.

**Flow:**
1. User logs in
2. Token is issued
3. Token is stored securely
4. Token is sent with every request
5. API validates token

---

## 🧠 Hybrid Session Model
The system uses a hybrid approach:

- Layer	Responsibility
- Runtime Session	Active state (in memory)
- Persistent Layer	Stored session (secure storage)

---

## ⚠️ Known Considerations
- Session synchronization must be handled carefully
- Token validation must be consistent across layers
- Expiration and invalidation strategies are required

---

## 🔄 Data Flow Example

User sends a message:
```text
User Input
   ↓
API receives request
   ↓
Authentication validation
   ↓
Business logic processes message
   ↓
AI request is triggered
   ↓
Response is stored in database
   ↓
Response returned to user
```

---

## ⚡ Scalability Considerations
- Serverless backend (auto-scaling)
- Stateless API layer
- Database optimized for relational queries
- Modular components allow independent scaling

---

## 🧱 Design Principles
- Separation of concerns
- Modular architecture
- Scalable system design
- Security-first approach
- Real-world production mindset

---

## 🚨 Limitations (Current State)
- Session model not fully unified
- No token refresh strategy yet
- Partial error handling integration
- Frontend not fully implemented

---

## 🔮 Future Improvements
- Token refresh system
- Real-time messaging (WebSockets)
- Caching layer (Redis or equivalent)
- Rate limiting and abuse protection
- Advanced AI context memory
- Observability (logs, metrics, tracing)

---

## 📌 Summary
OrbyChat is designed as a real-world AI SaaS platform, focusing on:

- Scalable backend architecture
- Secure authentication systems
- Structured data modeling
- AI-driven interaction

This architecture allows the system to evolve into a production-ready platform.