# CountryInfo — Architecture & Engineering Approach

## High-Level Architecture

**Pattern:** MVVM + Repository  
**UI Framework:** SwiftUI  
**Persistence:** SwiftData  
**Concurrency:** Swift Concurrency (`async/await`)  

```
View (SwiftUI)
   ↓
ViewModel (ObservableObject, @MainActor)
   ↓
Repository (Persistence / Networking abstraction)
   ↓
SwiftData / URLSession
```

---

### Chosen:
- **MVVM with lightweight dependency injection**

### Not chosen:
- Clean Architecture with UseCases / Interactors
- Model-View-Controller
- Coordinator pattern

### Reasoning:
- MVVM provides **clear ownership boundaries**
- Keeps the codebase **approachable and readable**
- Repositories can easily evolve into use cases
- ViewModels already isolate business logic
---

## Repository Pattern

- Abstracts persistence
- Enables testing
- Prevents SwiftData leakage into UI

### Trade-off:
Adds indirection, but improves scalability and testability.

---

## Persistence (SwiftData)

- Native Apple persistence
- Minimal boilerplate
---

## Navigation

- `NavigationStack` with `NavigationPath`
- Type-safe destinations
- No coordinators to reduce complexity

---

## Concurrency Model

- `async/await` throughout
- Sequential awaits where consistency matters
- Readability prioritized over micro-optimizations

---

## Search Feature

- Real time search using REST API
- Asynchronous and Debounced Search
- Cancellation Support

---

## Testing Readiness

- Mock repositories
- ViewModel unit testing

---



This is my first project using SwiftData. While this implementation explores only a subset of its features, I plan to continue exploring SwiftData in greater depth in future projects.

### App Screens

<table>
  <tr>
    <td align="center"><b>Country List</b></td>
    <td align="center"><b>Country Details</b></td>
    <td align="center"><b>Saved List</b></td>
  </tr>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/5f073e5c-c921-4607-abe5-e435fb20e149" width="302"/></td>
    <td><img src="https://github.com/user-attachments/assets/a184067b-473d-4549-9d0f-50227b7411a2" width="302"/></td>
    <td><img src="https://github.com/user-attachments/assets/1835a5ab-c758-493b-a5c7-ac82ee410af8" width="302"/></td>
  </tr>
</table>

