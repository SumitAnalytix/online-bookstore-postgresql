# Online Bookstore — PostgreSQL Sales Analysis

A relational database and SQL analytics project built in **PostgreSQL** to manage and analyze an online bookstore's inventory, customer base, and order transactions.

## Project Structure

```text
online-bookstore-postgresql/
├── data/
│   ├── Books.csv
│   ├── Customers.csv
│   └── Orders.csv
├── sql/
│   └── Ecommerce_sales_project.sql
├── .gitignore
└── README.md
```

## Dataset Overview

The dataset consists of three related CSV tables (500 records each):

| File | Table | Key Columns | Description |
| :--- | :--- | :--- | :--- |
| `data/Books.csv` | `Books` | `Book_ID`, `Title`, `Author`, `Genre`, `Published_Year`, `Price`, `Stock` | Book catalog across genres (Fiction, Non-Fiction, Fantasy, Mystery, Romance, Biography, Science Fiction) |
| `data/Customers.csv` | `Customers` | `Customer_ID`, `Name`, `Email`, `Phone`, `City`, `Country` | Customer contact and geographic details |
| `data/Orders.csv` | `Orders` | `Order_ID`, `Customer_ID`, `Book_ID`, `Order_Date`, `Quantity`, `Total_Amount` | Order transactions linking customers and books |

## Database Schema

- **`Books`**: Primary key `Book_ID` (`SERIAL`).
- **`Customers`**: Primary key `Customer_ID` (`SERIAL`).
- **`Orders`**: Primary key `Order_ID` (`SERIAL`), with foreign keys referencing `Customers(Customer_ID)` and `Books(Book_ID)`.

## How to Run Locally

### Prerequisites
- [PostgreSQL](https://www.postgresql.org/download/) installed (`psql` CLI or pgAdmin)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/online-bookstore-postgresql.git
   cd online-bookstore-postgresql
   ```

2. **Run the SQL script using `psql`**
   From the project root directory, connect to PostgreSQL and execute the script:
   ```bash
   psql -U postgres -f sql/Ecommerce_sales_project.sql
   ```
   *(If using pgAdmin, create the `OnlineBookstore` database, run the `CREATE TABLE` statements, and update the `COPY` file paths or use pgAdmin's Import/Export tool to load the CSVs from `data/`.)*

## Analysis Queries Included

The script `sql/Ecommerce_sales_project.sql` covers **20 business questions** split into two levels:

- **Basic Queries (11)**: Filtering by genre, publication year, country, and date range; calculating total stock and total revenue; finding the most expensive and lowest-stock books; identifying multi-quantity orders and orders over $20.
- **Advanced Queries (9)**: Genre-level sales volume, average price by genre, repeat customers (`>= 2` orders), most frequently ordered book, top 3 most expensive Fantasy books, total books sold per author, high-spending customer cities, top-spending customer, and remaining stock after fulfilling all orders (`FULL JOIN` + `COALESCE`).
