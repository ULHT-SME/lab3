# Lab3

## Description

This hands-on lab introduces students to state management in Flutter. Students will start with simple setState() patterns, build a Todo application, and then refactor it to use the Provider package for more scalable state management. By the end of this lab, students will understand different approaches to managing app state and when to use each pattern.

## Learning Objectives

By completing this lab, students will be able to:

- Understand the concept of state in Flutter and differentiate between stateful and stateless widgets
- Implement local state management using setState() for simple UI updates
- Build a functional Todo application with add and delete operations
- Refactor an application to use Provider for centralized state management
- Recognize when to use setState() versus Provider for state management
- Handle user input and update UI based on state changes

## Setup Instructions

### 1. Create a New Flutter Project

Option 1: Open your terminal/command prompt and run:

```bash
flutter create todo_state_app
cd todo_state_app
```

Option 2: Open Android Studio and go to File > New Project > New Flutter Project. Name it lab2. (Skip Step 2)

### 2. Open the project

Open the project folder in your preferred IDE.


### 3. Add Provider Package

Open `pubspec.yaml` and add the provider package under dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

Open a terminal in Android Studio > Run to install the package with the following command:

```bash
flutter pub get
```

### 4. Open and Run the Project

Open the project in your IDE and run:

```bash
flutter run
```

or

In Android Studio press the green icon ▶️ with the chosen device (Emulator of Phisical mobile)

---

## Lab Tasks

### Task 1: Understanding setState with a Counter

**Objective:** Learn the basics of state management with a simple counter example.

**What is State?**
State is information that can change over time and affects what is displayed on the screen. When state changes, Flutter rebuilds the affected parts of the UI.

**Your Challenge:**
1. Replace `main.dart` with a simple counter app
2. Understand how setState() triggers UI updates
3. Experiment with incrementing and decrementing the counter

**Starter Code:**
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'State Management Lab',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CounterScreen(),
    );
  }
}

class CounterScreen extends StatefulWidget {
  @override
  _CounterScreenState createState() => _CounterScreenState();
}

class _CounterScreenState extends State<CounterScreen> {
  int _counter = 0;

  void _incrementCounter() {
    // TODO: Use setState to update _counter
    // Hint: make use setState(() {  });
  }

