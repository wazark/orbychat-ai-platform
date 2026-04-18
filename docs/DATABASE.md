# 📊 Database Design

This document describes the database structure used in OrbyChat.

The system uses a **relational model (PostgreSQL)** designed for scalability, data consistency, and multi-tenant support.

---

## 🧠 Core Data Model

The platform is structured around the following entities:

User → Project → Thread → Message → AI Response

---

## 🧩 Main Entities

### 👤 User
Represents a platform user.

**Fields:**
- id
- email
- password_hash
- created_at

---

### 📁 Project
Logical container for conversations.

**Fields:**
- id
- user_id (FK)
- name
- created_at

---

### 💬 Thread
Represents a conversation context.

**Fields:**
- id
- project_id (FK)
- title
- created_at

---

### 📝 Message
Stores user messages.

**Fields:**
- id
- thread_id (FK)
- role (user / system)
- content
- created_at

---

### 🤖 AI Response
Stores AI-generated responses.

**Fields:**
- id
- thread_id (FK)
- content
- created_at

---

### 🏆 XP / Achievements (Optional System)
Tracks user engagement.

**Fields:**
- id
- user_id (FK)
- xp
- level
- achievements

---

## 🔗 Relationships

```text
User
 └── Projects
      └── Threads
           └── Messages
                └── AI Responses
```

---

## ⚡ Design Goals
- Data isolation per user
- Efficient querying
- Clear entity relationships
- Scalability for SaaS usage

---

## 🧠 Multi-Tenant Design
Each user owns:

- Multiple projects
- Multiple threads
- Independent conversation contexts

**This allows:**

- Data isolation
- Scalable architecture
- Flexible usage patterns

## 🚨 Considerations
- Indexing required for performance
- Message volume can grow rapidly
- Archiving strategies may be needed
- Query optimization is critical

---

## 🔮 Future Improvements
- Soft delete support
- Audit logs
- Analytics tables
- Caching layer integration

---

## 📌 Summary
The database is designed to support:

- Scalable AI conversations
- Structured user interaction
- Multi-tenant SaaS architecture

---

# 🔐 `docs/AUTH_FLOW.md`

Esse aqui é MUITO forte pra backend.

---

## 📄 COMPLETO

```md
# 🔐 Authentication Flow

This document describes how authentication and session management work in OrbyChat.

---

## 🧠 Authentication Model

OrbyChat uses a **token-based authentication system**.

---

## 🔄 Login Flow

```text
User submits credentials
   ↓
Backend validates credentials
   ↓
Token is generated
   ↓
Token is returned to client
   ↓
Client stores token securely
```

---

## 🔄 Authenticated Request Flow
```text
Client sends request
   ↓
Includes Authorization header (Bearer token)
   ↓
API validates token
   ↓
Request is processed
```

---

## 🧠 Session Model
The system uses a hybrid session approach:

- Runtime session (in memory)
- Persistent session (secure storage)

---

## 🔐 Token Handling
- Token must be sent on every request
- Token is validated server-side
- Invalid tokens are rejected

---

## 🚨 Logout Flow
```text
User logs out
   ↓
Token is removed from storage
   ↓
Session is cleared
```

---

## ⚠️ Current Limitations
- No token refresh mechanism
- Session synchronization depends on client logic
- No automatic invalidation of expired tokens

---

## 🔮 Future Improvements
- Token refresh system
- Token rotation
- Session unification
- Multi-device session handling
- Role-based access control (RBAC)

---

## 📌 Summary
Authentication is designed to be:

- Secure
- Scalable
- Stateless (API layer)
- Suitable for SaaS environments