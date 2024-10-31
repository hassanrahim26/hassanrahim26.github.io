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

## Examples of NewSQL database systems

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

- **Deutsche Bank**
  - **Database:** YugabyteDB
  - **Use Case:** Deutsche Bank uses YugabyteDB to improve its banking operations, speeding up transaction processing.

- **Spotify**
  - **Database:** Google Cloud Spanner
  - **Use case:** Spotify uses Google Cloud Spanner to manage its user data and playlists, ensuring high availability and scalability as millions of users stream music simultaneously.

- **Expedia**
  - **Database:** TiDB
  - **Use Case:** Expedia uses TiDB to support its travel booking platform, managing millions of transactions each day with real-time data.

```tsql
CREATE TABLE IF NOT EXISTS accounts (id INT PRIMARY KEY, balance INT);
INSERT INTO accounts (id, balance) VALUES (1, 1000), (2, 250);
```