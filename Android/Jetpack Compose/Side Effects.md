### What is Side Effects
In jetpack compose, side effects is any operation in composable function that interacts with or modifies something outside it's scope, potentially influence app's behavior or state beyond the UI. Side effects are actions that go beyond simply rendering the UI based on the current state, such as:

- Making network call
- Updating external shared state
- Launching coroutines
- Triggering notifications
- Accessing database or file system
- Log something

Composable are designed to be stateless and declarative, Jetpack compose provide specific API like(LaunchEffect, rememberCoroutineScope, rememberUpdatedState, DisposableEffect, SideEffect etc...) to manage this operation within the composition lifecycle. This allows side effects to be controlled, avoiding unwanted behaviors and ensuring the UI remains consistent and performant.

### Why Side Effects
Based on Jetpack Compose documentation a composable function may recompose one or many times, and now think of a scenario where we want to fetch some data from an API when a screen loads. Here, If we don't use side effects and place the network call directly in the composable function, it will execute the API request every time the composable recomposes, which could lead to multiple unnecessary API calls.

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

### Some potential problem
- `Unnecessary execution`: Without controlled side effects, some operation might be re-triggered every time a composable function recomposes.
- `State inconsistencies`: Side effects manage interactions with external dependencies or states that can impact UI consistency. Without them, the UI might not stay in sync with real-world data. For example, if you update some app-wide state(like user session data) without proper side effect management, it may result in an out-of-date or conflicting UI.
- `Memory leaks`: Some actions require cleanup, like removing listeners or stopping services. Without proper side effect manage, they continue running event after it's no longer needed. leading to memory leaks and increased battery usage on the devices. 
- `Missed one-time event`: Certain action should only execute once in response to a state change or user action, like starting timer or showing a welcome message on the first visit. Without side effects like `LaunchedEffect`, you might be trigger these actions multiple times. 
- `Lifecycle mismanagement`: Composable go through multiple lifecycle states, including recompositions. Without properly managed side effect long running task like coroutines may not stop as they should stop when a composable leaves the compositions, causing resource leaks, excessive CPU use or crash.

### Benefits of using Side Effect
- `Efficient resource management`: Side effects like `LaunchedEffect`, `DisposableEffect` ensure that resources(network call, database connection, listeners) are managed efficiently. This prevent unnecessary network call, memory leaks or excessive CPU use by stopping task or listeners when they're no longer needed.
- `Consistency & predictability`: Side effect allows composable to maintain a consistency UI by executing tasks based on specific conditions or state changes. For example `LaunchedEffect` runs a task only when certain key change, ensuring that operations happen exactly when intended. This helps in avoiding unintended behavior due to recompositions.
- `Simplified lifecycle management`: Jetpack compose side effects tools automatically tie operations to the composable lifecycle. This removes the need for manual lifecycle handling, like managing activity/fragment lifecycles, making it easier to execute and clean up actions right time.
- `Improved user experience`: Side effects manage unnecessary delay, duplicate action, or data inconsistency. This leads to a smoother, more responsive UI.
- `State sunchronization`: Side effects are particularly useful when your UI depends on external states or systems, such as API's database, or hardware sensors. They allow you to synchronize UI state with these external dependencies efficiently and only when needed.

In short, side effects help streamline operations, prevent repetitive or wasteful actions, and improve the app's responsiveness, making side effects essential for managing real-world app behavior in Jetpack Compose.

### Types of Side Effects in Jetpack Compose
- LaunchedEffect
- rememberCoroutinesScope
- DisposableEffect
- SideEffect
- ProduceState
- rememberUpdatedState

### LaunchedEffect
`LaunchedEffect` in jetpack compose is a side-effect function designed to run a block of code within a coroutine when certain conditions are met, specially when the composable is first added to the composition tree or when its dependencies are change. This function is particularly useful for running asynchronous or one-time operations ties to the lifecycle of a composable, such as fetching data, starting animation, or handling one-time events.

