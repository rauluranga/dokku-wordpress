![alt text](https://cirovladimir.files.wordpress.com/2018/01/wp-dokku.png "Dokku")

### Requirements:

1. dokku should be already installed in your instance.
1. [dokku mariadb plugin](https://github.com/dokku/dokku-mariadb).

### Steps 

1. Inside your instance run the following commands:

  ```
  ~ dokku apps:create mywpsite
  ~ dokku mariadb:create mywpdb
  ~ dokku mariadb:link mywpdb mywpsite
  ```

1. Generate SALT keys from: [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/)

1. Setup ENV vars:

  ```
  ~ dokku config:set --no-restart mywpsite DOMAIN_NAME='YOUR_WP_DOMAIN_NAME'
  ~ dokku config:set --no-restart mywpsite AUTH_KEY='YOUR_AUTH_KEY_VALUE'
  ~ dokku config:set --no-restart mywpsite SECURE_AUTH_KEY='YOUR_SECURE_AUTH_KEY'
  ~ dokku config:set --no-restart mywpsite LOGGED_IN_KEY='YOUR_LOGGED_IN_KEY'
  ~ dokku config:set --no-restart mywpsite NONCE_KEY='YOUR_NONCE_KEY'
  ~ dokku config:set --no-restart mywpsite AUTH_SALT='YOUR_AUTH_SALT'
  ~ dokku config:set --no-restart mywpsite SECURE_AUTH_SALT='YOUR_SECURE_AUTH_SALT'
  ~ dokku config:set --no-restart mywpsite LOGGED_IN_SALT='YOUR_LOGGED_IN_SALT'
  ~ dokku config:set --no-restart mywpsite NONCE_SALT= 'NONCE_SALT'
  ```
1. Mount your `uploads` folder!

  ```
  ~ dokku storage:mount wp /var/lib/dokku/data/wp/uploads:/app/public/uploads
  ```
  
1. Enjoy!