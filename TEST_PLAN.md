# 🧪 Document 5: QA Testing Plan & Test Cases Document
> **Project:** Task Management System (Kanban Style)  
> **Version:** 1.0.0  
> **Author:** Ashish Thombare  
> **Date:** 10-Oct-2026  
> **Status:** APPROVED QA Gates  

---

## 1. QA Strategy & Testing Methodology
To guarantee structural integrity, compliance with the SRS, and data sanity, this project utilizes a strict **Manual & Interface Verification Suite** via **Swagger UI** for the Backend REST APIs. Testing execution follows the **F.I.R.S.T** core testing principles (Fast, Independent, Repeatable, Self-Validating, Timely).

---

## 2. Backend API Test Cases Matrix (Swagger Verification)
The following test cases must be executed and passed before the backend layer can be certified as production-ready.

### 2.1 Epic: Task Fetching Engine (GET Endpoints)
* **TC-GET-001 (Fetch All):** Verify that `GET /api/tasks` returns an HTTP Status Code `200 OK` along with a valid JSON Array containing the seeded in-memory tasks.
* **TC-GET-002 (Fetch Single Valid ID):** Verify that `GET /api/tasks/{id}` with a pre-existing numeric ID returns `200 OK` and matches the exact object payload.
* **TC-GET-003 (Fetch Invalid ID):** Verify that `GET /api/tasks/{id}` with a non-existent ID (e.g., `9999`) successfully returns an HTTP Status Code `404 NotFound` with an explicit error message payload.

### 2.2 Epic: Task Generation Engine (POST Endpoints)
* **TC-POST-001 (Valid Task Creation):** Verify that a `POST /api/tasks` request with a complete valid payload (Title, Description, Priority, DueDate) returns `201 Created`, yields a newly assigned auto-incremented `Id`, and registers the item inside the system.
* **TC-POST-002 (Empty Title Validation):** Verify that sending a payload with an empty or whitespace `Title` string immediately returns an HTTP Status Code `400 BadRequest`, explicitly blocking transaction execution.

### 2.3 Epic: Task Modification Engine (PUT Endpoints)
* **TC-PUT-001 (Valid Update):** Verify that a `PUT /api/tasks/{id}` request with a modified status (e.g., changing status from `"To Do"` to `"In Progress"`) returns `204 NoContent`, updating the system state instantly.
* **TC-PUT-002 (Update Non-Existent ID):** Verify that an update request targeted at an invalid `Id` returns `404 NotFound`.

### 2.4 Epic: Task Purge Engine (DELETE Endpoints)
* **TC-DELETE-001 (Successful Deletion):** Verify that running a `DELETE /api/tasks/{id}` on an active task successfully returns `204 NoContent` and removes it from subsequent `GET` fetches.

---

## 3. Frontend UI Testing Gates (Future Validation)
* **TC-UI-001 (Grid Lane Rendering):** The application screen must dynamically construct 3 distinct visual columns representing the exact backend status states.
* **TC-UI-002 (Reactive Sync):** Form submissions must call the backend API cleanly and update the localized React state machine with zero refresh cycles.
---
