**What is Side Effects**: In jetpack compose, side effects is any operation in composable function that interacts with or modifies something outside it's scope, potentially influence app's behavior or state beyond the UI. Side effects are actions that go beyond simply rendering the UI based on the current state, such as:

- Making network call
- Updating external shared state
- Launching coroutines
- Trigering notifications
- Accessing database or file system
- Log something

Composable are designed to be stateless and declarative, Jetpack compose provide specific api like(LaunchEffect, rememberCoroutineScope, rememberUpdatedState, DisposableEffect, SideEffect etc...) to manage this operation within the composition lifecycle. This allows side effects to be controlled, avoiding unwanted behaviors and ensuring the UI remains consistent and performant.

**Why Side Effects are needed**: Based on Jetpack Compose documentation a composable function may recompose one or many times, and now think of a scenario where we want to fetch some data from an API when a screen loads. Here, If we don't use side effects and place the network call directly in the composable function, it will execute the API request every time the composable recomposes, which could lead to multiple unnecessary API calls.

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

It could decrease app performance, make the app laggy, consuming extra network, battery and memory resources. So this is a big headache for us.

So how do we fixed this problem? here, Side Effects come to play. Jetpack compose provide some specific api like(LaunchEffect, SideEffect, DisposableEffect etc..) to handle side effects.

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
- ==Unnecessary execution==: 

Types of Side Effects in Jetpack Compose
1. LaunchedEffect
2. rememberCoroutinesScope
3. DisposableEffect
4. SideEffect
5. ProduceState
6. rememberUpdatedState