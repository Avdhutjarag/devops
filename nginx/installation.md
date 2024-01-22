Certainly! Here are the responses for all three methods:

### Method 1: YUM Package Manager

**Installing Nginx on RHEL using YUM Package Manager**

1. **Update System:**
    ```bash
    sudo yum update
    ```

   - Output:
     ```
     [sudo] password for user:
     ...
     Complete!
     ```

2. **Install Nginx:**
    ```bash
    sudo yum install nginx
    ```

   - Output:
     ```
     Dependencies Resolved

     ================================================================================
      Package           Arch          Version               Repository        Size
     ================================================================================
     Installing:
      nginx             x86_64        1:1.20.0-1.el8        AppStream        570 k

     Transaction Summary
     ================================================================================
     Install  1 Package

     Total download size: 570 k
     Installed size: 1.6 M
     ...
     ```

3. **Start Nginx:**
    ```bash
    sudo systemctl start nginx
    ```

   - Output:
     ```
     ```

4. **Enable Autostart on Boot:**
    ```bash
    sudo systemctl enable nginx
    ```

   - Output:
     ```
     Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.
     ```

5. **Verify Installation:**
    Open a web browser and go to `http://your_server_ip`. You should see the default Nginx welcome page.

---

### Method 2: .zip File Extraction

**Installing Nginx on RHEL using .zip File**

1. **Download Nginx:**
    ```bash
    wget https://nginx.org/download/nginx-x.x.x.zip
    ```

   - Output:
     ```
     --2024-02-28 10:00:00--  https://nginx.org/download/nginx-x.x.x.zip
     ...
     ```

2. **Install Unzip (if not installed):**
    ```bash
    sudo yum install unzip
    ```

   - Output:
     ```
     Dependencies Resolved

     ================================================================================
      Package           Arch          Version               Repository        Size
     ================================================================================
     Installing:
      unzip             x86_64        6.0-43.el8            AppStream        208 k

     Transaction Summary
     ================================================================================
     Install  1 Package

     Total download size: 208 k
     Installed size: 317 k
     ...
     ```

3. **Extract .zip File:**
    ```bash
    unzip nginx-x.x.x.zip
    ```

   - Output:
     ```
     Archive:  nginx-x.x.x.zip
     ...

     ```

4. **Move Files to Installation Directory:**
    ```bash
    sudo mv nginx-x.x.x /usr/local/nginx
    ```

   - Output:
     ```
     ```

5. **Start Nginx:**
    ```bash
    /usr/local/nginx/sbin/nginx
    ```

   - Output:
     ```
     ```

6. **Verify Installation:**
    Open a web browser and go to `http://your_server_ip`. You should see the default Nginx welcome page.

7. **Optional: Create systemd Service:**
    Create a systemd service file for Nginx to manage it more effectively. Save the following content to `/etc/systemd/system/nginx.service`:
    ```ini
    [Unit]
    Description=The NGINX HTTP and reverse proxy server
    After=syslog.target network.target remote-fs.target nss-lookup.target

    [Service]
    Type=forking
    PIDFile=/usr/local/nginx/logs/nginx.pid
    ExecStartPre=/usr/local/nginx/sbin/nginx -t
    ExecStart=/usr/local/nginx/sbin/nginx
    ExecReload=/bin/kill -s HUP $MAINPID
    ExecStop=/bin/kill -s QUIT $MAINPID
    PrivateTmp=true

    [Install]
    WantedBy=multi-user.target
    ```
    Then, reload the systemd manager configuration:
    ```bash
    sudo systemctl daemon-reload
    ```

    Now, you can manage Nginx using `systemctl` commands:
    ```bash
    sudo systemctl start nginx
    sudo systemctl stop nginx
    sudo systemctl restart nginx
    sudo systemctl enable nginx
    ```

---

### Method 3: Source Compilation with `configure` and `make`

**Installing Nginx on RHEL from Source Code**

1. **Install Dependencies:**
    ```bash
    sudo yum groupinstall "Development Tools"
    sudo yum install pcre-devel zlib-devel openssl-devel
    ```

   - Output:
     ```
     ...
     ```

2. **Download and Extract Nginx Source Code:**
    ```bash
    wget https://nginx.org/download/nginx-x.x.x.tar.gz
    tar -zxvf nginx-x.x.x.tar.gz
    cd nginx-x.x.x
    ```

   - Output:
     ```
     --2024-02-28 10:10:00--  https://nginx.org/download/nginx-x.x.x.tar.gz
     ...
     ```

3. **Configure Nginx:**
    ```bash
    ./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_v2_module
    ```

   - Output:
     ```
     ...
     Configuration summary
     ...
     ```

4. **Compile Source Code:**
    ```bash
    make
    ```

   - Output:
     ```
     ...
     ```

5. **Install Nginx:**
    ```bash
    sudo make install
    ```

   - Output:
     ```
     ...
     ```

6. **Start Nginx:**
    ```bash
    /usr/local/nginx/sbin/nginx
    ```

   - Output:
     ```
     ```

7. **Verify Installation:**
    Open a web browser and go to `http://your_server_ip`. You should see the default Nginx welcome page.

8. **Optional: Configure systemd Service:**
    Follow the instructions in the [optional section](#method-3-using-configure-and-make-commands) to create a systemd service.

Feel free to customize these responses based on your specific preferences or provide additional information as needed.
