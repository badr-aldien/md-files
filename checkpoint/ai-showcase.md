---
marp: true
theme: default
paginate: true
theme: gaia
---

<!-- _class: cover -->

# 🤖 AI in the Dev Workflow

**Badr Aldien Soliman**

---

# The Problem

Writing unit tests is the most **boring** part of being a developer.

- You write the code
- You manually think of edge cases
- You write the tests
- You forget to update them when code changes

> _"Nobody enjoys writing tests. Everybody enjoys having them."_

---

# The Idea

What if your editor **watched your code** and wrote the tests for you?

- ✅ You write the function
- ✅ You save the file
- ✅ AI reads your code
- ✅ Tests appear automatically
- ✅ If tests pass → **auto git commit**

---

# Meet: Watchpoint

A custom Node.js CLI tool built for this exact problem.

```
src/index.js  ← you write code here
     ↓  file change detected
  OpenAI API  ← reads your code
     ↓  generates tests
index.test.js ← tests written automatically
     ↓  jest runs
  SAVEPOINT ✅ ← git commit if all pass
```

---

# Why This Matters

| Without AI          | With Watchpoint         |
| ------------------- | ----------------------- |
| Write code manually | Write code              |
| Think of test cases | Save file               |
| Write tests         | AI handles it           |
| Run tests           | Tests run automatically |
| Commit manually     | Auto-committed on pass  |

---

# What's Next

- Watch **any** file, not just `index.js`
- Support multiple file types (`.ts`, `.py`)
- VS Code extension version
- **Clean mode**: `watchpoint --clean` removes all SAVEPOINT commits

---

<!-- _class: cover -->

# Thank You

## **[badrsoliman.com](https://www.badrsoliman.com)**
