# 🔐 MySQL Root Password Recovery (Windows)

Forgot your MySQL `root` password? This guide will help you reset it safely using the **init-file** method on **Windows** and resolve common errors step by step.

---

## ✅ Step 1: Stop MySQL Service

Open **Command Prompt as Administrator** and run:

```bash
sc query state= all | findstr /I "mysql"
net stop MySQL80
```

> 🔁 Replace `MySQL80` with your actual service name from the first command.

---

## ✅ Step 2: Create a Password Reset File

1. Open **Notepad**
2. Paste the following SQL command:

   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'sample password';
   ```
3. Save it as: `C:\mysql-reset.sql`

> ✅ Make sure the file extension is `.sql`, **not `.txt`**

---

## ✅ Step 3: Start MySQL with Init File

Run this command in **Command Prompt as Administrator**:

```bash
mysqld --init-file="C:\\mysql-reset.sql" --console --datadir="C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Data"
```

---

## ✅ Step 4: Start MySQL Normally

After the password reset:

* Press `Ctrl + C` to stop the manual process
* Then restart MySQL service:

```bash
net start MySQL80
```

---

## ✅ Step 5: Log In with New Password

```bash
mysql -u root -p
```

> Enter the new password: `12345`

---

## 🧹 Step 6: Clean Up

Delete the reset SQL file for security:

```bash
del C:\mysql-reset.sql
```

---

## ❌ Common Errors & Fixes

<details>
<summary>🔸 ERROR 1045 (28000): Access denied (using password: YES)</summary>

**Cause:** Wrong password  
**Fix:** Follow this guide again to reset using the init-file method.

</details>

<details>
<summary>🔸 The service name is invalid</summary>

**Cause:** Incorrect MySQL service name  
**Fix:** Use:

```bash
sc query state= all | findstr /I "mysql"
```

to find the correct name.

</details>

<details>
<summary>🔸 Can't create test file... Permission denied</summary>

**Cause:** No admin rights or incorrect `datadir`  
**Fix:** Run CMD as Administrator and verify the data directory path.

</details>

<details>
<summary>🔸 Access denied (using password: NO)</summary>

**Cause:** You didn’t use the `-p` flag  
**Fix:**

```bash
mysql -u root -p
```

</details>

---

## 🏁 Done!

🎉 You’ve successfully reset the MySQL root password on Windows!

---

**Author:** M1yu3Xpl0rer22
**Last Updated:** July 2025  
**MySQL Version:** 8.0.x on Windows
