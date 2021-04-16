---
title: create_sql_server_db    
description: Create new Microsoft SQL Server database for SuperOffice onsite
author: {github-id}
keywords: database
so.topic: howto 
so.envir: onsite
# so.client:
---

# Create new Microsoft SQL Server database

Are you going to run SuperOffice on a Microsoft SQL Server, follow these steps to set up the target database.

1. Create a new target database using the SQL Management tool.
2. Add a user (Security > Users). The user may be called CRM8, but you are free to name the user whatever you like.
3. Give the user db\_owner permissions (lower list) on the new database.
4. Create a new schema, the name of the schema will be the table prefix.
5. Create a new 32-bit ODBC System Data Source pointing to the new database.

If you want to take advantage of the [SQL Server full-text search][1] you need to [set this up][2] before you run **DBSetup**/**ServerSetup** to create the new SuperOffice CRM database.

<!-- Referenced links -->
[1]: https://docs.microsoft.com/en-us/sql/relational-databases/search/full-text-search?view=sql-server-2017
[2]: sql-server-full-text-search.md