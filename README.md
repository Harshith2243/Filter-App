# 🛍️ Product Filter Store

> A real-time search, filter, and sort e-commerce app — built with pure HTML, CSS, and JavaScript. No frameworks. No installs. Just open and run.

---

## 📸 What It Looks Like

When you open the app you will see:
- A **grid of 20 products** loaded live from the internet (Fake Store API)
- A **search bar**, **category dropdown**, **sort dropdown**, and a **price range slider** at the top
- A **🛒 Cart button** in the top right corner
- A **🌙 Dark mode toggle** button

---

## 🚀 How to Run It

**No installation needed.**

1. Download or clone this project
2. Double-click `index.html`
3. It opens in your browser — done ✅

> Make sure you have an internet connection — products are fetched live from the API

---

## 🔍 How The Filter Works — Step by Step

This is the most important part to understand. Here is exactly what happens when a user interacts with the app:

### 1️⃣ Page Loads → Fetch Products from API

```
Browser opens → JavaScript runs fetch() → API returns 20 products as JSON → Products shown on screen
```

While loading, you see **shimmer/skeleton cards** (grey animated placeholders) instead of a blank screen.

---

### 2️⃣ User Types in Search Box → Live Filter by Name

```
User types "shirt" → JavaScript filters the 20 products → Only products with "shirt" in their name are shown
```

**How the code does it:**
```js
products.filter(p => p.title.toLowerCase().includes(query))
```

⚡ **Debounced** — meaning it waits 300ms after you stop typing before filtering. This avoids re-running the filter on every single keystroke.

---

### 3️⃣ User Picks a Category → Filter by Category

```
User selects "electronics" → Only electronics products remain visible
```

**How the code does it:**
```js
products.filter(p => p.category === selectedCategory)
```

Categories are **automatically populated** from the API — no hardcoding needed.

---

### 4️⃣ User Drags Price Slider → Filter by Max Price

```
User drags slider to $50 → Only products that cost $50 or less are shown
```

**How the code does it:**
```js
products.filter(p => p.price <= maxPrice)
```

---

### 5️⃣ All Filters Work Together (AND Logic)

If the user uses search + category + price at the same time:

```
"jacket" + "men's clothing" + max $60
→ Shows only men's clothing jackets under $60
```

**How the code does it — all three filters in one line:**
```js
products.filter(p =>
  p.title.toLowerCase().includes(query) &&   // search
  p.category === category &&                  // category
  p.price <= maxPrice                         // price
)
```

---

### 6️⃣ User Picks a Sort Option → Sort the Results

After filtering, the results are sorted:

| Option | What It Does |
|---|---|
| Default | Original order from API |
| Price (Low–High) | Cheapest product first |
| Price (High–Low) | Most expensive first |
| Rating (High–Low) | Highest rated first |

**How the code does it:**
```js
results.sort((a, b) => a.price - b.price)  // price low to high
results.sort((a, b) => b.rating.rate - a.rating.rate)  // rating high to low
```

---

### 7️⃣ User Clicks "Add to Cart" → Cart Updates Instantly

```
User clicks "Add to Cart" on a product → Product added to cart array in memory
→ Cart count badge updates → Slide-out drawer shows item + running total
```

**How the code does it:**
```js
cart.push(product)        // add to array
renderCart()              // re-render the drawer
```

> ⚠️ The cart is **in-memory only** — it resets when you refresh. No backend or database is needed for this project.

---

### 8️⃣ 0 Results → Friendly Empty State

```
User searches "xyzabc" → No products match → "No products match your filters" message shown
```

No blank screen. No broken layout. Always show the user what happened.

---

## 🧠 Core JavaScript Concepts Used

| Concept | Where It's Used |
|---|---|
| `fetch()` + `async/await` | Pulling products from the API |
| `Array.filter()` | Filtering products by search, category, price |
| `Array.sort()` | Sorting results by price or rating |
| `Array.map()` | (Used internally to build category list) |
| DOM Manipulation | Rendering cards, updating cart, showing/hiding states |
| Debounce | Preventing filter from firing on every keystroke |
| Event Listeners | Reacting to search input, dropdown changes, slider, button clicks |

---

## 📁 Project Structure

```
ecommerce-filter-app/
│
├── index.html        ← Everything: HTML + CSS + JavaScript in one file
└── README.md         ← This file
```

---

## 🌐 Deploy to Vercel (Free)

1. Push this folder to a **GitHub repo**
2. Go to [vercel.com](https://vercel.com) and sign in with GitHub
3. Click **"Add New Project"** → Import your repo
4. Click **Deploy** → Your app is live in under 60 seconds 🚀

Your live URL will look like: `https://your-project-name.vercel.app`

---

## 💡 Why This Project Matters

This search + filter + sort pattern is used in almost every real web app:

| Real App | What It Uses |
|---|---|
| Amazon | Filter by category, price, rating |
| Zomato / Swiggy | Filter by cuisine, price, distance |
| Naukri / LinkedIn | Filter by role, location, salary |
| Flipkart | Sort by popularity, price, discount |

Building this teaches you the **exact same logic** used in all of them.

---

## 👤 Built By

Made as part of the **Full Stack Web Dev 30-Day Learning Guide** by Hirewise Solutions.