  void _decrementCounter() {
    // TODO: Use setState to update _counter
    // Hint: Only decrement if _counter > 0
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Counter with setState'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Counter Value:',
              style: TextStyle(fontSize: 24),
            ),
            Text(
              '$_counter',
              style: TextStyle(fontSize: 72, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 40),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                // TODO: Add decrement button
                SizedBox(width: 20),
                // TODO: Add increment button
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

**Key Concepts:**
- `StatefulWidget` holds mutable state
- `setState(() { ... })` tells Flutter to rebuild the widget
- State variables (like `_counter`) are stored in the State class

**Test Your Understanding:**
- What happens if you modify `_counter` without calling `setState()`?
- Try adding a reset button that sets the counter back to 0

### Task 2: Build Todo App UI 

**Objective:** Create the user interface for a Todo application.

**Your Challenge:**
1. Create a new screen called `TodoListScreen`
2. Add a TextField for entering new tasks
3. Add a button to submit tasks
4. Display a ListView of existing tasks

**Todo Screen Structure:**
```dart
// Add this after CounterScreen in main.dart
class TodoListScreen extends StatefulWidget {
  @override
  _TodoListScreenState createState() => _TodoListScreenState();
}

class _TodoListScreenState extends State<TodoListScreen> {
  final TextEditingController _textController = TextEditingController();
  final List<String> _todos = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My Todo List'),
      ),
      body: Column(
        children: [
          // Input Section
          Padding(
            padding: EdgeInsets.all(16),
            child: Row(
              children: [
                Expanded(
                  child: TextField(
                    controller: _textController,
                    decoration: InputDecoration(
                      labelText: 'Enter a task',
                      border: OutlineInputBorder(),
                      // TODO: Add hintText
                    ),
                  ),
                ),
                SizedBox(width: 10),
                ElevatedButton(
                  onPressed: () {
                    // TODO: Implement add task functionality in next task
                    print('Add button pressed');
                  },
                  child: Icon(Icons.add),
                ),
              ],
            ),
          ),
          
          Divider(),
          
          // Todo List Section
          Expanded(
            child: _todos.isEmpty
                ? Center(
                    child: Text(
                      'No tasks yet! Add one above.',
                      style: TextStyle(fontSize: 18, color: Colors.grey),
                    ),
                  )
                : ListView.builder(
                    itemCount: _todos.length,
                    itemBuilder: (context, index) {
                      return ListTile(
                        leading: Icon(Icons.task_alt, color: Colors.blue),
                        title: Text(_todos[index]),
                        trailing: IconButton(
                          icon: Icon(Icons.delete, color: Colors.red),
                          onPressed: () {
                            // TODO: Implement delete functionality in next task
                            print('Delete ${_todos[index]}');
                          },
                        ),
                      );
                    },
                  ),
          ),
        ],
      ),
    );
  }

  @override
  void dispose() {
    _textController.dispose();
    super.dispose();
  }
}
```

**Update MyApp to use TodoListScreen:**
```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'State Management Lab',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TodoListScreen(), // Changed from CounterScreen
    );
  }
}
```

**Key Concepts:**
- `TextEditingController` manages text input
- `ListView.builder` efficiently displays lists
- Always dispose controllers in `dispose()` method

### Task 3: Implement Add and Delete with setState 

**Objective:** Add functionality to create and delete todo items using setState.

**Your Challenge:**
1. Implement the add task functionality
2. Implement the delete task functionality
3. Add input validation (don't add empty tasks)
4. Clear the TextField after adding a task

**Add Task Method:**
```dart
void _addTodo() {
  // TODO: Get text from _textController
  // TODO: Check if text is not empty (use trim())
  // TODO: Use setState to add the task to _todos list
  // TODO: Clear the TextField after adding
  
  // Hint: textController has a method called trim()
  // Hint: you can add items to an array using .add(...)
  // Hint: textController has a method called clear()
}
```

**Delete Task Method:**
```dart
void _deleteTodo(int index) {
  // TODO: Use setState to remove the task at the given index
  // Hint: _todos.removeAt(index)
}
```

**Update Your Button onPressed:**
```dart
ElevatedButton(
  onPressed: _addTodo,
  child: Icon(Icons.add),
),
```

**Update Your Delete IconButton:**
```dart
trailing: IconButton(
  icon: Icon(Icons.delete, color: Colors.red),
  onPressed: () => _deleteTodo(index),
),
```

**Validation Enhancement:**
Add a SnackBar for empty input:
```dart
void _addTodo() {
  String taskText = _textController.text.trim();
  
  if (taskText.isEmpty) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('Please enter a task')),
    );
    return;
  }
  
  // TODO: Add the task using setState
}
```

**Test Your App:**
- Try adding several tasks
- Delete tasks from different positions
- Try submitting an empty task
- Notice how the UI updates immediately

### Task 4: Refactor to Use Provider 

**Objective:** Refactor the Todo app to use Provider for centralized state management.

**Why Provider?**
- Separates business logic from UI
- Makes state accessible across multiple screens
- Easier to test and maintain
- Better for apps with complex state

**Your Challenge:**
1. Create a `TodoProvider` class to manage state
2. Wrap your app with `ChangeNotifierProvider`
3. Update the UI to use `Consumer` or `context.watch()`

**Step 1: Create the Provider Class**

Create a new file `lib/providers/todo_provider.dart`:

```dart
import 'package:flutter/foundation.dart';

class TodoProvider extends ChangeNotifier {
  final List<String> _todos = [];

  // Getter to access todos
  List<String> get todos => _todos;

  // Add a todo
  void addTodo(String task) {
    if (task.trim().isEmpty) return;
    
    // TODO: Add task to _todos list
    // TODO: Call notifyListeners() to update UI
  }

  // Delete a todo
  void deleteTodo(int index) {
    // TODO: Remove task at index
    // TODO: Call notifyListeners() to update UI
  }

  // Get count of todos
  int get todoCount => _todos.length;
}
```

**Step 2: Wrap App with Provider**

Update `main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'providers/todo_provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => TodoProvider(),
      child: MyApp(),
    ),
  );
}
```

**Step 3: Refactor TodoListScreen to Use Provider**

Create a new version of the screen:

```dart
class TodoListScreenWithProvider extends StatelessWidget {
  final TextEditingController _textController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todo with Provider'),
        actions: [
          // Show todo count in AppBar
          Center(
            child: Padding(
              padding: EdgeInsets.only(right: 16),
              child: Consumer<TodoProvider>(
                builder: (context, todoProvider, child) {
                  return Text(
                    '${todoProvider.todoCount} tasks',
                    style: TextStyle(fontSize: 16),
                  );
                },
              ),
            ),
          ),
        ],
      ),
      body: Column(
        children: [
          // Input Section
          Padding(
            padding: EdgeInsets.all(16),
            child: Row(
              children: [
                Expanded(
                  child: TextField(
                    controller: _textController,
                    decoration: InputDecoration(
                      labelText: 'Enter a task',
                      border: OutlineInputBorder(),
                      hintText: 'What needs to be done?',
                    ),
                  ),
                ),
                SizedBox(width: 10),
                ElevatedButton(
                  onPressed: () {
                    // TODO: Get the provider using context.read<TodoProvider>()
                    // TODO: Call addTodo with the text from controller
                    // TODO: Clear the text field
                    
                    // Hint: Provider.of<TodoProvider>(context, listen: false)
                    // Or: context.read<TodoProvider>()
                  },
                  child: Icon(Icons.add),
                ),
              ],
            ),
          ),
          
          Divider(),
          
          // Todo List Section with Consumer
          Expanded(
            child: Consumer<TodoProvider>(
              builder: (context, todoProvider, child) {
                if (todoProvider.todos.isEmpty) {
                  return Center(
                    child: Text(
                      'No tasks yet! Add one above.',
                      style: TextStyle(fontSize: 18, color: Colors.grey),
                    ),
                  );
                }
                
                return ListView.builder(
                  itemCount: todoProvider.todos.length,
                  itemBuilder: (context, index) {
                    return ListTile(
                      leading: Icon(Icons.task_alt, color: Colors.blue),
                      title: Text(todoProvider.todos[index]),
                      trailing: IconButton(
                        icon: Icon(Icons.delete, color: Colors.red),
                        onPressed: () {
                          // TODO: Delete the todo using provider
                        },
                      ),
                    );
                  },
                );
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

**Update MyApp:**
```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'State Management Lab',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TodoListScreenWithProvider(),
    );
  }
}
```

**Key Provider Concepts:**
- `ChangeNotifier` - base class for state classes
- `notifyListeners()` - triggers UI rebuild
- `Consumer<T>` - rebuilds when state changes
- `context.read<T>()` - access provider without listening
- `context.watch<T>()` - access provider with listening

### Task 5: Challenge - Add Checkbox for Complete Status

**Objective:** Extend the Todo app to track completed tasks.

**Your Challenge:**
1. Create a `Todo` model class with title and completed status
2. Update TodoProvider to use the Todo model
3. Add checkbox functionality to mark tasks complete

**Todo Model:**
```dart
// Add to lib/models/todo.dart
class Todo {
  String title;
  bool isCompleted;

