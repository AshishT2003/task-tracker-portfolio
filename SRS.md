# 📄 Document 2: Software Requirement Specification (SRS)

> **Project:** Task Management System (Kanban Style)  
> **Version:** 1.0.0  
> **Author:** Ashish Thombare  
> **Date:** 10-Oct-2026  
> **Status:** DRAFT - Awaiting Implementation

---

## 1. Introduction & Purpose

This document provides a comprehensive breakdown of the Functional and Non-Functional requirements for the Kanban-style Task Management System. It serves as a single source of truth for design, development, and testing alignment.

---

## 2. Functional Requirements (FR) & User Stories

Functional requirements describe what the system must do. These are broken down into agile **User Stories** from the user's perspective.

### 2.1 Epic: Task CRUD Lifecycle

- **FR-1 (Create Task):** The system must allow users to input a mandatory `Title`, an optional `Description`, select a `Priority` level, and assign an optional `DueDate`.
  - **User Story:** _As a user, I want to create a new task so that I can log my upcoming work into the system._
- **FR-2 (Read/View Tasks):** The system must fetch all logged tasks and group them visibly under their respective columns (`To Do`, `In Progress`, `Done`).
  - **User Story:** _As a user, I want to see all my tasks organized into visual columns so that I can immediately evaluate my daily progress._
- **FR-3 (Update Task Details):** The system must allow users to edit the text fields, priority, or due date of any pre-existing task.
  - **User Story:** _As a user, I want to modify task specifications when project mandates change._
- **FR-4 (Delete Task):** The system must allow users to completely purge a task from the board.
  - **User Story:** _As a user, I want to delete accidental or obsolete tasks to keep my board clutter-free._

### 2.2 Epic: Board State Transitions

- **FR-5 (Status Update):** The system must change a task's `Status` property immediately when it is moved across vertical columns (`To Do` ➔ `In Progress` ➔ `Done`).
  - **User Story:** _As a user, I want to move tasks between columns so that my board reflects the current operational stage of my work._

---

## 3. Non-Functional Requirements (NFR)

Non-functional requirements specify the operational criteria and constraints under which the software executes.

- **NFR-1 (Reliability & Data Consistency):** The API must enforce strict validation rules. Under no circumstances should an invalid state transition or empty title compromise data sanity.
- **NFR-2 (Performance & Latency):** Backend API endpoint processing execution (excluding network transit latency) must return payloads within less than 200 milliseconds, ensuring a highly responsive architecture.
- **NFR-3 (Maintainability & Extensibility):** The internal systems must enforce **Separation of Concerns (SoC)**. Business rules must reside strictly within the Backend Service layer, detached from controllers and frontend visual UI view rendering code.

---

## 4. Technical Constraints & Data Validation Matrix

The interface must strictly deny incorrect data payloads using these rules:

1. **Title Validation:** String, mandatory, minimum 3 characters, maximum 100 characters.
2. **Description Validation:** String, optional, maximum 500 characters.
3. **Status Enums:** Must strictly belong to `["To Do", "In Progress", "Done"]`.
4. **Priority Enums:** Must strictly belong to `["Low", "Medium", "High"]`.

---
