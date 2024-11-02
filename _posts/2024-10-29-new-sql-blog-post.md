# NewSQL: Bridging the Gap between Scalability and Consistency

Today, companies need databases that can grow quickly as their data grows but still keep data accurate and safe. Traditional databases (called SQL databases) have been great at keeping data safe and consistent. They use what’s called “ACID” rules, which make sure that data is correct and secure. However, SQL databases have trouble getting bigger easily—especially when companies need them to handle millions of users and huge amounts of data.

To solve this, NoSQL databases were created. These databases are great for handling very large amounts of data and can spread data across many servers. But NoSQL databases often don’t guarantee that the data will always be consistent, which can make things complicated.

## Introducing NewSQL: Combining the Best of Both Worlds

NewSQL combines the advantages of SQL and NoSQL, offering both strong data consistency and the ability to handle large amounts of data.

![Screenshot from 2024-11-02 09-58-55](https://github.com/user-attachments/assets/1dc3f8a9-1eb0-4091-87ec-c0744017ce78)

Here’s why NewSQL stands out:

- **Scalability (Can Grow Easily):** Like NoSQL, NewSQL databases spread data across multiple servers, allowing them to grow with data needs.
  
- **Consistency (Reliable Data):** Unlike many NoSQL systems, NewSQL follows ACID rules to make sure data is accurate and consistent even across multiple servers.
  
- **Familiar SQL Language:** NewSQL uses SQL, the language that most developers already know, so there’s no need to learn a new way of writing queries.
  
- **Flexible Deployment:** NewSQL databases can run both in the cloud and on-site, giving companies more control. This is ideal for businesses that need tight security or low data delay (latency).

## Is NewSQL Right for You?

![Screenshot from 2024-11-02 09-59-25](https://github.com/user-attachments/assets/28f8605c-1466-4d49-9554-b608410235b0)

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

- **Start the CockroachDB Cluster**
  ```tsql
  sudo cockroach start-single-node --insecure --store=/var/lib/cockroach --listen-addr=localhost:26257 --http-addr=localhost:8080
  ```
  This command starts a single-node instance of CockroachDB.


- **Access the SQL Shell**
  
  Open a new terminal window and connect to the CockroachDB SQL shell using:
  ```tsql
  cockroach sql --insecure --host=localhost:26257
  ```
  This command connects you to the SQL shell where you can execute SQL queries.


- **Create your first database**
  ```tsql
  CREATE DATABASE online_store;
  ```
  
- **Switch to your database**
  ```tsql
  USE online_store;
  ```
  
- **Creating Tables**
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


- **Basic Data Operations**
  - Insert sample products
    ```tsql
    INSERT INTO products (name, price, stock_count) VALUES
        ('Laptop', 999.99, 50),
        ('Smartphone', 499.99, 100),
        ('Headphones', 79.99, 200);
    ```
    ```tsql
    SELECT * FROM products;
    ```
    ![photo_5_2024-11-01_22-23-32](https://github.com/user-attachments/assets/df02b70e-7493-4150-b2e3-95d1819028c2)
    
  - Insert a customer
    ```tsql
    INSERT INTO customers (email, name) VALUES
        ('john@example.com', 'John Doe'),
        ('jane@example.com', 'Jane Smith');
    ```
    ```tsql
    SELECT * FROM customers;
    ```
    ![photo_7_2024-11-01_22-23-32](https://github.com/user-attachments/assets/98315033-8eda-4c9d-b181-82eeda6a29d6)

  - Update a customer
    ```tsql
    UPDATE customers
      SET email = 'jane@xyz.com'
      WHERE id = 'b0ad55ff-4894-4959-8883-d6e651daeaae';
    ```
    ```tsql
    SELECT * FROM customers;
    ```
    ![photo_1_2024-11-01_22-23-32](https://github.com/user-attachments/assets/08ffc9d6-e77b-4de7-ae49-716e80320ee4)

  - DELETE a product
    ```tsql
    DELETE FROM products WHERE id = '8baa470f-094f-49e1-a0d2-0fb65303edcc'
    ```
    ```tsql
    SELECT * FROM products;
    ```
    ![Screenshot from 2024-11-01 23-02-07](https://github.com/user-attachments/assets/3770321e-59ad-4ceb-b876-12b44b3e2dda)

    
- **Transaction Example**
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
    ![photo_6_2024-11-01_22-23-32](https://github.com/user-attachments/assets/53cce887-f9b5-46dd-a21a-697e856b7bf6)

    ```tsql
    SELECT name, stock_count FROM products WHERE name = 'Laptop';
    ```
    ![photo_8_2024-11-01_22-23-32](https://github.com/user-attachments/assets/239127fc-0051-4332-a6b3-b611029b7e29)

  As you continue exploring CockroachDB, you might want to dive deeper into advanced features like geo-partitioning, fault tolerance, and advanced indexing. You can find more resources in the [CockroachDB documentation](https://www.cockroachlabs.com/docs)

## Conclusion
In this blog, we explored NewSQL and its ability to bridge the gap between traditional SQL and NoSQL. NewSQL databases, like CockroachDB, provide the scalability of NoSQL with the consistency and reliability of SQL, making them a perfect choice for modern, data-driven applications. With NewSQL, you don’t have to choose between scaling your data and keeping it accurate—NewSQL offers both. 

Whether you’re building a simple app or a large-scale system, NewSQL has the tools and flexibility to support your project’s growth. Its combination of SQL familiarity, advanced data management, and scaling capabilities makes it a powerful database choice for developers today. Happy coding!