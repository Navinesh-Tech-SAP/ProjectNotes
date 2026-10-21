**Disk Space Monitoring and Email Alert System**

**Headline:** An automated C# application that monitors Windows and Linux disk usage, records daily logs, and sends email alerts when usage exceeds configured thresholds.

**Header: Purpose of This Code**
- To monitor disk space on Windows drives and Linux filesystems and identify usage exceeding defined limits.
- To automate email notifications and maintain date-wise log files for monitoring, troubleshooting, and auditing.

**Packages Used**
- System.IO – Disk information and file logging.
- System.Configuration – Reads application settings from App.config.
- System.Net.Mail and System.Net – Sends email alerts using SMTP.
- Renci.SshNet (SSH.NET) – Connects to the Linux server and executes disk usage commands.

**Windows Flow**
1. Reads drive letters and the warning threshold from App.config.
2. Checks total, used, and free disk space for each configured drive.
3. Logs disk usage and identifies drives exceeding the 50% threshold.
4. Sends an email alert when required and records the results in daily log files.

**Linux Flow**
1. Reads the Linux host IP, SSH port, username, password, and warning threshold from App.config.
2. Connects to the Linux server through SSH and executes the disk usage command.
3. Parses filesystem usage and identifies mount points exceeding the 20% threshold.
4. Sends an email alert when required and records disk usage and errors in daily log files.

**Result**
- The application automatically monitors Windows and Linux disk usage and sends email alerts when configured thresholds are exceeded.
- Date-wise log files are maintained in D:\Argit\Logs\DiskSpaceCheckLogs for tracking monitoring results, warnings, and errors.
