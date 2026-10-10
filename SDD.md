# 📐 Document 3: System Design & Architecture Document (SDD)
> **Project:** Task Management System (Kanban Style)  
> **Version:** 1.0.0  
> **Author:** Ashish Thombare  
> **Date:** 10-Oct-2026  
> **Status:** APPROVED Architecture Baseline  

---

## 1. Architectural Overview & Separation of Concerns (SoC)
The system is engineered using a decoupled **Client-Server Architecture** to ensure clean separation of responsibilities, high maintainability, and horizontal scalability.

┌────────────────────────────────────────────────────────┐
│               FRONTEND LAYER (Client)                  │
│   [React.js App] ──► [Tailwind CSS View Rendering]     │
└───────────────────────────┬────────────────────────────┘
│ (HTTP / JSON Payload)
▼
┌────────────────────────────────────────────────────────┐
│               BACKEND API LAYER (Server)               │
│   [Controllers] ──► [Services / In-Memory Data Store]  │
└────────────────────────────────────────────────────────┘

* **Client Layer (`client/`):** A Single Page Application (SPA) built using **React (Vite)** and styled with **Tailwind CSS**. Its sole responsibility is rendering data and capturing user interactions. It holds no complex business logic.
* **Server Layer (`server/`):** A RESTful Web API built using **ASP.NET Core (C#)**. It enforces business rules, handles request parsing, performs schema validations, and manages state state transitions.

---

## 2. Data Schema Matrix (Data Layer)
Adhering to the **Single Responsibility Principle (SRP)**, the `TaskItem` data schema isolates all variables vital to the task life cycle.

| Property Name | Data Type | Constraints / Validation | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| `Id` | `int` | Primary Key, Auto-incremented | N/A | Unique task identifier |
| `Title` | `string` | Required, Min: 3, Max: 100 chars | `string.Empty` | Brief name of the task |
| `Description` | `string` | Optional, Max: 500 chars | `string.Empty` | Detailed task context |
| `Status` | `string` | Enum: `["To Do", "In Progress", "Done"]` | `"To Do"` | Current operational lane |
| `Priority` | `string` | Enum: `["Low", "Medium", "High"]` | `"Medium"` | Structural urgency level |
| `DueDate` | `DateTime?` | Optional, Nullable | `null` | Target completion timeline |
| `CreatedAt` | `DateTime` | Read-only after generation | `DateTime.UtcNow` | System generation timestamp |

---

## 3. API RESTful Endpoints Specification (Swagger Design)
The backend exposes a highly standardized RESTful contract via **Swagger UI** for front-end consumption:

### 3.1 Fetch All Tasks
* **HTTP Method:** `GET`
* **Route:** `/api/tasks`
* **Success Response:** `200 OK` ➔ Returns an Array of `TaskItem` JSON objects.

### 3.2 Fetch Single Task
* **HTTP Method:** `GET`
* **Route:** `/api/tasks/{id}`
* **Success Response:** `200 OK` ➔ Returns target `TaskItem` JSON object.
* **Error Response:** `404 NotFound` ➔ If ID does not exist.

### 3.3 Create New Task
* **HTTP Method:** `POST`
* **Route:** `/api/tasks`
* **Request Body:** JSON Payload containing `Title`, `Description`, `Priority`, `DueDate`.
* **Success Response:** `201 Created` ➔ Returns the freshly generated object with assigned `Id`.
* **Error Response:** `400 BadRequest` ➔ If `Title` validation fails.

### 3.4 Update Existing Task
* **HTTP Method:** `PUT`
* **Route:** `/api/tasks/{id}`
* **Request Body:** Full updated `TaskItem` JSON object.
* **Success Response:** `204 NoContent` ➔ State updated successfully.
* **Error Response:** `404 NotFound` or `400 BadRequest`.

### 3.5 Delete Task
* **HTTP Method:** `DELETE`
* **Route:** `/api/tasks/{id}`
* **Success Response:** `204 NoContent` ➔ Task purged successfully.
* **Error Response:** `404 NotFound`.
---
