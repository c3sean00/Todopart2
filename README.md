# 📝 Todo App - Part 2

An Android Todo application that fetches real data from a REST API using Retrofit. Built with Jetpack Compose, MVVM architecture, and modern Android development practices.

## 📱 Description

This Todo application retrieves a list of todos from the JSONPlaceholder API and displays them in a clean, scrollable list. The app demonstrates API integration, coroutines for asynchronous operations, and proper state management using ViewModel.

## ✨ Features

- **REST API Integration:** Fetches real todo data from JSONPlaceholder API
- **Asynchronous Loading:** Uses Kotlin Coroutines for network calls
- **MVVM Architecture:** Clean separation between UI and business logic
- **Modern UI:** Built with Jetpack Compose and Material 3
- **Error Handling:** Proper exception handling for network failures
- **Lazy Loading:** Efficient list rendering with LazyColumn
- **Internet Permission:** Configured for network access

## 🏗️ Architecture

The app follows MVVM (Model-View-ViewModel) architecture:

- **Model:** `Todo` data class and `TodosApiService` (Retrofit interface)
- **ViewModel:** `TodoViewModel` - Manages API calls and UI state
- **View:** `TodoScreen` - Composable UI components

## 🛠️ Built With

- **Kotlin** - Primary programming language
- **Jetpack Compose** - Modern declarative UI toolkit
- **Material 3** - Latest Material Design components
- **ViewModel** - Lifecycle-aware state management
- **Retrofit** - Type-safe HTTP client for API calls
- **Gson** - JSON serialization/deserialization
- **Coroutines** - Asynchronous programming
- **Android Studio** - Official Android development environment

## 📡 API Integration

The app uses the [JSONPlaceholder API](https://jsonplaceholder.typicode.com/):

```kotlin
interface TodosApiService {
    @GET("todos")
    suspend fun getTodos(): List<Todo>
}
```

**Base URL:** `https://jsonplaceholder.typicode.com/`

## 🎨 Key Components

### Todo Data Model

```kotlin
data class Todo(
    val userId: Int,
    val id: Int,
    val title: String,
    val completed: Boolean
)
```

### TodoViewModel

Manages API calls and application state:

```kotlin
class TodoViewModel : ViewModel() {
    var todos: List<Todo> by mutableStateOf(listOf())

    init {
        getTodosList()
    }

    private fun getTodosList() {
        viewModelScope.launch {
            try {
                val apiService = TodosApiService.getInstance()
                todos = apiService.getTodos()
            } catch (e: Exception) {
                Log.d("TODOVIEWMODEL", e.message.toString())
            }
        }
    }
}
```

### TodoScreen

Displays the list of todos:

```kotlin
@Composable
fun TodoScreen(todoViewModel: TodoViewModel = viewModel()) {
    TodoList(todos = todoViewModel.todos)
}

@Composable
fun TodoList(todos: List<Todo>) {
    LazyColumn {
        items(todos) { todo ->
            Column {
                Text(text = todo.title)
                HorizontalDivider()
            }
        }
    }
}
```

## 🚀 Installation

1. Clone this repository:
   ```sh
   git clone https://github.com/c3sean00/Todopart2.git
   ```

2. Open the project in Android Studio

3. Make sure you have internet connection (app requires network access)

4. Build and run on an emulator or physical device

## 📋 Requirements

- Android Studio Hedgehog | 2023.1.1 or newer
- Minimum SDK: API 24 (Android 7.0)
- Target SDK: API 34 (Android 14)
- Kotlin 1.9+
- Internet connection (for API calls)

## 📦 Dependencies

```kotlin
dependencies {
    // Retrofit for API calls
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-gson:2.9.0")
    
    // ViewModel Compose
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.7.0")
    
    // Jetpack Compose
    implementation("androidx.compose.ui:ui")
    implementation("androidx.compose.material3:material3")
}
```

## 🔧 Permissions

The app requires internet permission in `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## 🔄 Future Improvements (Part 3+)

- Add loading indicator while fetching data
- Display error messages to user
- Add pull-to-refresh functionality
- Filter todos by completion status
- Add local caching with Room database
- Implement search functionality
- Add todo detail view
- Support for adding/editing/deleting todos

## 📝 License

This project is created for educational purposes.

## 👤 Author

**c3sean00**

- GitHub: [@c3sean00](https://github.com/c3sean00)

## 🔗 Related Projects

- [Todopart1](https://github.com/c3sean00/Todopart1) - Basic Todo app with static data

---
