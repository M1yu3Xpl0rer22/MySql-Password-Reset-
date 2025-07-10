# 🔐 MySQL Root Password Recovery (Windows)

Forgot your MySQL `root` password? No worries — this guide walks you through resetting it safely using the **init-file** method on Windows, plus how to fix common errors step by step.

---

## 📌 Step-by-Step Guide

### ✅ Step 1: Stop MySQL Service
```bash
sc query state= all | findstr /I "mysql"
net stop MySQL80
Replace MySQL80 with your actual service name.

✅ Step 2: Create a Password Reset File
Open Notepad

Paste this:

sql
Copy
Edit
ALTER USER 'root'@'localhost' IDENTIFIED BY '12345';
Save as: C:\mysql-reset.sql

✅ Ensure the file extension is .sql, not .txt

✅ Step 3: Start MySQL with Init File
Run this command in Command Prompt as Administrator:

bash
Copy
Edit
mysqld --init-file="C:\\mysql-reset.sql" --console --datadir="C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Data"
✅ Step 4: Start MySQL Normally
Once the password is reset, stop the manual process (Ctrl + C), then restart the service:

bash
Copy
Edit
net start MySQL80
✅ Step 5: Log In with New Password
bash
Copy
Edit
mysql -u root -p
Enter the new password (e.g., 12345)

🧹 Step 6: Clean Up
Delete the reset file for security:

bash
Copy
Edit
del C:\mysql-reset.sql
❌ Common Errors & Fixes
<details> <summary>🔸 ERROR 1045 (28000): Access denied (using password: YES)</summary>
Cause: Wrong password
Fix: Follow this guide again to reset it using init-file

</details> <details> <summary>🔸 The service name is invalid</summary>
Cause: Wrong MySQL service name
Fix: Use:

bash
Copy
Edit
sc query state= all | findstr /I "mysql"
</details> <details> <summary>🔸 Can't create test file... Permission denied</summary>
Cause: No admin rights or incorrect datadir
Fix: Run CMD as Administrator and verify the data path.

</details> <details> <summary>🔸 Access denied (using password: NO)</summary>
Cause: You didn’t use the -p flag
Fix:

bash
Copy
Edit
mysql -u root -p
</details>
🏁 Done!
You’ve successfully reset the MySQL root password on Windows! 🎉

Author: YourNameHere
Last Updated: July 2025
MySQL Version: 8.0.x on Windows
