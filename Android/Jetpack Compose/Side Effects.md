**What is Side Effects**: In jetpack compose, side effects is any operation in composable function that interacts with or modifies something outside it's scope, potentially influence app's behavior or state beyond the UI. Side effects are actions that go beyond simply rendering the UI based on the current state, such as:

- Making network call
- Updating external shared state
- Launching coroutines
- Triggering notifications
- Accessing database or file system
- Log something

Composable are designed to be stateless and declarative, Jetpack compose provide specific API like(LaunchEffect, rememberCoroutineScope, rememberUpdatedState, DisposableEffect, SideEffect etc...) to manage this operation within the composition lifecycle. This allows side effects to be controlled, avoiding unwanted behaviors and ensuring the UI remains consistent and performant.

**Why Side Effects**: Based on Jetpack Compose documentation a composable function may recompose one or many times, and now think of a scenario where we want to fetch some data from an API when a screen loads. Here, If we don't use side effects and place the network call directly in the composable function, it will execute the API request every time the composable recomposes, which could lead to multiple unnecessary API calls.

```
@Composable
fun UserScreen(viewModel: UserViewModel) {
    // This will re-fetch data every time the screen recomposes
    val userData by viewModel.userData.observeAsState()

    // Directly calling the data fetching function inside the composable
    viewModel.fetchUserData()

    Column {
        Text(text = "User Data: ${userData ?: "Loading..."}")
    }
}
```

It could decrease app performance, make the app leggy, consuming extra network, battery and memory resources. So this would be a big headache for us.

So how do we fixed this problem? here, Side Effects come to play. Jetpack compose provide some specific API like(LaunchEffect, SideEffect, DisposableEffect etc..) to handle side effects.

```
@Composable
fun UserScreen(viewModel: UserViewModel) {
    val userData by viewModel.userData.observeAsState()

    // Use LaunchedEffect to ensure this runs only once when the composable is first added to the composition
    LaunchedEffect(Unit) {
        viewModel.fetchUserData()
    }

    Column {
        Text(text = "User Data: ${userData ?: "Loading..."}")
    }
}
```

If we don't use side effect or use them incorrectly, it can lead to several issues in the app, affecting performance, user experience, and even stability.

**Some potential problem**
- `Unnecessary execution`: Without controlled side effects, some operation might be re-triggered every time a composable function recomposes.
- `State inconsistencies`: Side effects manage interactions with external dependencies or states that can impact UI consistency. Without them, the UI might not stay in sync with real-world data. For example, if you update some app-wide state(like user session data) without proper side effect management, it may result in an out-of-date or conflicting UI.
- `Memory leaks`: Some actions require cleanup, like removing listeners or stopping services. Without proper side effect manage, they continue running event after it's no longer needed. leading to memory leaks and increased battery usage on the devices. 
- `Missed one-time event`: Certain action should only execute once in response to a state change or user action, like starting timer or showing a welcome message on the first visit. Without side effects like `LaunchedEffect`, you might be trigger these actions multiple times. 
- `Lifecycle mismanagement`: Composable go through multiple lifecycle states, including recompositions. Without properly managed side effect long running task like coroutines may not stop as they should stop when a composable leaves the compositions, causing resource leaks, excessive CPU use or crash.

**Benefits of using Side Effect**
- `Efficient resource management`: Side effects like `LaunchedEffect`, `DisposableEffect` ensure that resources(network call, database connection, listeners) are managed efficiently. This prevent unnecessary network call, memory leaks or excessive CPU use by stopping task or listeners when they're no longer needed.
- `Consistency & predictability`: Side effect allows composable to maintain a consistency UI by executing tasks based on specific conditions or state changes. For example `LaunchedEffect` runs a task only when certain key change, ensuring that operations happen exactly when intended. This helps in avoiding unintended behavior due to recompositions.
- `Simplified lifecycle management`: Jetpack compose side effects tools automatically tie operations to the composable lifecycle. This removes the need for manual lifecycle handling, like managing activity/fragment lifecycles, making it easier to execute and clean up actions right time.
- `Improved user experience`: Side effects manage unnecessary delay, duplicate action, or data inconsistency. This leads to a smoother, more responsive UI.
- `State sunchronization`: Side effects are particularly useful when your UI depends on external states or systems, such as API's database, or hardware sensors. They allow you to synchronize UI state with these external dependencies efficiently and only when needed.

In short, side effects help streamline operations, prevent repetitive or wasteful actions, and improve the app's responsiveness, making side effects essential for managing real-world app behavior in Jetpack Compose.

**Types of Side Effects in Jetpack Compose**
- LaunchedEffect
- rememberCoroutinesScope
- DisposableEffect
- SideEffect
- ProduceState
- rememberUpdatedState

**LaunchedEffect**
