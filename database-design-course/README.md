# Notes

| Terms| Description |
| ---- | ----------- |
| Entity | eg. student (A table should be about on entity) |
| Attribute | (Non-key columns) eg. student name, address |

## Relationships

- Break big table to smaller tables and make relationships
- To know relationship between parent table and child table are important
    - primary key goes on parent and foreign key goes on child


### One to One

> Bi-direction that target table and current table point to each other

E.g husband and wife, Soical Security number (SSN) and American

- We can often store one to one relationshp as **attribute** rather than entities

> **Note**  
> There will be occasional times when we store a one to one relationship over multiple tables

E.g.

```mermaid
erDiagram
  Cardholder ||--o| Card: have
  Cardholder {
        string Id
        int cardId
        string model
  }
  Card {
        string Id
        string issue
        string maxAmount
  }
```

Therefore, the way to store 1:1 relationship is
  1. Attrible within the table
  2. Another table (can use foreign key to connect them)

### One to Many

> One direction to point target table from current table

```mermaid
erDiagram
  User ||--o{ Comment: have
```

### Many to Many

E.g class and student

- Need an inter-mediary table (junction table)

```mermaid
erDiagram
  CLASS ||--|{ classStudent: junction
  Student ||--|{ classStudent: junction
```

## Keys



## Indices

An index is a data structure that you build and assign on top of existing table
and analyze it and summerize it so that it can create a shortcut

- b-tree, and ???-tree

> The B-tree generalizes(概括) the binary search tree, allowing for nodes with more than two children.

```sql
create index employees_name on employees(name);
```

- Clustered:
- Non-clustered: 

> We can only choose one of these two

### Clustered

### Non-clustered

## Database Normalization

**1NF**

- Each cell to be single valued
- Entries in a column are same type => eg. eyeColor should contain blue, green instead of beautiful
- Rows uniquely identified =>  Add Unique ID or add more columns to make unique

**2NF**

- All a ttributes (Non-key columns) not dependtent on the key should be separated out

**3NF**

- All fields (all columns) can be determined only by the key in the table and no other column

**4NF**

- No multi-valued dependencies

## Finished Topics

### Database Design Course

- [x] Relationships
- [x] One to One Relationships + Design
- [x] One to Many Relationships + Design
- [x] Many yo Many Relationships + Design
- [ ] Keys
- [ ] Indices
- [ ] Database Normalization

## References

1. [Caleb Curry; Database Design Course - Learn how to design and plan a database for beginners (2018.8)](https://youtu.be/ztHopE5Wnpc)
2. [Normalization - 1NF, 2NF, 3NF and 4NF (2015.08)](https://youtu.be/UrYLYV7WSHM)
