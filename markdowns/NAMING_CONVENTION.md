# C++ Project Naming Convention

> **Purpose**  
This document defines a clear and consistent naming convention for our **group C++ school project**.  
Following this standard helps improve **readability**, **maintainability**, and **team collaboration**.

---

## 1. General Rules

- Use **English only** for all names
- Be **descriptive**, not abbreviated unless widely known
- Avoid vague names like `temp`, `data`, `stuff`
- Prefer **clarity over brevity**
- One concept = one name

---

## 2. File & Folder Naming

### 📁 Folders

- Use **lowercase + snake_case**
- Plural for collections

```txt
src/
include/
assets/
configs/
utils/
```

Examples:

```txt
game_logic/
input_handlers/
render_systems/
```

---

### 📄 Source & Header Files

- Use **snake_case**
- Header files: `.h` or `.hpp`
- Source files: `.cpp`
- Header and source must match names

```txt
player.cpp
player.h
render_system.cpp
render_system.h
```

---

## 3. Namespace Naming

- Use **lowercase**
- Short but meaningful
- Avoid `using namespace` in headers

```cpp
namespace game {
namespace utils {
}
}
```

---

## 4. Class & Struct Naming

- Use **PascalCase**
- Nouns only
- One class per file (recommended)

```cpp
class PlayerController;
struct Vector2;
```

Bad ❌
```cpp
class player;
class doStuff;
```

---

## 5. Function & Method Naming

- Use **camelCase**
- Verbs or verb phrases
- Boolean functions should start with `is`, `has`, `can`

```cpp
void updatePlayer();
bool isAlive() const;
int calculateScore();
```

---

## 6. Variable Naming

### 🔹 Local Variables

- **camelCase**
- Descriptive

```cpp
int playerHealth;
float deltaTime;
```

---

### 🔹 Member Variables

- **camelCase** + trailing underscore `_`

```cpp
class Player {
private:
    int health_;
    float speed_;
};
```

---

### 🔹 Global Variables

⚠️ Avoid if possible

- Prefix with `g_`

```cpp
int g_windowWidth;
```

---

## 7. Constants & Macros

### ✅ Constants

- Use `constexpr`
- **UPPER_SNAKE_CASE**

```cpp
constexpr int MAX_PLAYERS = 4;
constexpr float GRAVITY_FORCE = 9.8f;
```

---

### ❌ Macros (Avoid if possible)

If unavoidable:

```cpp
#define MAX_BUFFER_SIZE 1024
```

---

## 8. Enum Naming

- Enum type: **PascalCase**
- Enum values: **UPPER_SNAKE_CASE**

```cpp
enum class GameState {
    MAIN_MENU,
    RUNNING,
    PAUSED,
    GAME_OVER
};
```

---

## 9. Pointer & Reference Naming

- No special prefixes (`p`, `r`)
- Let the **type** explain it

```cpp
Player* player;
const Texture& texture;
```

---

## 10. Boolean Naming

- Always sound like a **question**

```cpp
bool isRunning;
bool hasInput;
bool canJump;
```

---

## 11. Comments Style

### Single-line

```cpp
// Updates player position
```

### Multi-line

```cpp
/*
 * Handles collision detection
 * between entities
 */
```

---

## 12. Git-Friendly Naming (Important for Groups)

- Do NOT rename files randomly
- Keep consistent casing (Linux is case-sensitive)
- Avoid special characters & spaces

---

## 13. Example Class Layout

```cpp
// player.h
#pragma once

class Player {
public:
    Player();

    void update(float deltaTime);
    bool isAlive() const;

private:
    int health_;
    float speed_;
};
```

---

## 14. Final Notes for Groupmates

✔ Follow this document strictly  
✔ Discuss naming **before coding**  
✔ If unsure, ask the group  
✔ Consistency > Personal Preference

---

**Document Version:** 1.0  
**Project Type:** School Group C++ Project

