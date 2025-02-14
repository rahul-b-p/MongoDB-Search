### **Case-Sensitive and Case-Insensitive Search using `$regex` in MongoDB**

#### **1. Case-Sensitive Search (Default)**
By default, `$regex` in MongoDB **is case-sensitive**. This means:
```js
db.users.find({ name: { $regex: "Alice" } });
```
- This **matches** `"Alice"`
- But **does NOT match** `"alice"` or `"ALICE"`

---

#### **2. Case-Insensitive Search using `$options: "i"`**
To make the search **case-insensitive**, use the `"i"` option:
```js
db.users.find({ name: { $regex: "alice", $options: "i" } });
```
This **matches** `"Alice"`, `"ALICE"`, `"alice"`, etc.

---

## **Other `$regex` Options**
### **1. Match Start of a String (`^`)**
Find users whose name starts with `"Al"`:
```js
db.users.find({ name: { $regex: "^Al" } });
```
- Matches: `"Alice"`, `"Alan"`
- **Does NOT match** `"Charlie Alice"`

For **case-insensitive** match:
```js
db.users.find({ name: { $regex: "^al", $options: "i" } });
```

---

### **2. Match End of a String (`$`)**
Find names ending with `"son"`:
```js
db.users.find({ name: { $regex: "son$" } });
```
- Matches: `"Johnson"`, `"Anderson"`
- **Does NOT match** `"Sonia"`

---

### **3. Match Any Character (`.`)**
Find names with any single character between `"A"` and `"ce"`:
```js
db.users.find({ name: { $regex: "A.ce" } });
```
- Matches: `"Alice"`, `"Aace"`
- **Does NOT match** `"Ace"`

---

### **4. Match One of Multiple Characters (`[]`)**
Find names containing `"a"`, `"e"`, or `"i"`:
```js
db.users.find({ name: { $regex: "[aei]" } });
```
- Matches: `"Alice"`, `"Eve"`, `"Ian"`

---

### **5. Match a Range of Characters (`[a-z]`)**
Find names containing **any lowercase letter from "a" to "f"**:
```js
db.users.find({ name: { $regex: "[a-f]" } });
```
- Matches: `"Alice"`, `"Bob"`
- **Does NOT match** `"Xavier"`

---

### **6. Match Repeated Characters (`*`, `+`, `?`)**
- `*` (zero or more times)
- `+` (one or more times)
- `?` (zero or one time)

#### **Example: Match `"Ali"` followed by any number of `"c"`**
```js
db.users.find({ name: { $regex: "Alic*" } });
```
- Matches: `"Ali"`, `"Alice"`, `"Aliccc"`

---

### **7. Match Exact Word using `\b`**
Find exact word `"Alice"`:
```js
db.users.find({ name: { $regex: "\\bAlice\\b" } });
```
- Matches **only `"Alice"`**
- **Does NOT match** `"Alicewonder"`

---

### **Example: Combining Multiple Options**
Case-insensitive search for names starting with `"Jo"`:
```js
db.users.find({ name: { $regex: "^Jo", $options: "i" } });
```
Matches: `"John"`, `"joel"`, `"JOHNSON"`

---

## **Conclusion**
🔹 Use `$regex` for flexible pattern matching.  
🔹 `"i"` option makes it **case-insensitive**.  
🔹 Combine with `^`, `$`, `*`, `+` for powerful queries.  

🚀 Let me know if you need more examples!

