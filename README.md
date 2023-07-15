# Frappe-ERPNext-Version-14--in-Ubuntu-22.04-LTS
A complete Guide to Install Frappe/ERPNext version 14  in Ubuntu 22.04 LTS



### Pre-requisites 

      Python 3.6+
      Node.js 14+
      Redis 5                                       (caching and real time updates)
      MariaDB 10.3.x                                (to run database driven apps)
      yarn 1.12+                                    (js dependency manager)
      pip 20+                                       (py dependency manager)
      wkhtmltopdf (version 0.12.5 with patched qt)  (for pdf generation)
      cron                                          (bench's scheduled jobs: automated certificate renewal, scheduled backups)
      NGINX                                         (proxying multitenant sites in production)



### STEP 1 Install git
    sudo apt-get install git

### STEP 2 install python-dev

    sudo apt-get install python3-dev

### STEP 3 Install setuptools and pip (Python's Package Manager).

    sudo apt-get install python3-pip

### STEP 4 Install virtualenv
    
    sudo apt-get install virtualenv
    sudo apt install python3.10-venv
    

### STEP 5 Install MariaDB

    sudo apt-get install software-properties-common
    sudo apt install mariadb-server
    
    
### STEP 6  MySQL database development files

    sudo apt-get install libmysqlclient-dev

### STEP 7 Edit the mariadb configuration ( unicode character encoding )

    sudo nano /etc/mysql/my.cnf

add this

    
    [mysqld]
      character-set-client-handshake = FALSE
      character-set-server = utf8mb4
      collation-server = utf8mb4_unicode_ci

    [mysql]
      default-character-set = utf8mb4


    sudo service mysql restart

### STEP 8 install Redis
    
    sudo apt-get install redis-server

### STEP 9 install Node.js 14.X package

    sudo apt install curl 
    curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
    source ~/.profile
    nvm install 14

### STEP 10  install Yarn

    sudo apt-get install npm

    sudo npm install -g yarn

### STEP 11 install wkhtmltopdf

    sudo apt-get install xvfb wkhtmltopdf
    

### STEP 12 install frappe-bench

    sudo pip install frappe-bench
    
    bench --version
    
### STEP 13 initilise the frappe bench & install frappe latest version 

    bench init frappe-bench --frappe-branch version-14
    
    cd frappe-bench/
    bench start
    
### STEP 14 create a site in frappe bench 
    
    bench new-site jlp.site
    
    bench use jlp.site

### STEP 15 install ERPNext latest version in bench & site

    
    bench get-app payments
    
    bench get-app erpnext --branch version-14

    bench --site jlp.site install-app erpnext
    
    bench start
    
### Step 16 setup production
    
    sudo bench setup production [user]
    bench restart

#### If bench restart is not worked run the following command again with all Questions Yes
    
    sudo bench setup production [user]
    
#### if js and css file is not loading on login window run the following command

    sudo chmod o+x /home/[user]
    
#### STEP 17 Create a new user
    
    sudo adduser [user]
    sudo usermod -aG sudo [user]
    su - [user]

    
    
    
#### STEP 16 SSL certificate for https
    
    sudo apt install certbot python3-certbot-nginx
    certbot -d {domain_name} --register-unsafely-without-email
