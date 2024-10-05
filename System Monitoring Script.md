## System Monitoring Script

```bash
#!/bin/bash

threshold=90
recipient="example@gmail.com"

# Monitor CPU usage and trigger alert if threshold is exceeded
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}' | cut -d. -f1)

if [ "$cpu_usage" -gt "$threshold" ]; then
  echo "High CPU usage detected: $cpu_usage%" | mail -s "CPU Usage Alert" "$recipient"
fi
```

### Explanation:

1. **`threshold=90`**: This sets the CPU usage threshold to 90%. If CPU usage exceeds this, an alert will be triggered.

2. **`recipient="example@gmail.com"`**: This sets the recipient email address where the alert will be sent. You can replace `"example@gmail.com"` with any email address you'd like to send alerts to.

3. **`cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4}' | cut -d. -f1)`**: 
   - `top -bn1`: This runs the `top` command in batch mode (`-bn1`) and captures system statistics one time (`n1`).
   - `grep "Cpu(s)"`: This filters the line containing CPU usage statistics.
   - `awk '{print $2 + $4}'`: This extracts the "user" CPU usage (`$2`) and "system" CPU usage (`$4`) and sums them to get total CPU usage.
   - `cut -d. -f1`: This cuts off the decimal part of the CPU usage to get an integer (whole number).

4. **`if [ "$cpu_usage" -gt "$threshold" ]; then`**: This checks if the current CPU usage (`$cpu_usage`) is greater than the threshold (90%).

5. **`echo "High CPU usage detected: $cpu_usage%" | mail -s "CPU Usage Alert" "$recipient"`**: 
   - This sends an email using the `mail` command.
   - `echo "High CPU usage detected: $cpu_usage%"`: This generates the body of the email, which will contain a message saying "High CPU usage detected" and the current CPU usage percentage.
   - `| mail -s "CPU Usage Alert" "$recipient"`: The `mail` command sends an email with the subject "CPU Usage Alert" to the recipient email address (`$recipient`).

### Requirements:
- The `mail` command should be installed and properly configured to send emails.
- Ensure the system has access to an SMTP server or email service to send out the notification. For testing on Linux, you can use utilities like `ssmtp` or `sendmail` to set this up.

When the CPU usage goes above 90%, the script will send an alert email to the specified recipient (`example@gmail.com`).
