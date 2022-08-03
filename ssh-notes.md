1. Use ssh-copy-id to copy public key
    ```bash
    ssh-copy-id -id you_public_key user@host
    ```

2. Ssh timeout solution
    ```bash
    # Add config on client
    touch ~/.ssh/config
    chmod 600 ~/.ssh/config
    echo "ServerAliveInterval 600" >> ~/.ssh/config 
    ```

    ```bash
    # For all host
    Host *
    ServerAliveInterval 600
    ```

3. Open server ssh config file: `sshd_config`
    ```bash
    vim /etc/ssh/sshd_config

    # Update the following parameters
    ClientAliveInterval 200
    ClientAliveCountMax  3
    ```