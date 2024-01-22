Certainly! Below are sample `README.md` files for each of the three methods: YUM package manager, .zip file extraction, and source compilation using `configure` and `make` commands.

### Method 1: YUM Package Manager

#### README.md

**Installing Nginx on RHEL using YUM Package Manager**

1. **Update System:**
    ```bash
    sudo yum update
    ```

2. **Install Nginx:**
    ```bash
    sudo yum install nginx
    ```

3. **Start Nginx:**
    ```bash
    sudo systemctl start nginx
    ```

4. **Enable Autostart on Boot:**
    ```bash
    sudo systemctl enable nginx
    ```

5. **Verify Installation:**
    Open a web browser and go to `http://your_server_ip`. You should see the default Nginx welcome page.

---

### Method 2: .zip File Extraction

#### README.md

**Installing Nginx on RHEL using .zip File**

1. **Download Nginx:**
    ```bash
    wget https://nginx.org/download/nginx-x.x.x.zip
    ```

2. **Install Unzip (if not installed):**
    ```bash
    sudo yum install unzip
    ```

3. **Extract .zip File:**
    ```bash
    unzip nginx-x.x.x.zip
    ```

4. **Move Files to Installation Directory:**
    ```bash
    sudo mv nginx-x.x.x /usr/local/nginx
    ```

5. **Start Nginx:**
    ```bash
    /usr/local/nginx/sbin/nginx
    ```

6. **Verify Installation:**
    Open a web browser and go to `http://your_server_ip`. You should see the default Nginx welcome page.

7. **Optional: Create systemd Service:**
    Follow the instructions in the [optional section](#method-2-using-zip-file) to create a systemd service.

---

### Method 3: Source Compilation with `configure` and `make`

#### README.md

**Installing Nginx on RHEL from Source Code**

1. **Install Dependencies:**
    ```bash
    sudo yum groupinstall "Development Tools"
    sudo yum install pcre-devel zlib-devel openssl-devel
    ```

2. **Download and Extract Nginx Source Code:**
    ```bash
    wget https://nginx.org/download/nginx-x.x.x.tar.gz
    tar -zxvf nginx-x.x.x.tar.gz
    cd nginx-x.x.x
    ```

3. **Configure Nginx:**
    ```bash
    ./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_v2_module
    ```

4. **Compile Source Code:**
    ```bash
    make
    ```

5. **Install Nginx:**
    ```bash
    sudo make install
    ```

6. **Start Nginx:**
    ```bash
    /usr/local/nginx/sbin/nginx
    ```

7. **Verify Installation:**
    Open a web browser and go to `http://your_server_ip`. You should see the default Nginx welcome page.

8. **Optional: Configure systemd Service:**
    Follow the instructions in the [optional section](#method-3-using-configure-and-make-commands) to create a systemd service.

Feel free to customize these README files based on your specific preferences or provide additional information as needed.