### Key feature of LaunchedEffect
1. `Runs only once`: 
- When `LaunchedEffect` is provided a key or a dependencies, it executes its block of code only when this key changes. For example, if you pass `Unit` as the key, the effect will run only once when the composable enters the compositions.
-  By adding a dependency, it will run each time the dependency changes, making it ideal for running task that need to re-trigger based on specific state changes.
2.  `Runs on the composables' couroutine scope`:  `LaunchedEffect` runs its code block on the composable's scope, which automatically cancels the coroutine when the composable is removed from the composition. This lifecycle awareness prevents resources leaks and unnecessary background tasks when the composable is no longer needed.
3. `Safe for asynchronus task`: `LaunchedEffect` is a suspendable function, so you can safely perform asynchronous task(like network call) without blocking UI thread.

### What LaunchedEffect does
- Launces a coroutine in the background to perform your desired side effect.
- Ensures the coroutine starts only when the composable composition occurs.
- Cancels the coroutine automatically when the composable's is removed from the composition.
- Allows specifying dependencies to control the coroutine execution based on changes in data or state.

### Benefits of using LaunchedEffect
- Ensures asynchronous task are ties to the composable lifecycle. 
- Prevent redundant recompositions or repeated call by controlling when the code executed. 
- Automatically cancels tasks if the composables leaves the composition, managing resources effectively.
- Simplifies the handling of one-time events and state change in composable.

### Usage of LaunchedEffect
```
@Composable
fun WelcomeScreen(viewModel: WelcomeViewModel) {
    val userData by viewModel.userData.observeAsState()

    // LaunchedEffect with Unit as the key, so it runs only once when the composable enters composition
    LaunchedEffect(Unit) {
        viewModel.loadUserData() // Load user data only when this screen is first displayed
    }

    Column {
        Text(text = "Welcome, ${userData?.name ?: "Guest"}")
    }
}
```

<mark>Note</mark>
- `LaunchedEffect` should not directly update the UI state. Use composable state updates like `useState` to ensure proper recomposition.
- Avoid nesting complex logic within `LaunchedEffect`. Consider separate suspend functions for organization and clarity.

### rememberCoroutinesScope
`rememberCoroutineScop` in jetpack compose provides a `CoroutineScope` tied to the lifecycle of a composable. This allows you to launch coroutines safely from within composables, enabling actions like handling user interactions or triggering UI updates without being tied to a specific `LaunchedEffect` or recomposition. Unlike `LaunchedEffect`, `rememberCoroutineScope` does not automatically cancel coroutines when dependencies change or the screen recomposes, so you manage the coroutine's lifecycle more directly. 

### Why use rememberCoroutineScope
- `Triggering coroutines on user action`: It's ideal for handling events that happen based on user action rather than being tied to the lifecycle of the composable.
- `Launching coroutines outside of the LaunchedEffect`: `LaunchedEffect` automatically restart when key changes, which is not always needed. With `rememberCoroutineScope` you can trigger one-off events without restarting coroutines.
- `More control over coroutine lifecycle`: `remeberCoroutineScope` persists across recompositions, it's useful for event that need to maintain state even as the UI re-renders.

### Usage of rememberCoroutineScope
```
@Composable
fun SaveDataScreen(viewModel: DataViewModel) {
    val coroutineScope = rememberCoroutineScope()
    var isSaving by remember { mutableStateOf(false) }

    Button(onClick = {
        // Launch a coroutine on button click to save data
        coroutineScope.launch {
            isSaving = true
            viewModel.saveData()
            isSaving = false
        }
    }) {
        Text(if (isSaving) "Saving..." else "Save Data")
    }
}
```

