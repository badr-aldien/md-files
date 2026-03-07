# Node.js — Day 1 Task

**Topics:** Global Object · Modules · File System

---

## The Scenario

You're building a **personal activity logger**. Each time the script runs, it records an entry into a log file — using globals, modules, and the `fs` module.

---

## Project Structure

```
activity-logger/
├── app.js
├── logger.js
└── logs/
    └── activity.txt   ← auto-created if it doesn't exist
```

---

## Part 1 — Globals (`app.js`)

At the top of `app.js`, print the following to the console **without hardcoding any paths**:

```
Current file:      /Users/.../app.js
Current directory: /Users/.../activity-logger
```

---

## Part 2 — Modules (`logger.js`)

Create `logger.js` that exports **two things**:

- `appName` — a string with your app's name (e.g. `"Activity Logger"`)
- `log(message)` — a function that prints: `[AppName] message`

Then in `app.js`, import and use both.

```
// Expected output:
// [Activity Logger] App is starting...
```

---

## Part 3 — File System (`app.js`)

Using the `fs` module, do all of the following **in order**:

1. **Create** the `./logs/` folder if it doesn't already exist
2. **Write** a first entry to `activity.txt`: `App started.`
3. **Append** a second line without overwriting: `User logged in.`
   > 🔍 Look up `fs.appendFile`
4. **Read** the final file and print its contents to the console
5. After **3 seconds**, delete `activity.txt` using a timer

---

## Part 4 — Timers

After the file is read (step 4), use `setInterval` to print a countdown every second, then clear the interval and delete the file:

```
Deleting file in 3...
Deleting file in 2...
Deleting file in 1...
activity.txt deleted.
```

---

## Expected Final Console Output

```
Current file:      /Users/.../app.js
Current directory: /Users/.../activity-logger
[Activity Logger] App is starting...
--- File Contents ---
App started.
User logged in.
Deleting file in 3...
Deleting file in 2...
Deleting file in 1...
activity.txt deleted.
```
