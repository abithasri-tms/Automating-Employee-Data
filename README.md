# Automating Employee Data

A browser-based system that streamlines employee record management by
eliminating manual data entry and repetitive administrative tasks.
Upload your Excel file and the dashboard automatically validates,
organizes, and reports on your employee data instantly.

No server. No installation. Just open the HTML file in any browser.

---

## How to Run

1. Download `dashboard.html`
2. Open it in any browser (Chrome, Firefox, Edge)
3. Click **Upload File** and select your employee Excel or CSV file
4. Everything loads instantly

---

## Input Format

Your file must have these 5 columns:

| Column | Description |
|---|---|
| `name` | Employee full name |
| `email` | Employee email address |
| `department` | Department (IT, HR, Finance...) |
| `manager` | Manager name |
| `manager_email` | Manager email address |

---

## Features

**Overview** — Summary cards, bar charts, doughnut chart, data health score

**Employees** — Searchable table, filter by department and manager, export CSV

**Managers** — Team size, member list, departments managed per manager

**Departments** — Headcount, manager details, employee list per department

**Auto Cleanse** — Detects missing fields, invalid emails, duplicates — auto-fixes with before/after diff view, download clean Excel

**Email Drafts** — Auto-generated welcome emails per employee, one-click copy

---

## Built With

- HTML5, CSS3, JavaScript
- SheetJS — Excel/CSV parsing in browser
- Chart.js — Charts and visualization
- Google Fonts — Outfit + Space Mono


