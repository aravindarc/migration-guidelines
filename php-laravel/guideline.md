# Environment Setup

1. First complete the DB setup required for the application, use mysql workbench(mysql) or azure data studio(mssql)
2. Install apache server and check if it is running, load `localhost` on browser it should load apache default page.
    * `sudo systemctl restart apache2.service`
    * To check status of the service use `sudo systemctl status apache2.service`
3. Install php and check by running `php --version`
    * `sudo apt install php7.2 php7.2-mysql libapache2-mod-php7.2`, change version as needed.
    * If you have multiple php installations, you can switch the php version by using `sudo update-alternatives --set php /usr/bin/php7.2`
4. Create a file `/var/www/html/index.php` with content:
    ```php
    <?php
    phpinfo();
    ?>
    ```
5. Load localhost, it should show the php information
6. In the file `/etc/apache2/apache2.conf` find a block called `<Directory /var/www/>` and edit it:
    ```
    <Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ```

# Run the application in local

1. Create a symlink for the application in `/var/www/html` by running `sudo ln -s /home/aravindarc/Consulting/MM/app /var/www/html/app`
2. Once this is created the application will be available at `localhost/app/`
3. Try the opening the application, if there are errors, you can find the error logs at locations `/var/log/apache2/error.log`, `./storage/logs/laravel.log`
4. All your db connection and base path will be located in `./.env` file, change the db username, password and other configurations.
5. If you want to use system environment variables to override the configuration in `.env` file
   * Create a function in `./app/Helpers/Helpers.php`:
   ```php
    public static function loadEnv(string $envName, $defaultValue = null)
    {
        if (getenv($envName) != false) {

            switch (strtolower(getenv($envName))) {
                case 'true':
                case '(true)':
                    return true;
                case 'false':
                case '(false)':
                    return false;
                case 'empty':
                case '(empty)':
                    return '';
                case 'null':
                case '(null)':
                    return null;
            }
        }

        return env($envName, $defaultValue);
    }
   ```
    * Find the places in code where you want to use `loadEnv()`, there will be `env()` used already, replace that with `loadEnv()`.
    * Now you can override configurations in `./.env` file by setting the system environment variables using `export DB_URL=127.0.0.1` when starting apache server or in the `./.htaccess` using `SetEnv DB_URL 127.0.0.1` command.
6. Login into the application and ensure db connection is working.

# Add Dockerfile and Helm Charts

1. You can use the sample Dockerfile and httpd.conf provided in this directory
2. The available base images are:
    * aravindbootlabs/php-apache-alpine:php-7.2.3_apache-2_alpine-3.7
    * aravindbootlabs/php-apache-alpine:php-5.6_apache-2_alpine-3.7
3. If you need any other php version, mail at `aravind.kumar@bootlabstech.com`
4. You can use the sample `httpd.conf` file, change the below line to match your php version:

    `LoadModule php5_module        modules/libphp5.so`
5. Copy paste the `httpd.conf` file to `.apache/.httpd.conf` in you application directory
6. You can use the sample helm chart in this directory.
7. Copy paste the `helm-chart` directory to your application directory and do a global search and replace `myapp` with your application name
8. For each environment use a file `environment/<env>-values.yaml`
9. To override values in `.env` file you can add under `podEnv:` block in `<env>-values.yaml`

