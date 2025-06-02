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

If you want a script or aliases for these, I can help set that up too!
