# Server setup

To rebuild the server:

1. Run the scripts documented in *server-config*
2. `scp` the pitch-home.conf and pitch-web.conf files to the home folder of the ubuntu user. Then move the files into the proper apache folder:

```bash
scp pitch-web.conf pitch-home.conf pitch-web:~/

ssh pitch-web
#on the server
sudo cp ~/*.conf /etc/apache2/sites-enabled
```
3. Create a directory for the www.tagpitch.com web page:
```bash
mkdir /var/www/home
```
And then scp all home page files to the server and copy them to directory.

4. Upload the production database settings in a file called database.yml. The format for this file is:
```yml
production:
  adapter: mysql2
  encoding: utf8
  database: deck
  username: root
  password: PASSWORD
  host: deck-production.cfmjmatrvdif.us-west-2.rds.amazonaws.com
  port: 3306
```

Make sure to replace the password. This file just needs to live in your home directory.

5. Add environment variables for Gmail SMTP proxy, in */etc/apache2/envvars*

```bash
export GMAIL_USERNAME="no-reply@tagpitch.com"
export GMAIL_PASSWORD="the password for this account"
```
Make sure you replace the password.

6. Restart Apache after any config/file changes
```bash
sudo /etc/init.d/apache2 restart
```