<mark>Note</mark>
- `Lifecycle awarness`: The `CoroutineScope` created by `rememberCoroutineScope` is tied to the composable's lifecycle. When the composable leaves the composition the scop will canceled, avoiding potential memory leaks.
- `Avoiding automatic cancellation`: Unlike `LaunchedEffect`, the coroutine in `rememberCoroutineScop` does not cancel on recompositions, which makes it suitable for actions tied to specific events like user interactions
- `Manual cancelation`: If you need fine-grained control over the coroutine's lifecycle, you may still need to manage cancellation manually using `Job` or `MutableState` if the coroutine need to be stopped prematurely.  

### LaunchedEffect Vs rememberCoroutineScope
Both `LaunchedEffect` and `rememberCoroutineScope` are tools in Jetpack Compose for launching coroutines, but they serve different purposes and are suited to different use cases. Here’s a breakdown of the differences, benefits, and when to use each.

1. `Lifecycle & depedency awarness`:
	- `LaunchedEffect`
		- Tied directly to the composable's lifecycle
		- Automatically cancels and restarts the coroutines when dependencies or keys change.
		- Best for task that need to react to lifecycle changes or dependencies changes within a composable.
	- `rememberCoroutineScope`
		- Not automatically linked to any lifecycle dependency.
		- Persists across recompositions without being restarted, allowing you to launch coroutines without worrying about dependency changes.
		- Ideal for user-initiated actions that don't need to automatically restart on recomposition.
2. `Use case scenarios`:   
	 - `LaunchEffect`
		 - For side effects that should start and stop automatically with the composable lifecycle, or when specific keys change.
		 - `Example`: Loading data when a screen appears, where data needs to reload if the screen reappears or if the data source changes.
	- `rememberCoroutineScope`:
		- For actions that happen based on events, like button clicks, where you want more control and don't want automation cancellation or re-triggering on recompositions.
		- `Example`: A user clicks a button, triggering a CRUD operation on database
3. `Automatic cancellation & re-triggering`:
	- `LaunchedEffect`
		- Cancels any running coroutine whenever the composable is removed from the composition or a dependency key changes, ensuring no redundant tasks continue in the background.
		- This makes `LaunchedEffect` ideal for lifecycle-dependent actions where you don’t want background tasks running when the composable is inactive.
	- `rememberCoroutineScope`
		- The coroutine is not automatically canceled on recompositions. It is, however, canceled when the composable is permanently removed from the composition.
		- This makes it ideal for tasks that should continue despite recompositions, like tasks triggered by user interactions
4. `Code example`
- `LaunchedEffect`
```
@Composable
fun ProfileScreen(userId: String, viewModel: ProfileViewModel) {
    val userProfile by viewModel.userProfile.observeAsState()

    LaunchedEffect(userId) {
        viewModel.loadUserProfile(userId)
    }

    // UI to display the profile
    Text(text = userProfile?.name ?: "Loading...")
}
```
- `rememberCoroutineScope`
```
@Composable
fun SaveButton(viewModel: ProfileViewModel) {
    val coroutineScope = rememberCoroutineScope()
    var isSaving by remember { mutableStateOf(false) }

    Button(onClick = {
        coroutineScope.launch {
            isSaving = true
            viewModel.saveProfile()
            isSaving = false
        }
    }) {
        Text(if (isSaving) "Saving..." else "Save")
    }
}
```

5. `Summary`

| `Feature`              | `LaunchedEffect`                             | `rememberUpdateCoroutine`                       |
| ---------------------- | -------------------------------------------- | ----------------------------------------------- |
| Best fore              | Lifecycle-aware side effects                 | User-initiated actions                          |
| Lifecycle tied to      | Composable lifecycle, with dependency keys   | Composable, but not tied to dependency keys     |
| Recomposition behavior | Cancels and re-launches on dependency change | Persists across recompositions                  |
| Automatic cancellation | On key change or when composable exits       | Only when composable exits composition          |
| Ideal use case         | Loading data when a screen appears           | Handling button clicks or user-triggered events |
