# 🚀 Git Basics Notes

> Beginner Friendly Git Notes with Examples

---

# 📖 What is Git?

Git is a **Version Control System (VCS)**.

Is ka kaam hota hai project ki history maintain karna, changes track karna aur multiple developers ko ek hi project par kaam karne dena.

Example:

```
Project
│
├── index.html
├── style.css
└── app.js
```

Har change Git save karta rehta hai.

---

# 📂 What is a Repository?

Repository (Repo) ek folder hota hai jahan Git project ki history aur configuration store karta hai.

Jab aap command chalate ho:

```bash
git init
```

To Git project ke andar hidden **.git** folder bana deta hai.

```
MyProject/
│
├── .git/
├── index.html
├── app.js
└── style.css
```

Ye **.git** folder hi actual repository hoti hai.

---

# 🔄 Git Workflow

```
Working Directory
        │
        │ git add
        ▼
Staging Area
        │
        │ git commit
        ▼
Local Repository
        │
        │ git push
        ▼
Remote Repository (GitHub)
```

---

# 🖥️ Working Directory

Ye wo files hoti hain jin par aap currently kaam kar rahe hote ho.

Example:

```
app.js
```

Aap ne code likha.

Abhi Git sirf dekhta hai ke file change hui hai.

Abhi commit nahi hui.

---

# 📦 Staging Area

Isay "Waiting Room" bhi kehte hain.

Yahan aap decide karte ho kaunsi files commit hongi.

Command:

```bash
git add app.js
```

Ya

```bash
git add .
```

Ab file staging area mein aa gayi.

---

# 💾 Local Repository

Jab aap commit kar dete ho.

```bash
git commit -m "Added Login Feature"
```

Ab Git permanently us snapshot ko save kar leta hai.

---

# 🌍 Remote Repository

Ye GitHub hota hai.

Local commits upload karne ke liye:

```bash
git push
```

---

# 🎯 Complete Git Flow

```
Create File
     │
     ▼
git status
     │
     ▼
git add .
     │
     ▼
git commit
     │
     ▼
git push
```

---

# 📌 git status

Sabse important command.

Batati hai project ki current condition.

Command:

```bash
git status
```

Example:

```
On branch main

Changes not staged for commit:

modified: app.js
```

Meaning:

✅ app.js change hui hai

❌ Abhi stage nahi hui.

---

Example 2

```
Changes to be committed:

new file: login.js
```

Meaning:

✅ File stage ho chuki hai.

---

# 📌 git add

Changes ko staging area mein bhejta hai.

Single file:

```bash
git add app.js
```

Multiple files:

```bash
git add app.js style.css
```

Sab files:

```bash
git add .
```

Current folder:

```bash
git add *
```

---

# 📌 git commit

Snapshot save karta hai.

Command:

```bash
git commit -m "Created Login Page"
```

Example:

```
[main abc123]

Created Login Page
```

Ab history save ho gayi.

---

# 📌 git branch

Project ki sari branches dikhata hai.

Command:

```bash
git branch
```

Output:

```
* main
development
feature/login
```

⭐ Star (*) current branch batata hai.

---

# 🌳 Branch kya hoti hai?

Suppose project live chal raha hai.

Aap naya feature banana chahte ho.

Instead of directly changing main:

```
main
```

Aap branch bana lete ho.

```
main
 │
 └──────── feature/login
```

Ab safely feature bana sakte ho.

---

# 📌 git checkout

Branch switch karne ke liye.

Command:

```bash
git checkout development
```

Ab current branch:

```
development
```

---

Purani Git versions mein branch create bhi hoti thi.

```bash
git checkout -b feature/login
```

Ye:

✔ branch create karegi

✔ usi par switch bhi karegi

---

# 📌 git switch

Modern command.

Sirf branch switching ke liye.

Command:

```bash
git switch development
```

---

# 📌 git switch -c

New branch create + switch.

Command:

```bash
git switch -c feature/login
```

Equivalent to:

```bash
git checkout -b feature/login
```

Example:

```
main

↓

git switch -c payment

↓

payment
```

---

# 📊 Difference

## git checkout

Older command

✔ Switch branch

✔ Restore file

✔ Create branch

---

## git switch

New command

✔ Only branch switching

✔ Easier

✔ Recommended

---

# 📌 Practical Example

Suppose project:

```
Student-System
```

Check status:

```bash
git status
```

Output:

```
modified: Student.java
```

Stage:

```bash
git add Student.java
```

Commit:

```bash
git commit -m "Added Fee Calculation"
```

Check branches:

```bash
git branch
```

Output:

```
* main
```

Create new branch:

```bash
git switch -c payment
```

Output:

```
Switched to a new branch 'payment'
```

Check again:

```bash
git branch
```

Output:

```
main

* payment
```

Go back:

```bash
git switch main
```

---

# 🎯 Most Used Commands

| Command | Purpose |
|----------|----------|
| `git status` | Show current changes |
| `git add .` | Stage all files |
| `git add filename` | Stage specific file |
| `git commit -m "message"` | Save snapshot |
| `git branch` | List branches |
| `git switch branch` | Switch branch |
| `git switch -c new-branch` | Create & switch |
| `git checkout branch` | Old way to switch |
| `git checkout -b branch` | Old way to create & switch |

---

# 🧠 Easy Way to Remember

```
Coding
   │
   ▼
git status
   │
   ▼
git add
   │
   ▼
git commit
   │
   ▼
git push
```

---

# 💡 Pro Tips

✅ Always run:

```bash
git status
```

before committing.

---

✅ Write meaningful commit messages.

❌ Bad

```bash
git commit -m "update"
```

✅ Good

```bash
git commit -m "Added Student Fee Module"
```

---

✅ Use `git switch` instead of `git checkout` for switching branches.

---

✅ Commit small changes frequently instead of one huge commit.

---

# 🎉 Congratulations!

Ab aap Git ke basic workflow ko samajh gaye ho:

✅ Repository

✅ Working Directory

✅ Staging Area

✅ Local Repository

✅ git status

✅ git add

✅ git commit

✅ git branch

✅ git checkout

✅ git switch

✅ git switch -c

Happy Coding! 🚀
