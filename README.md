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

## 🧩 Core Python Code (recommender.py)

```python
import json
 
def load_data(filename):
    with open(filename, "r") as file:
        return json.load(file)
 
def find_people_you_may_know(user_id, data):
    user_friends = {}
    for user in data["users"]:
        user_friends[user["id"]] = set(user["friends"])
    
    if user_id not in user_friends:
        return []
    
    direct_friends = user_friends[user_id]
    suggestions = {}
    
    for friend in direct_friends:
        # For all friends of friend
        for mutual in user_friends[friend]:
            # If mutual id is not the same user and not already a direct friend of user
            if mutual != user_id and mutual not in direct_friends:
                # Count mutual friends
                suggestions[mutual] = suggestions.get(mutual, 0) + 1
    
    sorted_suggestions = sorted(suggestions.items(), key=lambda x: x[1], reverse=True)
    return [user_id for user_id, _ in sorted_suggestions]
 
# Load data
data = load_data("cleaned_data.json")
user_id = 1  # Example: Finding suggestions for Amit
recommendations = find_people_you_may_know(user_id, data)
print(f"People You May Know for User {user_id}: {recommendations}")
```

---

## ▶️ How to Run

### 1. Clone the repository
```bash
git clone https://github.com/your-username/pure-python-recommendation-engine.git
cd pure-python-recommendation-engine
```

### 2. Run the script
```bash
python recommender.py
```

---

## 🧪 Example Output

```
People You May Know for User 1: [7, 8, 9, 10, ...]
```

The list is sorted by **mutual friend score (highest first)**.

---

## 🌱 Future Improvements

- ⭐ Integrate page likes into scoring  
- ⭐ Use weights (direct connection vs. page similarity)  
- ⭐ Build a FastAPI/Flask backend  
- ⭐ Add Streamlit UI for visualization  
- ⭐ Convert dataset into a graph using NetworkX  
- ⭐ Add tests & benchmarks  

---


## 💡 Author  
**Shoaib** — Data Science & Python Enthusiast  