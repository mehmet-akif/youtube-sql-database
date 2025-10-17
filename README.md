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

---

## Implemented Queries
