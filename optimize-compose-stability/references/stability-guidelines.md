# Jetpack Compose Stability Guidelines

This document provides detailed rules, patterns, and configuration templates for optimizing Jetpack Compose UI stability.

## 1. Data Model Refactoring

### Avoid Unstable Types
The Compose compiler must be able to verify that a class is immutable. If it can't, it marks the class as unstable, leading to unnecessary recompositions.

*   **java.util.Date:** DO NOT USE. It is mutable.
    *   **Alternative:** Use `java.time.Instant`, `java.time.LocalDateTime`, or `Long` (timestamps).
*   **Mutable Properties:** Avoid `var` in data classes. Prefer `val`.
*   **External Types:** Classes from external libraries (like `UUID` or third-party models) are often treated as unstable by default.

### Use Immutable Collections
Standard Kotlin interfaces like `List`, `Set`, and `Map` are considered unstable because their underlying implementation (e.g., `ArrayList`) might be mutable.

*   **Recommendation:** Use `kotlinx.collections.immutable`.
*   **Dependency:** `implementation("org.jetbrains.kotlinx:kotlinx-collections-immutable:0.4.0")`
*   **Pattern:**
    ```kotlin
    data class MyUiState(
        val items: ImmutableList<Item> = persistentListOf()
    )
    ```

## 2. Stability Annotations

### `@Immutable`
A promise to the compiler that the class's properties will never change after construction.
*   **Usage:** Use on data models where all properties are immutable.

### `@Stable`
A promise that the type is mutable, but Compose will be notified when changes occur.
*   **Usage:** Use for types that implement an observer pattern or whose public properties always return the same result for the same instance.

> [!WARNING]
> Do not lie to the compiler. Using these on truly mutable classes without proper notification can cause UI bugs where the screen doesn't update.

## 3. Compiler Configuration

### `compose_stability.conf`
For classes you don't own (external libraries), create a configuration file to mark them as stable.

1.  Create `compose_stability.conf` in your module.
2.  Add classes/packages:
    ```
    com.myapp.models.*
    java.time.Instant
    java.util.UUID
    ```
3.  Configure in `build.gradle.kts`:
    ```kotlin
    composeCompiler {
        stabilityConfigurationFile = project.file("compose_stability.conf")
    }
    ```

### Strong Skipping Mode
Enables the compiler to skip recomposition even with unstable parameters by using structural comparison.
*   **Enable in `build.gradle.kts`:**
    ```kotlin
    composeCompiler {
        enableStrongSkippingMode = true
    }
    ```

## 4. State Hoisting & ViewModel Patterns

Passing a ViewModel directly to a Composable can hinder stability, reusability, and testability. Instead, use **State Hoisting** to create "Stateless" Composables.

### The "Stateless" Screen Pattern
Separate your UI into a **Stateful** entry point and a **Stateless** UI implementation.

1.  **Stateful (Entry Point):** Handles ViewModel initialization, state collection, and navigation.
2.  **Stateless (UI):** Receives only the state and lambdas for actions.

```kotlin
// Stateful Entry Point (e.g., in Navigation Entry)
@Composable
fun UserProfileScreen(viewModel: UserViewModel = viewModel()) {
    val uiState by viewModel.uiState.collectAsStateWithLifecycle()
    
    // Pass only state and callbacks
    UserProfileContent(
        uiState = uiState,
        onRefresh = { viewModel.refresh() }
    )
}

// Stateless UI Implementation (Easy to Preview & Test)
@Composable
fun UserProfileContent(
    uiState: UserUiState,
    onRefresh: () -> Unit
) {
    // UI Logic here
}
```

### Why This Improves Stability
*   **Decoupling:** The UI doesn't depend on the ViewModel implementation.
*   **Preview Support:** You can easily create previews with static `UiState` objects.
*   **Explicit State:** The Compose compiler can more easily verify the stability of simple data classes (`UiState`) compared to complex ViewModel instances.

### Choosing the Right Pattern
*   **Small/Internal Screens:** Passing ViewModel might be okay for speed.
*   **Standard Production Screens:** Pass a single `UiState` data class (ensure it's `@Immutable`).
*   **Highly Reusable Components:** Pass plain values (e.g., `title: String`, `onClick: () -> Unit`).

## 5. Debugging & Metrics

### Enable Compiler Reports
Identify "unstable" suspects by generating metrics reports.
*   **Configure in `build.gradle.kts`:**
    ```kotlin
    composeCompiler {
        reportsDestination = layout.buildDirectory.dir("compose_reports")
        metricsDestination = layout.buildDirectory.dir("compose_metrics")
    }
    ```

### Workflow
1.  **Layout Inspector:** Use "Show Recomposition Counts" to find high-frequency updates.
2.  **Run Reports:** Analyze the generated metrics to find unstable parameters.
3.  **derivedStateOf:** Use to buffer expensive calculations or high-frequency state changes (e.g., scroll position).
