# FileManager C++ Class - Usage Guide

## Overview

The `FileManager` class is a simple C++ utility for managing user data stored in a CSV-formatted text file. It provides functionality for user authentication, registration, and balance management.

## Features

- Add new users
- Authenticate users (login)
- Retrieve user information
- Update user balances
- Check if users exist
- Initialize database with test data

## Data Structure

### User Struct
```cpp
struct User {
  std::string username;
  std::string password;
  std::string balance;
};
```

### File Format
The data is stored in CSV format:
```
username,password,balance
```

Example:
```
aaronmathew,password,100000
john_doe,mypass123,5000
jane_smith,secure456,15000
```

## Installation

Include both header and implementation files in your project:
  - `FileManager.h`
  - `FileManager.cpp`

## Usage Examples

### 1. Initialize the FileManager

```cpp
#include "FileManager.h"

int main() {
    // Create FileManager instance with default file (users.txt)
    FileManager fm;
    
    // Or specify a custom file
    FileManager fm("custom_users.txt");
    
    return 0;
}
```

### 2. Initialize Database with Test Data

```cpp
FileManager fm;
fm.initializeFile();
// Creates users.txt with test user: aaronmathew,password,100000
```

### 3. Add a New User

```cpp
FileManager fm;

bool success = fm.addUser("john_doe", "mypassword123");
if (success) {
    std::cout << "User registered successfully!\n";
} else {
    std::cout << "Registration failed. User may already exist.\n";
}
```

### 4. Authenticate a User (Login)

```cpp
FileManager fm;

User* user = fm.getUser("john_doe", "mypassword123");
if (user != nullptr) {
    std::cout << "Login successful!\n";
    std::cout << "Username: " << user->username << "\n";
    std::cout << "Balance: " << user->balance << "\n";
    
    // Don't forget to delete the user object
    delete user;
} else {
    std::cout << "Invalid username or password\n";
}
```

### 5. Get User by Username Only

```cpp
FileManager fm;

User* user = fm.getUserByUsername("john_doe");
if (user != nullptr) {
    std::cout << "User found: " << user->username << "\n";
    std::cout << "Balance: " << user->balance << "\n";
    delete user;
} else {
    std::cout << "User not found\n";
}
```

### 6. Update User Balance

```cpp
FileManager fm;

bool success = fm.updateBalance("john_doe", "10000");
if (success) {
    std::cout << "Balance updated successfully!\n";
} else {
    std::cout << "Failed to update balance\n";
}
```

### 7. Check if User Exists

```cpp
FileManager fm;

if (fm.userExists("john_doe")) {
    std::cout << "User exists in the system\n";
} else {
    std::cout << "User not found\n";
}
```

## Complete Example: User Registration and Login System

```cpp
#include "FileManager.h"
#include <iostream>

int main() {
    FileManager fm;
    
    // Initialize file with test data
    fm.initializeFile();
    
    // Register a new user
    std::cout << "=== User Registration ===\n";
    if (fm.addUser("alice", "alice123")) {
        std::cout << "Alice registered successfully!\n\n";
    }
    
    // Login
    std::cout << "=== User Login ===\n";
    User* user = fm.getUser("alice", "alice123");
    if (user != nullptr) {
        std::cout << "Welcome, " << user->username << "!\n";
        std::cout << "Your balance: $" << user->balance << "\n\n";
        
        // Update balance
        std::cout << "=== Updating Balance ===\n";
        fm.updateBalance("alice", "5000");
        
        // Check updated balance
        delete user; // Clean up old user object
        user = fm.getUserByUsername("alice");
        std::cout << "New balance: $" << user->balance << "\n";
        
        delete user; // Clean up
    } else {
        std::cout << "Login failed!\n";
    }
    
    return 0;
}
```

## Important Notes

### Memory Management
- The `getUser()` and `getUserByUsername()` methods return dynamically allocated `User` objects
- **Always delete the returned User pointer** after use to prevent memory leaks
- Consider using smart pointers (`std::unique_ptr<User>`) for automatic memory management

### Error Handling
- Methods return `nullptr` or `false` on failure
- Error messages are printed to `std::cerr`
- Always check return values before proceeding

### File Operations
- The file is opened and closed for each operation
- For high-frequency operations, consider implementing caching
- The entire file is read into memory for balance updates

### Security Considerations
⚠️ **WARNING**: This implementation is for educational purposes only and should NOT be used in production without significant improvements:

- **Passwords are stored in plain text** - Use proper password hashing (bcrypt, argon2, etc.)
- **No input validation** - Validate and sanitize all user inputs
- **No concurrent access protection** - Not thread-safe or multi-process safe
- **CSV injection possible** - Usernames/passwords with commas will break the format

## API Reference

### Constructor
```cpp
FileManager(const std::string &file = "users.txt")
```
Creates a FileManager instance for the specified file.

### Methods

| Method | Return Type | Description |
|--------|-------------|-------------|
| `addUser(username, password)` | `bool` | Adds a new user with balance 0 |
| `getUser(username, password)` | `User*` | Authenticates and returns user (or nullptr) |
| `getUserByUsername(username)` | `User*` | Returns user by username only (or nullptr) |
| `updateBalance(username, newBalance)` | `bool` | Updates user's balance |
| `userExists(username)` | `bool` | Checks if username exists |
| `initializeFile()` | `void` | Creates file with test user if it doesn't exist |

## Troubleshooting

### "Failed to open file for reading"
- Ensure the file exists or call `initializeFile()` first
- Check file permissions
- Verify the file path is correct

### "User already exists"
- The username is already registered
- Use `userExists()` to check before adding

### "User not found"
- Verify the username is correct
- Check if the file is properly formatted
- Ensure data hasn't been corrupted

## License

This code is provided as-is for educational purposes.

---

**Last Updated**: December 2025
