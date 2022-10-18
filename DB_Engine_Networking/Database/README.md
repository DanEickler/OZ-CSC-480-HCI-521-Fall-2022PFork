# Prerequisites
- A running MySQL server 
- JRE 11
- Maven

# Setup

## MySQL
- Enter your MySQL shell
- Create a MySQL user with all privileges on all databases. The commands to do this are: <br/> 
`CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';`<br> 
`GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost'; FLUSH PRIVILEGES;` 
<br><br>**Replace username and password with a username and password to be used as the admin user for the database. 
<br><br>Replace localhost with the IP the user will be accessing from. If the MySQL server is running on the same machine you can leave it as localhost.<br/><br/>**
## .env File
A file named `.env` is expected to be located in `OZ-CSC-480-HCI-521-Fall-2022`. This file will contain the credentials for three MySQL users that are utilized by the project. `MYSQL_INITIALIZATION_USER` has admin privileges and is used to create the database and the other two users.  
`MYSQL_REST_USER` is the MySQL user that is utilized indirectly by any user accessing the database through the frontend. For security, this user will have read-only privileges aside from changing stored emojis. `MYSQL_BOT_USER` is the MySQL user that the bot utilizes in order to create, read, updated, and delete items from the database.  
<br>The .env file should contain the following:

```
DISCORD_BOT_TOKEN=""

MYSQL_URL="jdbc:mysql://localhost:3306/"

MYSQL_INITIALIZATION_USER="OZ_init"
MYSQL_INITIALIZATION_USER_PASSWORD="password"

MYSQL_REST_USER="OZ_rest"
MYSQL_REST_USER_PASSWORD="password"

MYSQL_BOT_USER="OZ_bot"
MYSQL_BOT_USER_PASSWORD="password"
```

Note: It is recommended to surround the values with quotes to prevent some machines causing issues with special characters.
- Set `DISCORD_BOT_TOKEN` equal to the token of your discord bot. (Not necessary for testing the standalone database module)
- Set `MYSQL_URL` equal to the URL of your MySQL server. localhost being the IP address, then 3306 being the port (default).
- Set `MYSQL_INITIALIZATION_USER` equal to the username of the MySQL user you created earlier.
- Set `MYSQL_INITIALIZATION_USER_PASSWORD` equal to the password of the MySQL user you created earlier.
- Set `MYSQL_REST_USER_PASSWORD` AND `MYSQL_BOT_USER_PASSWORD` to two new, unique passwords. These users will be created. You can change their usernames if you'd like, but it isn't necessary.

# Testing the Database Module
In a new testing class, a `Database` object can be constructed with `new Database testDB(guildID, User)`
For testing purposes, guildID can be any long integer. User can be: <br>
- `User.BOT` (Recommended. Has broader permissions for more through testing) 
- `User.REST` (Read-only, utilized by users through the frontend)
- `User.INIT` (should not be used for this case as its only purpose is to create the database and users.) 

It is recommended to also include the following line in order to output constructed queries and results to the console:
`testDB.toggleQueryVisible();`
<br><br> Upon constructing a `Database` class, `Create`, `Read`, `Update`, and `Delete` classes are also constructed. These classes are used to perform the respective CRUD operations on the MySQL database. An example of one such operation is below:
<br>`testDB.create.author(374978505777217546L, "Dan", "MegadanX5", 4825);` 
<br>With parameters: authorDiscordID, "nickname", "username", discriminator
<br>For further information on specific interactions with the CRUD classes, please refer to the JavaDoc comments within the source code, or contact Daniel Eickler. 