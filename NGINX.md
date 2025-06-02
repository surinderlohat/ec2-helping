Sure! Here’s a handy list of common **NGINX commands** you’ll use on your EC2 (or any Linux) server, mostly using `systemctl` and some direct commands:

---

## Using systemd (`systemctl`)

* **Start NGINX service**

  ```bash
  sudo systemctl start nginx
  ```

* **Stop NGINX service**

  ```bash
  sudo systemctl stop nginx
  ```

* **Restart NGINX service** (stop + start)

  ```bash
  sudo systemctl restart nginx
  ```

* **Reload NGINX config without downtime**

  ```bash
  sudo systemctl reload nginx
  ```

* **Check NGINX service status**

  ```bash
  sudo systemctl status nginx
  ```

* **Enable NGINX to start on boot**

  ```bash
  sudo systemctl enable nginx
  ```

* **Disable NGINX autostart on boot**

  ```bash
  sudo systemctl disable nginx
  ```

---

## Direct NGINX commands (without systemd)

* **Test NGINX configuration syntax**

  ```bash
  sudo nginx -t
  ```

* **Start NGINX manually (foreground)**

  ```bash
  sudo nginx
  ```

* **Stop NGINX gracefully**

  ```bash
  sudo nginx -s quit
  ```

* **Reload config gracefully (send signal)**

  ```bash
  sudo nginx -s reload
  ```

---

### Notes:

* Prefer using `systemctl` on systems with systemd (like Amazon Linux 2, Ubuntu, CentOS 7+).
* Use `nginx -t` **before** reload/restart to check config syntax.
* `reload` applies config changes without dropping connections.
* `restart` fully stops and starts the service, causing a brief downtime.

---

To run **NGINX** service using a **specific config file** (not the default `/etc/nginx/nginx.conf`), you have a couple of options depending on whether you use `systemctl` or run it manually.

---

### 1. Run NGINX manually with a specific config file

```bash
sudo nginx -c /path/to/your/custom-nginx.conf
```

* This starts NGINX with the config file you specify.
* To reload or stop, you may need to specify the same config file again, e.g.:

```bash
sudo nginx -c /path/to/your/custom-nginx.conf -s reload
sudo nginx -c /path/to/your/custom-nginx.conf -s quit
```

---

### 2. Run NGINX as a **systemd service** with a specific config file

The systemd service for NGINX usually uses the default config file. To override:

#### Option A: Edit the systemd service file temporarily

```bash
sudo systemctl edit nginx
```

This opens an override file. Add:

```ini
[Service]
ExecStart=
ExecStart=/usr/sbin/nginx -c /path/to/your/custom-nginx.conf
```

Then reload systemd and restart nginx:

```bash
sudo systemctl daemon-reload
sudo systemctl restart nginx
```

---

#### Option B: Create a custom systemd service file

Copy the default service file and modify the config path:

```bash
sudo cp /usr/lib/systemd/system/nginx.service /etc/systemd/system/nginx-custom.service
sudo nano /etc/systemd/system/nginx-custom.service
```

Change the `ExecStart` line to:

```
ExecStart=/usr/sbin/nginx -c /path/to/your/custom-nginx.conf
```

Then:

```bash
sudo systemctl daemon-reload
sudo systemctl start nginx-custom
sudo systemctl status nginx-custom
```

---

### Summary

* For **quick test or manual run**: `sudo nginx -c /your/config.conf`
* For **systemd service**, override `ExecStart` to add `-c /your/config.conf`


