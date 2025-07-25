---
source_url: https://go.dev/doc/database/prepared-statements
title: Using prepared statements - The Go Programming Language
crawl_date: 2025-07-25T12:08:26.400557
watsonmd_version: 0.1.0
---

# Using prepared statements

You can define a prepared statement for repeated use. This can help your code run a bit faster by avoiding the overhead of re-creating the statement each time your code performs the database operation.

**Note:** Parameter placeholders in prepared statements vary depending on the DBMS and driver you’re using. For example, the [pq driver](https://pkg.go.dev/github.com/lib/pq) for Postgres requires a placeholder like `$1` instead of `?`.

### What is a prepared statement?

A prepared statement is SQL that is parsed and saved by the DBMS, typically containing placeholders but with no actual parameter values. Later, the statement can be executed with a set of parameter values.

### How you use prepared statements

When you expect to execute the same SQL repeatedly, you can use an `sql.Stmt` to prepare the SQL statement in advance, then execute it as needed.

The following example creates a prepared statement that selects a specific album from the database. [`DB.Prepare`](https://pkg.go.dev/database/sql#DB.Prepare) returns an [`sql.Stmt`](https://pkg.go.dev/database/sql#Stmt) representing a prepared statement for a given SQL text. You can pass the parameters for the SQL statement to `Stmt.Exec`, `Stmt.QueryRow`, or `Stmt.Query` to run the statement.
    
    
    // AlbumByID retrieves the specified album.
    func AlbumByID(id int) (Album, error) {
        // Define a prepared statement. You'd typically define the statement
        // elsewhere and save it for use in functions such as this one.
        stmt, err := db.Prepare("SELECT * FROM album WHERE id = ?")
        if err != nil {
            log.Fatal(err)
        }
        defer stmt.Close()
    
        var album Album
    
        // Execute the prepared statement, passing in an id value for the
        // parameter whose placeholder is ?
        err := stmt.QueryRow(id).Scan(&album.ID, &album.Title, &album.Artist, &album.Price, &album.Quantity)
        if err != nil {
            if err == sql.ErrNoRows {
                // Handle the case of no rows returned.
            }
            return album, err
        }
        return album, nil
    }
    

### Prepared statement behavior

A prepared [`sql.Stmt`](https://pkg.go.dev/database/sql#Stmt) provides the usual `Exec`, `QueryRow`, and `Query` methods for invoking the statement. For more on using these methods, see [Querying for data](/doc/database/querying) and [Executing SQL statements that don’t return data](/doc/database/change-data).

However, because an `sql.Stmt` already represents a preset SQL statement, its `Exec`, `QueryRow`, and `Query` methods take only the SQL parameter values corresponding to placeholders, omitting the SQL text.

You can define a new `sql.Stmt` in different ways, depending on how you will use it.

  * `DB.Prepare` and `DB.PrepareContext` create a prepared statement that can be executed in isolation, by itself outside a transaction, just like `DB.Exec` and `DB.Query` are.
  * `Tx.Prepare`, `Tx.PrepareContext`, `Tx.Stmt`, and `Tx.StmtContext` create a prepared statement for use in a specific transaction. `Prepare` and `PrepareContext` use SQL text to define the statement. `Stmt` and `StmtContext` use the result of `DB.Prepare` or `DB.PrepareContext`. That is, they convert a not-for-transactions `sql.Stmt` into a for-this-transaction `sql.Stmt`.
  * `Conn.PrepareContext` creates a prepared statement from an `sql.Conn`, which represents a reserved connection.



Be sure that `stmt.Close` is called when your code is finished with a statement. This will release any database resources (such as underlying connections) that may be associated with it. For statements that are only local variables in a function, it’s enough to `defer stmt.Close()`.

#### Functions for creating a prepared statement

Function | Description  
---|---  
`[DB.Prepare](https://pkg.go.dev/database/sql#DB.Prepare)`  
`[DB.PrepareContext](https://pkg.go.dev/database/sql#DB.PrepareContext)` | Prepare a statement for execution in isolation or that will be converted to an in-transaction' prepared statement using Tx.Stmt.  
`[Tx.Prepare](https://pkg.go.dev/database/sql#Tx.Prepare)`  
`[Tx.PrepareContext](https://pkg.go.dev/database/sql#Tx.PrepareContext)`  
`[Tx.Stmt](https://pkg.go.dev/database/sql#Tx.Stmt)`  
`[Tx.StmtContext](https://pkg.go.dev/database/sql#Tx.StmtContext)` | Prepare a statement for use in a specific transaction. For more, see [Executing transactions](/doc/database/execute-transactions).   
`[Conn.PrepareContext](https://pkg.go.dev/database/sql#Conn.PrepareContext)` | For use with reserved connections. For more, see [Managing connections](/doc/database/manage-connections).