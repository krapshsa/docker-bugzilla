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
