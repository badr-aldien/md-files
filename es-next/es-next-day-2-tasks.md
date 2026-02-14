---
marp: true
paginate: true
---

# ES Next: Day 2 Tasks

### Exercises & Lab

---

## 🚩 Task 1: Unique Numbers (Set)

Given the following array:
`const numbers = [1, 2, 3, 2, 4, 5, 1, 6, 4, 7, 8, 5];`

1. Convert the list into a **Set** to remove duplicates.
2. Print how many **unique numbers** there are.
3. Check if the number **5** is in the set.
4. **Remove** the number 2 from the set.
5. **Loop** through the set and print each number.

---

## 🚩 Task 2: Countries & Capitals (Map)

1. Create a **Map** of 3 countries and their capitals:
   - "India" → "New Delhi"
   - "France" → "Paris"
   - "Japan" → "Tokyo"

2. Print the capital of **"France"**.
3. Add a new country **"Germany" → "Berlin"**.
4. Check if **"Japan"** exists in the map.
5. **Loop** through the map and print all countries with their capitals.

---

## 🚩 Task 3: Animal Hierarchy (Classes)

1. Create a class `Animal` with:
   - Properties: `name`, `sound`
   - Method `makeSound()` → prints: `Animal <name> makes sound: <sound>`

2. Create a class `Dog` that **inherits** from `Animal`:
   - Add a method `bark()` → prints: `<name> is barking: Woof! Woof!`

3. Create an object `dog1` of class `Dog` with `name = "Buddy"` and `sound = "Woof"`.
4. Call both `makeSound()` and `bark()` on the `dog1` object.

---

## 🚩 Task 4: String Helpers (Modules)

Create two files:

1. **`helpers.js`**:
   - Export a function `toUpperCase(str)` → returns `str.toUpperCase()`
   - Export a function `toLowerCase(str)` → returns `str.toLowerCase()`

2. **`main.js`**:
   - **Import** `toUpperCase` and `toLowerCase` from `./helpers.js`
   - Use them to format the string `"JavaScript is Fun"`
   - Print the results.
