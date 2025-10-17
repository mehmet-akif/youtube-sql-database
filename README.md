# YouTube Channel Database using Oracle SQL

## Overview

This project models a simplified version of **YouTube’s user and subscription system** using **Oracle SQL Developer**.  
It demonstrates the creation of database tables, relationships, and analytical queries to extract insights such as user subscriptions, channel categories, and content creator activity.

The project showcases skills in **database design**, **relational modeling**, and **SQL query optimization**.

---

## Table of Contents
- [Database Schema](#database-schema)
- [Implemented Queries](#implemented-queries)
- [Results](#results)
- [Technologies Used](#technologies-used)
- [Usage](#usage)
- [Files Included](#files-included)

---

## Database Schema

The database consists of **three related tables**:

1. **`yt_user`** – Stores YouTube user information (user ID, name, Gmail).  
2. **`channel`** – Stores channel details (ID, name, category, URL, creator ID).  
3. **`subscription`** – Represents user subscriptions to channels.

Each table is linked via **foreign key relationships**:

```sql
yt_user.user_id → channel.user_id  
channel.ch_id → subscription.ch_id  
yt_user.user_id → subscription.user_id
```

---

## Implemented Queries

### 1. List of non-business channels
```sql
SELECT ch_name, ch_id
FROM channel
WHERE ch_category != 'Business';
```

### 2. List of personal channels and their creators
```sql
SELECT user_name, ch_name
FROM channel
JOIN yt_user ON channel.user_id = yt_user.user_id
WHERE ch_category = 'Personal';
```

### 3. Personal channels belonging to Alice
```sql
SELECT yt_user.user_id, yt_user.user_name, channel.ch_name
FROM channel
JOIN yt_user ON channel.user_id = yt_user.user_id
WHERE ch_category = 'Personal' AND yt_user.user_name = 'Alice';
```

### 4. List of channels with subscription counts
```sql
SELECT ch_name, COUNT(subscription_id) AS num_subscriptions
FROM channel
LEFT JOIN subscription ON channel.ch_id = subscription.ch_id
GROUP BY ch_name;
```

### 5. Channels with zero subscriptions
```sql
SELECT ch_name, COUNT(subscription_id) AS num_subscriptions
FROM channel
LEFT JOIN subscription ON channel.ch_id = subscription.ch_id
GROUP BY ch_name;
```

### 6. List of channels, their creators, and number of subscriptions
```sql
SELECT ch_name, user_name, COUNT(subscription_id) AS num_subscriptions
FROM channel
JOIN yt_user ON channel.user_id = yt_user.user_id
LEFT JOIN subscription ON channel.ch_id = subscription.ch_id
GROUP BY ch_name, user_name;
```

### 7. Total number of subscriptions
```sql
SELECT COUNT(subscription_id) AS total_number_of_subscriptions
FROM subscription;
```

---

## Results

- Schema successfully created in **Oracle SQL Developer (11g)**.  
- Queries executed with results returned in under **0.05 seconds** each.  
- Verified referential integrity between all foreign keys.  

### Derived insights:
- Total subscriptions across all channels = **31**  
- “Art” channel belongs to **Alice** under *Personal* category  
- Channels like *Class* and *Books* have the **highest subscription counts**  

📸 *Screenshots of executed queries are included in the repository.*

---

## Technologies Used

- **Database:** Oracle SQL 11g  
- **Tool:** Oracle SQL Developer  
- **Language:** SQL (DDL, DML, and DQL)  
- **Concepts:**  
  - Schema design  
  - Foreign key constraints  
  - JOIN operations  
  - GROUP BY & HAVING clauses  
  - Aggregate functions  

---

## Usage

1. Open **Oracle SQL Developer**.  
2. Connect to your Oracle 11g instance.  
3. Run the SQL script:
   ```sql
   @Lab1.sql
   ```
4. Execute queries individually or all together to explore:
   - Channel categories  
   - Subscriptions  
   - Creator statistics  


---

## License
This project is open-source under the **MIT License**.
