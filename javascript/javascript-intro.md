---
marp: true
paginate: true
theme: uncover
---

# Introduction to JavaScript

### Badr Aldien Soliman

---

## Before We Start: A Quick Question

You use websites and apps every day.

Have you ever wondered...

- How does a button _do something_ when you click it?
- How does Google show suggestions _as you type_?
- How does a form tell you _"password is too short"_ instantly?

---

### The answer to all of those is the same:

## JavaScript.

---

## The Three Languages of the Web

Think of building a house:

| Layer        | Technology     | Role                                       |
| ------------ | -------------- | ------------------------------------------ |
| 🧱 Structure | **HTML**       | The walls, floors, and rooms               |
| 🎨 Style     | **CSS**        | The paint, furniture, and decoration       |
| ⚡ Behavior  | **JavaScript** | The electricity: lights, doors, appliances |

---

### HTML alone gives you this:

A page with content (text, images, buttons) but **nothing responds** when you interact with it.

### Add CSS and you get:

A page that looks good (colors, fonts, layout).

### Add JavaScript and now:

The page **comes alive**: it reacts, updates, communicates, and responds to the user in real time.

---

## What Exactly is JavaScript?

JavaScript is a **programming language** that runs inside your browser.

When you open a webpage, your browser downloads three things:

```
index.html   →   "Here's the content"
style.css    →   "Here's how it looks"
script.js    →   "Here's how it behaves"
```

Your browser reads the JavaScript file and **executes it**, with no installation needed.

---

## Where Does JavaScript Run?

### 1. In the Browser (Frontend)

Every modern browser has a built-in JavaScript engine:

| Browser       | Engine         |
| ------------- | -------------- |
| Chrome / Edge | V8             |
| Firefox       | SpiderMonkey   |
| Safari        | JavaScriptCore |

---

## A Brief History of JavaScript

---

### 1991: The Web is Born

Tim Berners-Lee creates the World Wide Web.

Pages are pure HTML: text and links, nothing more. No interactivity at all.

---

### 1995: JavaScript is Created

**Brendan Eich** at Netscape writes the first version of JavaScript in just **10 days**.

It was called _Mocha_, then _LiveScript_, then finally **JavaScript**.

> ⚠️ Despite the name, JavaScript has **nothing to do with Java**. The name was a marketing decision to ride Java's popularity at the time.

---

### 1996–2000s: The Browser Wars

Microsoft and Netscape both built their own versions of JavaScript, causing inconsistencies across browsers.

Developers had to write different code for different browsers: a painful era.

---

### 2008: The Speed Revolution

Google releases **Chrome** with the V8 engine, making JavaScript dramatically faster.

This changed everything: suddenly JavaScript was fast enough for real applications.

---

### 2009: JavaScript Leaves the Browser

**Ryan Dahl** creates **Node.js**, allowing JavaScript to run on servers.

JavaScript was no longer just a "browser toy"; it became a serious, full-stack language.

---

### 2010s–Today: JavaScript Everywhere

JavaScript is now the **most widely used programming language in the world**.

- Web apps (Gmail, Twitter, Notion)
- Mobile apps (React Native)
- Desktop apps (VS Code is built with JS)
- Servers and APIs (Node.js: what this course focuses on)
- Even IoT devices and robotics

---

## Why Learn JavaScript?

### It's Everywhere

One language that works across the entire stack: browser, server, mobile, desktop.

### It's Beginner-Friendly

You can write JavaScript and see results instantly in the browser: no compilation, no complex setup.

---

### It's In-Demand

JavaScript consistently ranks as one of the most sought-after skills in the job market.

### You're Already Using It

Every time you use a modern website, JavaScript is running. Now you'll understand what's happening under the hood.

---

# Let's get started.
