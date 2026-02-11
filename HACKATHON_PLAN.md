# ⚽ Sports Booking App - SIMPLE Hackathon Plan

**DON'T PANIC.** This is much simpler than it looks. We're building just a few pages.

---

## 🎯 What We're Building (Super Simple)

A website where you can:
1. Create an account & login
2. See available time slots for basketball court
3. Click to book a time slot
4. See your bookings

**That's it!** Everything else is extra.

---

## 🛠️ Setup (Do This First - 30 minutes)

### Step 1: Create folders
```
sports-app/
├── app.py                 (the whole app is here)
├── app.db                 (auto-created database)
├── index.html             (home page)
├── login.html             (login page)
├── book.html              (booking page)
└── my_books.html          (see your bookings)
```

### Step 2: Install Python libraries
Run this in PowerShell:
```powershell
pip install flask
```

That's it! Flask is all you need.

---

## 📅 Your 20 Hours (Realistic Timeline)

| Time | What You Do | How Long |
|------|------------|----------|
| **Hour 1** | Build database + create `app.py` | 1 hour |
| **Hour 2-3** | Build login page (HTML) | 2 hours |
| **Hour 4-5** | Build booking page (HTML) | 2 hours |
| **Hour 6-8** | Add login/booking code to `app.py` | 3 hours |
| **Hour 9** | Make it look nice (CSS) | 1 hour |
| **Hour 10-15** | Test everything, fix bugs | 6 hours |
| **Hour 16-20** | Record 5-min video | 4-5 hours |

**TOTAL: 20 hours** ✅

---

## 🚀 Let's Build It

### Step 1: Create `app.py` (The Main File)

This ONE file does everything. Here's the basic structure:

```python
from flask import Flask, render_template, request, redirect
import sqlite3
import os

app = Flask(__name__)

# Create database if it doesn't exist
if not os.path.exists('app.db'):
    conn = sqlite3.connect('app.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE users (id INTEGER PRIMARY KEY, username TEXT, password TEXT)''')
    c.execute('''CREATE TABLE bookings (id INTEGER PRIMARY KEY, username TEXT, time_slot TEXT)''')
    c.execute('''CREATE TABLE slots (id INTEGER PRIMARY KEY, time TEXT, is_booked INTEGER)''')
    conn.commit()
    conn.close()

# HOME PAGE - Show available slots
@app.route('/')
def home():
    return render_template('index.html')

# LOGIN PAGE
@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        # Check password
        # If correct, save user in session
        pass
    return render_template('login.html')

# BOOKING PAGE - Book a slot
@app.route('/book', methods=['GET', 'POST'])
def book():
    if request.method == 'POST':
        # Save booking to database
        pass
    return render_template('book.html')

# MY BOOKINGS - See your bookings
@app.route('/my-bookings')
def my_bookings():
    return render_template('my_books.html')

if __name__ == '__main__':
    app.run(debug=True)
```

### Step 2: Create `index.html` (Home Page)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Sports Booking</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        a { display: block; margin: 10px 0; padding: 10px; background: blue; color: white; text-decoration: none; }
    </style>
</head>
<body>
    <h1>⚽ Sports Facilities Booking</h1>
    <p>Welcome! Choose what you want to do:</p>
    <a href="/login">Login / Signup</a>
    <a href="/book">Book a Time Slot</a>
    <a href="/my-bookings">See My Bookings</a>
</body>
</html>
```

### Step 3: Create `login.html` (Login Page)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        input { padding: 10px; margin: 5px; width: 200px; }
        button { padding: 10px 20px; background: blue; color: white; }
    </style>
</head>
<body>
    <h1>Login or Sign Up</h1>
    <form method="POST">
        <input type="text" name="username" placeholder="Username">
        <input type="password" name="password" placeholder="Password">
        <button type="submit">Login</button>
    </form>
    <a href="/">Back Home</a>
</body>
</html>
```

### Step 4: Create `book.html` (Booking Page)

```html
<!DOCTYPE html>
<html>
<head>
    <title>Book a Slot</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        .slot { padding: 10px; margin: 5px; border: 1px solid gray; cursor: pointer; }
        .slot:hover { background: lightblue; }
        button { padding: 10px 20px; background: green; color: white; }
    </style>
</head>
<body>
    <h1>Available Time Slots - Basketball Court</h1>
    
    <form method="POST">
        <h3>Monday:</h3>
        <input type="radio" name="slot" value="mon_3pm"> 3:00 PM - 4:00 PM <br>
        <input type="radio" name="slot" value="mon_4pm"> 4:00 PM - 5:00 PM <br>
        <input type="radio" name="slot" value="mon_5pm"> 5:00 PM - 6:00 PM <br>
        
        <h3>Tuesday:</h3>
        <input type="radio" name="slot" value="tue_3pm"> 3:00 PM - 4:00 PM <br>
        <input type="radio" name="slot" value="tue_4pm"> 4:00 PM - 5:00 PM <br>
        
        <h3>Wednesday:</h3>
        <input type="radio" name="slot" value="wed_3pm"> 3:00 PM - 4:00 PM <br>
        
        <button type="submit">Book This Slot</button>
    </form>
    
    <a href="/">Back Home</a>
</body>
</html>
```

### Step 5: Create `my_books.html` (Your Bookings)

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Bookings</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid black; padding: 10px; text-align: left; }
        th { background: lightgray; }
    </style>
</head>
<body>
    <h1>Your Bookings</h1>
    
    <table>
        <tr>
            <th>Time Slot</th>
            <th>Status</th>
            <th>Action</th>
        </tr>
        <tr>
            <td>Monday 3:00 PM</td>
            <td>✅ Confirmed</td>
            <td><button>Cancel</button></td>
        </tr>
        <tr>
            <td>Wednesday 4:00 PM</td>
            <td>✅ Confirmed</td>
            <td><button>Cancel</button></td>
        </tr>
    </table>
    
    <a href="/">Back Home</a>
</body>
</html>
```

---

## ✅ What This App Does

1. **Home Page** - Links to everything
2. **Login Page** - Users can create account or login
3. **Book Page** - Shows available times, user picks one
4. **My Bookings** - Shows what user booked

---

## 💻 How to Run It

1. Save all files above (app.py + 4 HTML files) in your `sports-app` folder
2. Open PowerShell in that folder
3. Type: `python app.py`
4. Go to: `http://127.0.0.1:5000`
5. Click around!

---

## 🎯 If You Want to Add More (Optional)

**Find Players Page** - Just add another HTML file (`find-players.html`)
**Notifications** - Use database to track who's looking for players
**Real Time** - Add refresh button to see updates

**But you don't NEED these to win!**

---

## 📹 Your 5-Minute Video

**Just show:**
1. **Open the app** → Show home page (10 sec)
2. **Login** → Create account (15 sec)
3. **Book a slot** → Click Monday 3pm, book it (30 sec)
4. **Show my bookings** → "Here's my booking!" (20 sec)
5. **Explain the idea** → "Students can now easily book courts" (1 min)
6. **Show code** → "Built with Python Flask" (30 sec)

**Use:** OBS Studio (free screen recorder) or just record your screen with Windows

---

## 🎯 FOCUS ON THIS FIRST

✅ Make the app work (even if ugly)  
✅ Then make it pretty  
✅ Then record video

**DON'T spend 10 hours making it perfect. Spend 8 hours making it work, 1 hour making it look good, 1 hour recording.**

---

## 📝 Next Step

Tell me which file you want help with first, and I'll help you build it with step-by-step code.

**Ready? Let's go!** 🚀
