# NewSQL: Bridging the Gap between Scalability and Consistency

Today, companies need databases that can grow quickly as their data grows but still keep data accurate and safe. Traditional databases (called SQL databases) have been great at keeping data safe and consistent. They use what’s called “ACID” rules, which make sure that data is correct and secure. However, SQL databases have trouble getting bigger easily—especially when companies need them to handle millions of users and huge amounts of data.

To solve this, NoSQL databases were created. These databases are great for handling very large amounts of data and can spread data across many servers. But NoSQL databases often don’t guarantee that the data will always be consistent, which can make things complicated.

## Introducing NewSQL: Combining the Best of Both Worlds

NewSQL combines the advantages of SQL and NoSQL, offering both strong data consistency and the ability to handle large amounts of data.

Here’s why NewSQL stands out:

- **Scalability (Can Grow Easily):** Like NoSQL, NewSQL databases spread data across multiple servers, allowing them to grow with data needs.
  
- **Consistency (Reliable Data):** Unlike many NoSQL systems, NewSQL follows ACID rules to make sure data is accurate and consistent even across multiple servers.
  
- **Familiar SQL Language:** NewSQL uses SQL, the language that most developers already know, so there’s no need to learn a new way of writing queries.
  
- **Flexible Deployment:** NewSQL databases can run both in the cloud and on-site, giving companies more control. This is ideal for businesses that need tight security or low data delay (latency).

## Is NewSQL Right for You?

NewSQL might be a good choice if you need:

- **High Growth:** If you expect your app or website to grow quickly, NewSQL can handle big data
and lots of users.

- **Data Accuracy:** For apps that need real-time data that’s always correct, NewSQL gives peace of
mind because of its strong data consistency.

- **Easy Learning Curve:** If you already know SQL, working with NewSQL is easy because it uses the
same commands.

## Some examples of NewSQL database systems

- CockroachDB
- Google Spanner
- VoltDB
- NuoDB
- TiDB
- Clustrix
- YugabyteDB

## Real-World Examples: Who Uses NewSQL?

Some well-known companies are using NewSQL to power their high-growth applications, taking advantage of both reliability and scalability.

- **Slack**
  - **Database:** CockroachDB
  - **Use Case:** Slack relies on CockroachDB for messaging, ensuring fast, reliable data for millions of active users.
  <br><br>
- **Deutsche Bank**
  - **Database:** YugabyteDB
  - **Use Case:** Deutsche Bank uses YugabyteDB to improve its banking operations, speeding up transaction processing.
  <br><br>
- **Spotify**
  - **Database:** Google Cloud Spanner
  - **Use case:** Spotify uses Google Cloud Spanner to manage its user data and playlists, ensuring high availability and scalability as millions of users stream music simultaneously.
  <br><br>
- **Expedia**
  - **Database:** TiDB
  - **Use Case:** Expedia uses TiDB to support its travel booking platform, managing millions of transactions each day with real-time data.
  <br><br>

## Let’s Write Some NewSQL Queries Using CockroachDB

To get started with CockroachDB, first install it on your machine by following the instructions on the official [CockroachDB installation page](https://www.cockroachlabs.com/docs/v24.2/install-cockroachdb).

Once installed, you can access CockroachDB through the command-line interface (CLI) and start a local cluster to try out queries. Follow this guide to [start a local cluster](https://www.cockroachlabs.com/docs/stable/start-a-local-cluster).

Now that you’re set up, let’s write some queries with CockroachDB.

- Start the CockroachDB Cluster
  ```tsql
  sudo cockroach start-single-node --insecure --store=/var/lib/cockroach --listen-addr=localhost:26257 --http-addr=localhost:8080
  ```
  This command starts a single-node instance of CockroachDB.

- Access the SQL Shell
  
  Open a new terminal window and connect to the CockroachDB SQL shell using:
  ```tsql
  cockroach sql --insecure --host=localhost:26257
  ```
  This command connects you to the SQL shell where you can execute SQL queries.

- Create your first database
  ```tsql
  CREATE DATABASE online_store;
  ```
- Switch to your database
  ```tsql
  USE online_store;
  ```
- Creating Tables
  - Create a products table
    ```tsql
    CREATE TABLE products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name STRING NOT NULL,
    price DECIMAL(10,2),
    stock_count INT,
    last_updated TIMESTAMP DEFAULT current_timestamp()
    );
    ```
  - Create a customers table
    ```tsql
    CREATE TABLE customers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email STRING UNIQUE,
    name STRING,
    created_at TIMESTAMP DEFAULT current_timestamp()
    );
    ```
  - Create an orders table
    ```tsql
    CREATE TABLE orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_id UUID REFERENCES customers(id),
    total_amount DECIMAL(10,2),
    order_date TIMESTAMP DEFAULT current_timestamp()
    );
    ```
  - Show tables
    ```tsql
    SHOW TABLES;
    ```
    <img width="1440" alt="Screenshot 2024-11-01 at 9 18 51 PM" src="https://github.com/user-attachments/assets/e7b92746-2465-49e8-88c7-b583bf55988c">

- Basic Data Operations
  - Insert sample products
    ```tsql
    INSERT INTO products (name, price, stock_count) VALUES
        ('Laptop', 999.99, 50),
        ('Smartphone', 499.99, 100),
        ('Headphones', 79.99, 200);
    ```
  - Insert a customer
    ```tsql
    INSERT INTO customers (email, name) VALUES
        ('john@example.com', 'John Doe'),
        ('jane@example.com', 'Jane Smith');
    ```
  - View your data
    ```tsql
    SELECT * FROM products;
    ```
    <img width="1440" alt="Screenshot 2024-11-01 at 8 14 46 PM" src="https://github.com/user-attachments/assets/17779b04-b13c-4dd5-94aa-0a0b2cada475">
    
    ```tsql
    SELECT * FROM customers;
    ```
    <img width="1440" alt="Screenshot 2024-11-01 at 8 15 12 PM" src="https://github.com/user-attachments/assets/f123216c-5b73-42ce-826c-061a6d2e2b15">

- Transaction Example
  - Start a transaction for placing an order
    ```tsql
    BEGIN;
    ```
  - Insert new order
    ```tsql
    INSERT INTO orders (customer_id, total_amount) 
    SELECT id, 999.99 
    FROM customers 
    WHERE email = 'john@example.com';
    ```
  - Update product stock
    ```tsql
    UPDATE products 
    SET stock_count = stock_count - 1,
    last_updated = current_timestamp()
    WHERE name = 'Laptop' 
    AND stock_count > 0;
    ```
  - Commit the transaction
    ```tsql
    COMMIT;
    ```
  - View the results
    ```tsql
    SELECT * FROM orders;
    ```
    ```tsql
    SELECT name, stock_count FROM products WHERE name = 'Laptop';
    ```