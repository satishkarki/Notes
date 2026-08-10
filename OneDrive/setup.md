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



