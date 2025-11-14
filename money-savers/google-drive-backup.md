## 💾 Automated Offsite Backup Strategy (VPS to Google Drive)

This guide outlines the steps to implement a secure, cost-saving, and automated offsite backup solution for your WordPress VPS using Google Drive storage (available via Gemini Pro / Google One subscription) and the command-line utility **`rclone`**.

### 🎯 Goal

Replace the paid Hostinger backup service ($12/month) with a free, automated system that stores encrypted backups directly on your personal Google Drive account, enhancing data security and redundancy.

---

### 1. ⚙️ Install and Configure rclone

**rclone** is a powerful utility for syncing files to cloud storage services. This step must be performed via SSH on your Hostinger VPS.

1.  **Install rclone:** Connect to your VPS via SSH and install the utility (commands vary by OS, e.g., `sudo apt install rclone` for Ubuntu/Debian).
2.  **Configure Google Drive Remote:** Run the setup command:
    ```bash
    rclone config
    ```
    Follow the prompts to create a new remote, select **Google Drive** as the storage type, and authorize your VPS by generating and pasting a token via your local browser. Name the remote something descriptive (e.g., `gdrive`).

### 2. 📝 Create the Backup Script (`backup.sh`)

Create a shell script that performs the necessary steps for data capture and transfer.

```bash
#!/bin/bash

# Define variables
DB_NAME="[YOUR_WP_DATABASE_NAME]"
DB_USER="[YOUR_WP_DATABASE_USER]"
DB_PASS="[YOUR_WP_DATABASE_PASSWORD]"
SITE_ROOT="/home/[site_user]/domains/[example.com/public_html](https://example.com/public_html)"
BACKUP_DIR="/root/backups"
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="wp_backup_$TIMESTAMP.tar.gz"
RCLONE_REMOTE="gdrive:VPS_Backups/example.com" # Target folder on your Google Drive

# 1. Create backup directory
mkdir -p $BACKUP_DIR

# 2. Dump and compress the database
mysqldump -u$DB_USER -p$DB_PASS $DB_NAME | gzip > $BACKUP_DIR/$DB_NAME.sql.gz

# 3. Archive all site files (Excluding unnecessary cache/backup files)
tar -czf $BACKUP_DIR/$BACKUP_FILE -C $SITE_ROOT . --exclude='wp-content/cache' --exclude='wp-content/backups'

# 4. Transfer to Google Drive using rclone
rclone copy $BACKUP_DIR $RCLONE_REMOTE --progress

# 5. Clean up local files (optional, but recommended)
rm -rf $BACKUP_DIR/*
