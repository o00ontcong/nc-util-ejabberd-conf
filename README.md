# nc-util-ejabberd-conf
Bash alias:

export PATH=${PATH}:/home/nhancao/Softs/ejabberd-16.12.beta1/bin
alias xmpp.start='/home/nhancao/Softs/ejabberd-16.12.beta1/bin/start'
alias xmpp.stop='/home/nhancao/Softs/ejabberd-16.12.beta1/bin/stop'

---------------------------------------------------------------
##Setup mysql database:
https://docs.ejabberd.im/admin/guide/databases/mysql/

```
echo "GRANT ALL ON ejabberd.* TO 'ejabberd'@'localhost' IDENTIFIED BY 'password';" | mysql -h localhost -u root
echo "CREATE DATABASE ejabberd;" | mysql -h localhost -u ejabberd -p
wget https://raw.githubusercontent.com/processone/ejabberd/master/sql/mysql.sql
mysql -h localhost -D ejabberd -u ejabberd -p < mysql.sql
echo "SHOW TABLES;" | mysql -h localhost -D ejabberd -u ejabberd -p --table
```

Edit ejabberd.yml
```
sql_type: mysql
sql_server: "localhost"
sql_database: "ejabberd"
sql_username: "ejabberd"
sql_password: "password"
## If you want to specify the port:
sql_port: 3306


auth_method: sql


```

Create user on sql with cli
```
ejabberdctl register "testuser" "localhost" "passw0rd"
```


##Setup rest api
https://docs.ejabberd.im/developer/ejabberd-api/oauth

###Use api with basic auth

POST http://localhost:7011/api/get_roster
Authorization: Basic YWRtaW5AbG9jYWwuYmVlc2lnaHRzb2Z0LmNvbToxMjMzMjE=
Content-Type: application/json
{}

where: 
Authorization: Basic <userJid>:<password>

if you want use more command, you must add it to config 
add_commands: