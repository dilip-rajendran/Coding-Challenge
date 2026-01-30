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

## Testing Readiness

- Mock repositories
- ViewModel unit testing

---


## Known Issue - Search & SwiftUI Limitations

- `.searchable` does not reliably dismiss in `TabView`
- Explicit dismissal using tab selection observation

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
    <td><img src="https://github.com/user-attachments/assets/d460a172-a532-4ca5-b076-021fb4567c9b" width="302"/></td>
    <td><img src="https://github.com/user-attachments/assets/a184067b-473d-4549-9d0f-50227b7411a2" width="302"/></td>
    <td><img src="https://github.com/user-attachments/assets/c35e7307-6a44-4e5c-a59b-1f116ed66dfd" width="302"/></td>
  </tr>
</table>
