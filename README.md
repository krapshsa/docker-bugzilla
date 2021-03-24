### 0. Create volume folder for bugzilla and database
```
bash init.sh
```

### 1. start & enter bugzilla container shell
```
docker-compose up -d
docker-compose exec bugzilla /bin/bash
```

### 2. Create `localconfig`
```
cd /var/www/html/bugzilla
perl checksetup.pl
```

### 3. Configure `localconfig`
```
$webservergroup = 'www-data';
$db_driver = 'mysql';
$db_name = 'bugs';
$db_user = 'bugz';
$db_pass = 'bugpw';
$db_port = 3306;
```

### 4. Install (Interactive)
```
perl checksetup.pl
```

---

Convert from Bugzilla to Redmine:

### 0. Login into redmine with admin / admin and change password

### 1. Init some propeties for new installation redmine
```
docker-compose exec redmine rake redmine:load_default_data
```

### 2. copy migrate script to redmine
```
docker cp migrate_from_bugzilla.rake <redmine container name>:/usr/src/redmine/lib/tasks/
```

### 3. run script in redmine
```
docker-compose exec redmine rake redmine:migrate_from_bugzilla
```
