# iris-sys-recs-2026

# Task1

Fixed the error generated due to `activesupport` and `activerecord` version issue. Just commented them so ruby manages them automatically.

![alt text](<Screenshot 2026-02-12 at 5.31.23 PM.png>)

# Task2

Changes made in `database.yml`:
* `socket: /var/run/mysqld/mysqld.sock` to `host: mysql-db`
* since the databse is hosted by docker container named `mysql-db` not in the host machine

Create a network `iris-network`

Command to run the sql:

```bash
docker run -d \
  --name mysql-db \
  --platform linux/amd64 \
  --network iris-network \
  -e MYSQL_ROOT_PASSWORD=Gukesh12garry@ \
  mysql:5.7
```

![alt text](<Screenshot 2026-02-12 at 5.57.34 PM.png>)

Command to run the app:

Before that had to build again since we changed `database.yaml`.

```bash
docker run -d \
  --name rails-app \
  --network iris-network \
  -p 8080:3000 \
  iris
```

add then migrated the database create database and tables.

```bash
docker exec rails-app bin/rails db:create db:migrate
```

![alt text](<Screenshot 2026-02-12 at 5.58.01 PM.png>)


# Task 3

Added the `nginx.conf` file and restarted the app container to not expose the port 8080.

now the app is accessed from the url `localhost` since it proxies it to `rails_app` which set to `rails_app:3000` which is the docker container name of the app.

![alt text](<Screenshot 2026-02-12 at 6.28.52 PM.png>)
