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

## 4. Debugging & Metrics

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
