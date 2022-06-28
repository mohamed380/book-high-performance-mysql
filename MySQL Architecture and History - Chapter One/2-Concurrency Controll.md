## Concurrency Control
Anytime more than one query needs to change data at the same time, the problem of
concurrency control arises. MySQL has to do this at
two levels: `the server level and the storage engine level`

### Read/Write Locks
Systems that deal with concurrent read/write access typically implement a locking system that
consists of two lock types:
* Read locks on a resource are shared or mutually nonblocking
* Write locks, on the other hand, are exclusive, they block both read locks and other write
  locks

### Lock Granularity
To improve concurrency we can be more selective to what will be locked, locking the entire table, row or a specific column.
> The more selective the more concurrent and the more resources consuming because of locking handling
* Table Locks
    * The most basic strategy with the lowest overhead.
    * When a client wishes to write to a table (insert, delete, update,
      etc.), it acquires a write lock
    * Write locks have a higher priority than read locks, even if there is a read lock in the queue.
    * Although storage engines can manage their own locks, MySQL itself also uses a variety
      of locks that are effectively table-level for various purposes, while ALTER TABLE statement for example.
* Row Locks
    * Offers the greatest concurrency and carries the greatest overhead.
    * Implemented in the storage engine, not the server
    * Available in innoDB and XtraDB storage engines