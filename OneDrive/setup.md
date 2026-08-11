# OneDrive setup in Fedora

```shell
# Install
sudo dnf install onedrive
```
```bash
# Run the client for the first time in your terminal
onedrive 
```
Authorize the account and then back in terminal

```bash
# Test the sync with a dry run
onedrive --synchronize --verbose --dry-run
```

```bash
# Start full sync
onedrive --syn
```

```bash
# Enable background sync so it runs automatically
systemctl --user enable --now onedrive
```
To view the live changes in OneDrive from Terminal
```bash
journalctl --user -u onedrive -f
```
* `journalctl`: The Linux utility used to query and view system logs.
* `--user`: Filters the logs to show only services running under your personal user account.
* `-u onedrive`: Limits the output to a specific unit (service), which in this case is onedrive.
* `-f`: Stands for "follow." Instead of showing a static list and exiting, it keeps the terminal window open and appends new log lines the exact second they happen.