  Todo({
    required this.title,
    this.isCompleted = false,
  });
}
```

**Updated TodoProvider:**
```dart
import 'package:flutter/foundation.dart';
import '../models/todo.dart';

class TodoProvider extends ChangeNotifier {
  final List<Todo> _todos = [];

  List<Todo> get todos => _todos;

  void addTodo(String title) {
    ...
    notifyListeners();
  }

  void deleteTodo(int index) {
    ...
    notifyListeners();
  }

  void toggleComplete(int index) {
    ...
    notifyListeners();
  }

  int get todoCount => _todos.length;
  int get completedCount => _todos.where((todo) => todo.isCompleted).length;
}
```

**Updated ListTile:**
```dart
ListTile(
  leading: Checkbox(
    value: todoProvider.todos[index].isCompleted,
    onChanged: (value) {
      // TODO: Call toggleComplete on provider
    },
  ),
  title: Text(
    todoProvider.todos[index].title,
    style: TextStyle(
      decoration: todoProvider.todos[index].isCompleted
          ? TextDecoration.lineThrough
          : TextDecoration.none,
    ),
  ),
  trailing: IconButton(
    icon: Icon(Icons.delete, color: Colors.red),
    onPressed: () => todoProvider.deleteTodo(index),
  ),
)
```

---

## Deliverables

You are required to .zip file this project and deliver it in Moodle before the next class. The .zip should contain all the content of inside project folder with the exception of the .dart_tool and build folders (these will make the .zip file extremely large and they are not necessary for evaluation).

---

## Tips and Resources

### Common Issues and Solutions

**Provider not found error:**
- Make sure ChangeNotifierProvider wraps your MaterialApp in main()
- Check that you've run `flutter pub get` after adding provider to pubspec.yaml

**UI not updating:**
- Verify you're calling `notifyListeners()` in Provider methods
- Ensure you're using `Consumer` or `context.watch()` to listen to changes
- With setState, make sure the state change is inside `setState(() { })`

**TextEditingController issues:**
- Remember to dispose controllers in StatefulWidgets
- StatelessWidgets can create controllers but be careful with rebuilds

### Best Practices

- Keep state classes focused (Single Responsibility Principle)
- Use `context.read()` for actions that don't need to listen
- Use `Consumer` or `context.watch()` for UI that needs updates
- Separate models from providers for better organization
- Always validate user input before updating state
