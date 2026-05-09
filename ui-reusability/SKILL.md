---
name: ui-reusability
description: Ensures UI components are reusable, modular, and placed in the ui/components/ directory. Use when creating new UI elements or refactoring existing ones to improve code maintainability and reduce repetition.
---

# UI Reusability

This skill focuses on maintaining a clean and DRY (Don't Repeat Yourself) UI layer by promoting the creation of reusable Jetpack Compose components.

## Guidelines

1. **Component Placement**: All reusable UI components must be placed in:
   `app/src/main/java/com/rve/systemmonitor/ui/components/`

2. **Decomposition**: Break down complex screens into smaller, manageable components. If a UI element is used more than once, it *must* be extracted into a reusable component.

3. **API Design**:
   - Use standard naming conventions (e.g., `RvCard`, `SystemMetricRow`).
   - Prefer passing `Modifier` as the first optional parameter to allow customization from the caller.
   - Use slot-based APIs (`content: @Composable () -> Unit`) for flexible containers.

4. **Theming**: Always use the project's custom Material 3 Expressive theme (`com.rve.systemmonitor.ui.theme`). Avoid hardcoding colors or typography.

5. **Preview**: Provide `@Preview` functions for all reusable components to facilitate UI development and testing.

## Example
When you see repeated UI patterns like a row with an icon and a value, extract it:
```kotlin
@Composable
fun MetricRow(
    icon: Painter,
    label: String,
    value: String,
    modifier: Modifier = Modifier
) {
    // Implementation...
}
```
