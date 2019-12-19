# magento-docker
Custom docker setup for Magento example using Nginx/PHP-FPM web server, mySQL and Redis. It is based on the `hansphung` docker images. 

# Installation
Get the clone by running the following command in the terminal:

`git clone https://github.com/zaifastafa/magento-docker.git`

Execute the following commands using the `magento` script which is a helpful wrapper for the `docker-compose` commands.

### Setup
- Start all the containers: `./magento start`
- Install magento through a command line wizard: `./magento magerun install`
    - use `db` for database `host`
    - use the directory `.` for the root directory. It will be installed in the `var/www/html` folder
    - use `root` for username and password (can be configured through environment variables)
    - use `http://127.0.0.1:8010` for base URL (also configurable)

Note: you can type `no` when it prompts to import sample data as it sometimes causes timeouts

If everything goes well, you will see the following message at the end: 

```
✔ MySQL Version 5.7.28 found.
✔ Required MySQL Storage Engine InnoDB found.
Successfully installed magento
```
To enter into different containers use: `./magento enter [php, db ... ]`

### Remove
If for any reason you need to install a fresh copy of Magento
- Stop magento containers: `./magento stop`
- Remove the `var` folder. You might need to use `sudo` due to permission issues
- Follow the steps mentioned in the Setup section

 
### mySQL import
For database, we use mysql offical image v.5.7. Using v.8 or latest image gives an authenticn issue. You can change the root password through environment variable `MYSQL_ROOT_PASSWORD`. To keep the data persitence, we create a volume and mount it to a directory under `var`: `./var/lib/mysql:/var/lib/mysql`
### Load a mySQL dump file to the container
To import an existing `.sql` dump to a database in the container, execute this inside the `db` container:

`mysql -u username -p database_name < file.sql`

# docker-compose wrapper
This is a script to shorten the docker-compose commands. The script was copied and modified from https://github.com/hanhpv/dockerized-magento/blob/master/magento.

Available commands:

```
start      Starts the docker containers
stop       Stops all docker containers
restart    Restarts all docker containers
status     Prints the status of all docker containers
stats      Displays live resource usage statistics of all containers
magerun    Executes magerun in the magento root directory
composer   Executes composer in the magento root directory
enter      Enters the bash of a given container type (e.g. php, db)
destroy    Stops all containers and removes all data. 
```

## Disclaimer
We are not affiliated, associated, authorized, endorsed by, or in any way officially connected with Magento, or any of its subsidiaries or its affiliates.

The names Magento as well as related names, marks, emblems and images are registered trademarks of their respective owners. 

# License
MIT License

Copyright (c) 2019 Huzaifa Mustafa

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
