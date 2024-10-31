# NewSQL

NewSQL is a unique database system that combines ACID compliance and horizontal scalability. Database systems strive to maintain the advantages of these two worlds. Integrating OLTP-based transactions with NoSQL’s high-performance solution.

```tsql
CREATE TABLE IF NOT EXISTS accounts (id INT PRIMARY KEY, balance INT);
INSERT INTO accounts (id, balance) VALUES (1, 1000), (2, 250);
```
