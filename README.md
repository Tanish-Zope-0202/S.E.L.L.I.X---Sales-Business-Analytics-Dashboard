# S.E.L.L.I.X — Sales & Business Analytics Dashboard

A full-stack sales analytics dashboard that transforms raw CSV sales data into interactive business insights using **Python, Flask, Pandas, SQLite, SQL, JavaScript, and Chart.js**.

S.E.L.L.I.X allows users to upload sales data, automatically process and store it in a relational database, and explore revenue, sales volume, regional performance, product performance, and order-level data through an interactive dashboard.

---

## Overview

Businesses often have large amounts of sales data but need a simple way to turn that data into actionable insights.

S.E.L.L.I.X provides a lightweight analytics platform where users can:

- Upload sales data through CSV files
- Automatically calculate revenue
- Store structured sales records in SQLite
- Analyze key business metrics
- Explore revenue trends over time
- Compare regional performance
- Identify top-performing products
- Filter results dynamically
- Export filtered data as CSV

The project combines **data processing, relational databases, REST APIs, and interactive visualization** into a single full-stack application.

---

## Features

### 📊 Business KPIs

The dashboard provides real-time calculations for:

- Total Revenue
- Units Sold
- Number of Orders
- Average Order Value

### 📈 Interactive Analytics

Visualize sales performance through:

- Revenue over time
- Revenue by region
- Top products by revenue
- Recent order history

Charts are implemented using **Chart.js**.

### 🔎 Dynamic Filtering

Sales data can be filtered by:

- Region
- Product category
- Start date
- End date

Filters are processed through SQL queries on the backend.

### 📂 CSV Data Import

Users can:

- Drag and drop CSV files
- Select CSV files manually
- Load sample data
- Add additional datasets

The application validates required columns before importing the data.

### 📤 CSV Export

Filtered sales records can be exported directly from the dashboard as a CSV report.

### 🗄️ Relational Data Storage

Sales records are stored in a SQLite database and queried using SQL aggregation functions such as:

- `SUM()`
- `AVG()`
- `COUNT()`
- `GROUP BY`
- `ORDER BY`

### 📱 Responsive Dashboard

The frontend is designed to work across desktop and mobile screen sizes.

### ⚡ Offline-Friendly Frontend

The application self-hosts its fonts and Chart.js library rather than relying on external CDNs.

A service worker and PWA manifest are also included.

---

## Tech Stack

| Layer | Technologies |
|---|---|
| Backend | Python, Flask |
| Data Processing | Pandas |
| Database | SQLite |
| Query Language | SQL |
| Frontend | HTML, CSS, JavaScript |
| Visualization | Chart.js |
| API | Flask REST-style JSON endpoints |
| Fonts | Inter, Fraunces |
| Deployment Support | Gunicorn |

---

## Application Architecture

```text
                    ┌──────────────────┐
                    │    CSV Dataset   │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │      Pandas      │
                    │ Data Validation  │
                    │ Revenue Compute  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  Flask Backend   │
                    │   REST APIs      │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ SQLite Database  │
                    │   SQL Queries    │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   JSON API Data  │
                    └────────┬─────────┘
                             │
                             ▼
              ┌─────────────────────────────┐
              │ JavaScript + Chart.js      │
              │ Interactive Dashboard      │
              └─────────────────────────────┘
```

---

## Project Structure

```text
sales-analytics-dashboard/
│
├── app.py
├── database.py
├── requirements.txt
├── README.md
├── .gitignore
│
├── sample_data/
│   └── sample_sales.csv
│
├── static/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   ├── chart.umd.min.js
│   │   └── dashboard.js
│   ├── fonts/
│   ├── icons/
│   ├── manifest.json
│   └── service-worker.js
│
└── templates/
    └── dashboard.html
```

---

## CSV Format

S.E.L.L.I.X expects CSV files containing the following columns:

```csv
order_date,region,category,product,quantity,unit_price
```

Example:

```csv
order_date,region,category,product,quantity,unit_price
2026-01-05,West,Electronics,Laptop,3,55000
2026-01-06,South,Accessories,Keyboard,10,1500
```

Revenue is calculated automatically:

```text
Revenue = Quantity × Unit Price
```

Column names are normalized during upload by converting them to lowercase and replacing spaces with underscores.

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/sales-analytics-dashboard.git
cd sales-analytics-dashboard
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Initialize the database

```bash
python database.py
```

### 5. Start the application

```bash
python app.py
```

### 6. Open the dashboard

Open:

```text
http://127.0.0.1:5000
```

You can either upload your own CSV file or use the built-in sample dataset.

---

## API Endpoints

| Endpoint | Method | Purpose |
|---|---|---|
| `/` | GET | Dashboard interface |
| `/api/upload` | POST | Upload CSV data |
| `/api/load-sample` | POST | Load sample dataset |
| `/api/reset` | POST | Clear current data |
| `/api/filters` | GET | Retrieve available filters |
| `/api/kpis` | GET | Retrieve KPI metrics |
| `/api/revenue-trend` | GET | Revenue trend data |
| `/api/top-products` | GET | Top products by revenue |
| `/api/region-breakdown` | GET | Revenue by region |
| `/api/table` | GET | Recent order data |
| `/api/export` | GET | Export filtered sales data |

---

## Key Technical Highlights

### Data Processing

Pandas is used to:

- Read uploaded CSV files
- Normalize column names
- Validate required fields
- Convert numerical columns
- Handle invalid numerical values
- Calculate revenue
- Prepare records for database insertion

### Database

SQLite is used to persist structured sales data.

The main sales table contains:

```text
id
order_date
region
category
product
quantity
unit_price
revenue
```

### Backend

Flask exposes JSON endpoints for the dashboard.

The backend dynamically builds SQL filters based on:

- Date range
- Region
- Category

This allows the dashboard to request only the data required for each visualization.

### Frontend

Vanilla JavaScript handles:

- File uploads
- Filters
- API communication
- KPI updates
- Chart rendering
- Table rendering
- CSV export
- Dashboard state

Chart.js is used for interactive data visualization.

---

## Example Use Cases

S.E.L.L.I.X can be used to analyze:

- Sales performance
- Regional revenue distribution
- Product performance
- Order volume
- Average order value
- Revenue trends
- Filtered sales reports

---

## Future Improvements

Potential extensions include:

- PostgreSQL support
- User authentication
- Role-based access control
- Automated report generation
- Advanced sales forecasting
- Customer segmentation
- Profit and margin analysis
- Inventory analytics
- Excel export
- PDF reports
- Docker deployment
- Cloud deployment
- Automated tests
- Advanced dashboard drill-downs

---

## Learning Outcomes

This project demonstrates practical experience with:

- Python web development
- Flask
- REST API development
- Pandas data processing
- SQL querying
- Relational databases
- Data visualization
- Frontend JavaScript
- CSV data pipelines
- Full-stack application development
- Business analytics

---

## License

This project is available for educational and portfolio purposes.
