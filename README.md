# BASH PostgreSQL `pg-execute`

### (forked from: [MySQL/MariaDB `execute`](https://github.com/Dev-Op5/execute))

An impressive ~~black magic~~ management tools to easily maintain your SQL code.

## 1. INSTALLATION

You have **no need** to `git clone` this repo to implement this on your Linux Box. Just [download from here](https://raw.githubusercontent.com/Dev-Op5/pg-execute/master/pg-execute) and copy the `pg-execute` file to folder `/usr/local/bin`. 

```bash
cd /tmp
wget https://github.com/Dev-Op5/pg-execute.git
chmod +x /tmp/pg-execute
sudo cp /tmp/pg-execute /usr/local/bin
```

Of course, there is no restriction if you wanna fork this repo and changes the code to suit your needs. I'll be happy if you add the functionality to this script to make this more powerful. Please don't hesitate to gimme pull requests.

Example :

```bash
mkdir -p ~/MyScripts
cd ~/MyScripts/
git clone https://github.com/Dev-Op5/pg-execute.git pg-execute 
chmod +x pg-execute/pg-execute
sudo ln -s ~/MyScripts/pg-execute/pg-execute /usr/local/bin 
```

## 2. COMMON USAGE: backup & restore

To perform backup just type in the directory that **already have** the `db.conf` file:

```bash
pg-execute backup
```

This command will generate sub-folder with the name based on the date when you perform backup (format: `YYYY-MM-DD`), e.g. `2021-10-02`

To perform restore, just type the `execute restore` and add extra-parameter with the name of the folder that you've previously backup.

```bash
pg-execute restore 2021-10-02
```

As simple as that.

## 3. ADVANCE USAGE: Code Development (SQL Routines)

You must code your data structures and initial data scripts in the SQL file with this naming conventions:

```bash
FOLDER
  ├── routines (directory)
  ├── 1-structure.sql (file)
  ├── 2-data.sql (file)
  └── db.conf (file)
```

If you doesn't have a `db.conf` file, you can make it by command `pg-execute generate-config`, and edit the content within.

```bash
  db_host = your_database_hostname
  db_port = your_database_port
  db_user = your_username
  db_pass = your_password
  db_name = your_database_name
```

Every Stored Procedures and/or Stored function could be placed inside the `routines` sub-folder. Use the file extension `.sql`.
The `pg-execute routines` will execute ALL OF `*.sql` files inside those sub-folder and implemented to your database.


## 4. USAGE EXAMPLES

```bash
cd /path/to/your/folder
pg-execute init                               # this will create database, user & grant privileges automatically (this will drop everything!)

pg-execute backup                             # this will dump your database into *.sql that'll be generated on the timestamp-based-name subfolder
pg-execute backup 7z                          # alternate backup, which generate a *.7z file (maximum compression)
pg-execute restore backup-20150101.073059     # this will restore the previous backup in the folder 'backup-20150101.073059'
pg-execute restore backup-20150101.073059.7z  # alternate restore, which will load the backup from *.7z file generated from previous backup

pg-execute migrate                            # this will be drop/re-create your database and refill the schema (including: views, routines and triggers) + data
pg-execute routines                           # this will be re-create ONLY the files under the 'routines' folder
pg-execute "SELECT * FROM some_table"         # this will be execute the specified queries and output the result to screen

pg-execute generate-config                    # this will generate the db.conf (if not exists)
pg-execute show-config                        # this will display the db.conf values
pg-execute login                              # this will login into CLI Mode of MySQL/MariaDB database console

pg-execute -v                                 # display the program version
pg-execute self-update                        # update the program

pg-execute help                               # display this inline help
```


# ENJOY!
