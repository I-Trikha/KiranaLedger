# 🏪 Kirana Ledger

> A browser-based digital credit ledger for local grocery stores (Kirana Shops) built with SQLite running entirely in the browser.

Kirana Ledger digitizes the traditional *Udhaari* (credit) notebook used by small retailers. It allows shopkeepers to manage customers, record credit and payments, monitor overdue balances, and even execute custom SQL queries on their data—all without requiring a backend server.

The application is powered by **sql.js**, enabling a fully client-side relational database experience.

---

## Features

### 👥 Customer Management

- Add new customers
- Store phone numbers and addresses
- Search customers instantly
- Customer profile with transaction history

### 💰 Credit Ledger

- Record credit purchases
- Record customer payments
- Automatic balance calculation
- Running account statement

### ⏰ Overdue Tracking

- Due date support
- Overdue payment alerts
- Days overdue calculation
- Top debtors dashboard

### 📊 Business Analytics

- Total outstanding credit
- Number of customers on credit
- Monthly recovery amount
- Customer-wise balances

### 🗄 Interactive SQL Console

Run SQL queries directly on the application database.

Example queries include:

- Customer balances
- Outstanding customers
- Recent transactions
- Overdue payments
- Custom analytics

---

## Screenshots

| Dashboard | Customer Profile | SQL Console |
|------------|------------------|-------------|
| *(Add Screenshot)* | *(Add Screenshot)* | *(Add Screenshot)* |

---

## Architecture

```

              User Interface
                     │
                     ▼
        Customer & Transaction Forms
                     │
                     ▼
              SQLite Database
               (sql.js WASM)
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
 Customer List  Reports      SQL Console
        │
        ▼
 Dashboard & Analytics

```

---

## Database Schema

### Customers

| Field | Type |
|--------|------|
| id | INTEGER |
| name | TEXT |
| phone | TEXT |
| address | TEXT |
| created_at | TIMESTAMP |

### Transactions

| Field | Type |
|--------|------|
| id | INTEGER |
| customer_id | INTEGER |
| type | credit / payment |
| amount | REAL |
| description | TEXT |
| date | DATE |
| due_date | DATE |

---

## Key Functionalities

### Customer Management

- Add customers
- Search customers
- View transaction history
- Outstanding balance tracking

### Transaction Management

Supports

- Credit Entries
- Payment Entries

Balances are automatically calculated using SQL aggregation.

### Overdue Alerts

Automatically detects:

- Outstanding balances
- Earliest due dates
- Days overdue

### SQL Playground

Execute custom SQL queries directly inside the application.

Useful for learning:

- SQL
- Joins
- Aggregations
- Group By
- HAVING
- Analytics queries

---

## Technologies Used

- HTML5
- CSS3
- Vanilla JavaScript
- SQLite (sql.js)
- WebAssembly
- Tabler Icons

---

## Project Structure

```

Kirana-Ledger/
│
├── index.html
├── README.md
├── LICENSE
├── .gitignore
│
├── screenshots/
│   ├── dashboard.png
│   ├── customer.png
│   ├── overdue.png
│   └── sql-console.png
│
├── docs/
│   ├── schema.png
│   └── sample-queries.md
│
└── assets/
    └── logo.svg

```

---

## Running the Project

Clone the repository

```bash
git clone https://github.com/<username>/kirana-ledger.git
```

Open

```
index.html
```

in your browser.

No installation is required.

---

## Example SQL Queries

### Outstanding Balances

```sql
SELECT c.name,
SUM(
CASE
WHEN t.type='credit' THEN t.amount
ELSE -t.amount
END
) AS balance
FROM customers c
LEFT JOIN transactions t
ON c.id=t.customer_id
GROUP BY c.id;
```

### Top Debtors

```sql
SELECT c.name,
SUM(CASE WHEN type='credit'
THEN amount ELSE -amount END)
AS balance
FROM customers c
JOIN transactions t
ON c.id=t.customer_id
GROUP BY c.id
ORDER BY balance DESC;
```

---

## Future Improvements

- Export ledger to PDF
- WhatsApp payment reminders
- SMS notifications
- CSV import/export
- Offline PWA support
- Barcode billing
- Multi-store support
- User authentication
- Cloud synchronization
- Inventory management
- Sales analytics dashboard
- GST invoice generation

---

## Learning Outcomes

This project demonstrates:

- Relational database design
- SQL query optimization
- Client-side SQLite using WebAssembly
- CRUD application architecture
- Interactive data visualization
- Business software development

---

## Author

**Ishan Trikha**

B.Tech Mechanical Engineering

Indian Institute of Technology Kanpur

---

## License

MIT License
