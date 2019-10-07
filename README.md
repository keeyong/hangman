# hangman
A lecture sample code from http://inventwithpython.com/chapter9.html

## hangman_web.py

- Requires MySQL

- If you want to run this in EC2 Ubuntu server, here is what you need to do:

```
sudo apt update
git clone https://github.com/keeyong/hangman.git

# install mysql and flask modules
sudo apt install python3-pip
sudo pip3 install flask
sudo pip3 install pymysql

# install mysql server
sudo apt-get install mysql-server
sudo systemctl start mysql
sudo systemctl enable mysql
```

- Next you need to set up MySQL credentials. By default, MySQL root account's password isn't available
```
sudo cat /etc/mysql/debian.cnf .  # get the password of debian-sys-maint
/usr/bin/mysql -u debian-sys-maint -p .   # type the password from the previous step
```

- In the mysql shell, run the following 3 commands (change the password accordingly and use it in the Python code)
```
UPDATE mysql.user SET plugin='mysql_native_password' WHERE User='root';
UPDATE mysql.user set authentication_string=password('YOUR_PASSWORD') where user='root';
FLUSH PRIVILEGES;
```

- Now using the ID/PW you created earlier, log in to the shell again and create a database ("test") and a word table ("words")
```
/usr/bin/mysql -u root -p
mysql> CREATE DATABASE test;
mysql> CREATE TABLE words ( word varchar(64) );
mysql> INSERT INTO test.words value ("iphone");
mysql> INSERT INTO test.words value ("cookie");
mysql> INSERT INTO test.words value ("airplane");
```

- Finally to run the code (note that Flask app is using port 80 and the port needs to be open). Change directory to the hangman folder 
```
sudo python3 hangman_web.py
```

- Access the server (either localhost or a server)
