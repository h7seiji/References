# SQL Databases

## Key Features

- Relational/Normalized data - changes to one table may require changes to others
  - E.g. adding an author and their books to different tables on different nodes
  - May require two phase commit (Expensive)
- Have transactional (ACID guarantees)
  - Excessively slow if you don't need them (due to two phase locking)
- Typically use B-trees
  - Better for reads than writes in theory
