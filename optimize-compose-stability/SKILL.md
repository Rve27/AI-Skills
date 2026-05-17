---
name: optimize-compose-stability
description: Diagnoses and fixes Jetpack Compose stability issues to prevent unnecessary recompositions. Use when a project experiences UI performance lag, high recomposition counts in the Layout Inspector, or when adding new domain models and UI state classes.
---

# Optimize Compose Stability

This skill provides a structured workflow to identify and resolve "unstable" parameters in Jetpack Compose, ensuring efficient recomposition and smooth UI performance.

## Workflow

When tasked with optimizing Compose performance or fixing stability issues, follow these steps:

### 1. Analysis & Auditing
*   **Identify Suspects:** Look for classes using `java.util.Date`, standard Kotlin collections (`List`, `Set`, `Map`), or mutable properties (`var`).
*   **Check Compiler Reports:** If available, analyze reports in `build/compose_reports` and `build/compose_metrics`.
*   **Layout Inspector:** Use the "Show Recomposition Counts" feature to pinpoint components with excessive updates.

### 2. Implementation
For detailed rules and patterns, refer to [references/stability-guidelines.md](references/stability-guidelines.md).

*   **Refactor Data Models:** 
    *   Replace `java.util.Date` with `java.time.Instant` or `Long`.
    *   Convert standard collections to `ImmutableList`, `ImmutableSet`, or `ImmutableMap` from `kotlinx.collections.immutable`.
*   **Apply Stability Annotations:** Use `@Immutable` for immutable models and `@Stable` for observable or predictable mutable types.
*   **Configure Compiler:**
    *   Set up `compose_stability.conf` for external library types.
    *   Enable **Strong Skipping Mode** in `build.gradle.kts` for Compose Compiler 2.0+.

### 3. Verification
*   **Run Build:** Ensure the project compiles with new dependencies (e.g., `kotlinx-collections-immutable`).
*   **Verify Metrics:** Regenerate compiler reports to confirm the classes are now marked as `stable`.
*   **Benchmarking:** If possible, verify 60 FPS scrolling and reduced recomposition counts in the Layout Inspector.

## Detailed Guidelines
See [references/stability-guidelines.md](references/stability-guidelines.md) for:
*   Dependency configuration for immutable collections.
*   Templates for `compose_stability.conf`.
*   Gradle snippets for enabling metrics and strong skipping mode.
*   `derivedStateOf` patterns for high-frequency state management.
