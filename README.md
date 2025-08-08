# 📘 PostgreSQL Server Setup Guide

Instructions for installing and configuring **PostgreSQL** on a server running **Ubuntu 24.04 or newer**.

---

## 🖥️ Configuring the Server

1. Create a VDS/VPS with **Ubuntu 24.04+**
2. Update the system:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
3. Install PostgreSQL:
   ```bash
   sudo apt install postgresql postgresql-contrib -y
   ```
4. Check if the PostgreSQL service is running:
   ```bash
   sudo systemctl status postgresql
   ```
5. Switch to the `postgres` user:
   ```bash
   sudo -i -u postgres
   ```
6. Launch PostgreSQL shell:
   ```bash
   psql
   ```

---

## 🗃️ Setting Up and Creating a Database

### 🛡️ (Optional) Grant Superuser Privileges

If you want to give your user full administrative rights (use with caution):

```sql
ALTER USER your_user WITH SUPERUSER;
```

You can verify with:

```sql
\du
```

The user should now show `Superuser` in the `Attributes` column.


Inside the PostgreSQL shell (`psql`):

```sql
CREATE DATABASE your_database_name;                -- Create a database
CREATE USER your_user WITH PASSWORD 'your_password';  -- Create a user
GRANT ALL PRIVILEGES ON DATABASE your_database_name TO your_user; -- Grant privileges
```

Then exit:

```sql
\q      -- Exit psql
```

Exit the `postgres` shell:

```bash
exit
```

---

## 🌐 Setting Up Network Access (Optional)

### 1. Edit `postgresql.conf` to allow remote connections:

```bash
sudo nano /etc/postgresql/YOUR_VERSION/main/postgresql.conf
```

Find this line:

```conf
#listen_addresses = 'localhost'
```

And change it to:

```conf
listen_addresses = '*'
```

> Or restrict to a specific IP, e.g. `listen_addresses = '127.0.0.1'`

---

### 2. Edit `pg_hba.conf` to allow authentication:

```bash
sudo nano /etc/postgresql/YOUR_VERSION/main/pg_hba.conf
```

Add one of the following lines at the end of the file:

```conf
# Allow all IPs (use with caution)
host    all             all             0.0.0.0/0               md5

# OR restrict by DB/user/IP:
host    your_db         your_user       your_host_ip           md5
```

---

### 3. Restart PostgreSQL to apply changes:

```bash
sudo systemctl restart postgresql
```

---

## ✅ Done!

You now have a working PostgreSQL server.

---

## 🧪 Test Remote Connection

From a remote machine:

```bash
psql -h your.server.ip -U your_user -d your_database_name
```

---

## 💡 Tips

- Replace `YOUR_VERSION` with your actual PostgreSQL version (e.g. `16`)
- Use strong passwords and consider using SSL for production environments
- Open port `5432` in your firewall if using UFW:
  ```bash
  sudo ufw allow 5432/tcp
  ```

---

## 📄 License

MIT License. Feel free to fork, modify, and use.

---

## 🙋‍♂️ Contributing

Pull requests are welcome! If you want to add examples (e.g. connecting with Python, Docker setup, backups), feel free to contribute.
