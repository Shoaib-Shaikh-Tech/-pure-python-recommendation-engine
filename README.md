# 📌 pure-python-recommendation-engine  
A lightweight social network recommendation engine that suggests new connections using mutual friend scoring. No ML — just clean Python data structures.

---

## 🚀 Features

- 🔍 Suggests **"People You May Know"** based on mutual friends  
- 👥 Pure Python logic — **no machine learning**  
- 📂 Reads social graph from a JSON dataset  
- ⚡ Fast, simple, beginner-friendly  
- 🧠 Demonstrates Python fundamentals (loops, dictionaries, sets, sorting)
- 🔧 Fully customizable recommendation rules

---

## 📁 Project Structure

```
pure-python-recommendation-engine/
│── cleaned_data.json            # Social network dataset
│── recommender.py               # Friend recommendation logic
│── README.md                    # Documentation
```

---

## 🗂 Example Dataset (cleaned_data.json)

The dataset has two sections:

### ✔️ `users`
Each user has:
- `id`
- `name`
- `friends` → list of user IDs they are connected with  
- `liked_pages` → extra social attributes (not used yet)

### ✔️ `pages`
Contains page IDs & names (for future improvements)

**Small sample from your real dataset:**

```json
{
  "users": [
    {"id": 1, "name": "Amit", "friends": [2, 3, 4, 5, 6], "liked_pages": [101, 102]},
    {"id": 2, "name": "Priya", "friends": [1, 3, 5, 6, 7], "liked_pages": [102, 103]},
    {"id": 3, "name": "Rahul", "friends": [1, 2, 4, 7, 8], "liked_pages": [101, 103]}
    ...
  ],
  "pages": [
    {"id": 101, "name": "Python Developers"},
    {"id": 102, "name": "Data Science Enthusiasts"}
    ...
  ]
}
```

---

## 🧠 How the Algorithm Works

The logic follows early Facebook-style mutual friend scoring:

1. Take the target user  
2. Look at all their **friends**  
3. For each friend, look at their **friends**  
4. Count how many times each candidate appears  
5. Exclude:
   - the user themself  
   - users already in friend list  
6. Sort the remaining users by **highest mutual friend count**


---


## 💡 Author  
**Shoaib** — Data Science & Python Enthusiast  