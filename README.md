# Pi-hole Docker Setup with Docker Compose

This project sets up Pi-hole, a network-wide ad blocker, using Docker Compose. The Pi-hole web interface password is stored in an `.env` file for security.

## Prerequisites

- Docker installed on your system.
- Docker Compose installed.

## Setup

### Step 1: Create an `.env` File

To secure the Pi-hole web interface with a password, you need to create an `.env` file in the same directory as your `docker-compose.yml` file. This file will contain your web interface password as an environment variable.

1. In the root directory of this project (where your `docker-compose.yml` is located), create a file named `.env`.

   ```bash
   touch .env
   ```

2. Open the `.env` file and add the following line, replacing `your_secure_password` with your desired password:

   ```bash
   WEBPASSWORD=your_secure_password
   ```

   Example:

   ```bash
   WEBPASSWORD=supersecretpassword
   ```

   This password will be used to log into the Pi-hole web admin interface.

### Step 2: Update the `docker-compose.yml` File

Make sure the `docker-compose.yml` file is configured to use the password from the `.env` file

### Step 3: Run the Pi-hole Service

Once the .env file is created and configured, you can start the Pi-hole service using Docker Compose.

In the terminal, navigate to the directory containing your docker-compose.yml file and run:

```bash
docker-compose up -d
```

This command will:

Pull the latest Pi-hole Docker image.
Start the Pi-hole container.

Detach from the terminal (run in the background).
To check if the container is running, you can use:

```bash
docker ps
```

You should see a container named pihole in the list.

### Step 4: Access the Pi-hole Web Interface

Once Pi-hole is up and running, you can access the web interface by navigating to:

```arduino
http://<your-raspberry-pi-ip>/admin
```

Log in using the password you set in the .env file.

Stopping the Pi-hole Service
To stop the Pi-hole service, run the following command:

```bash
docker-compose down
```

This will stop and remove the container, but your configuration and data will persist because it is stored in volumes.

### Restarting the Pi-hole Service

To restart the Pi-hole service, simply run:

```bash
docker-compose up -d
```

### Troubleshooting

Cannot access the web interface: Ensure the container is running by checking with docker ps. Also, ensure you are using the correct IP address of your Raspberry Pi.

Forgot the password? You can reset the password by running the following command inside the running container:

```bash
docker exec -it pihole pihole -a -p
```

This will prompt you to set a new password for the web interface.

### License

This project is licensed under the MIT License.

#### Key Points:

- The `.env` file allows you to keep sensitive information like passwords out of your version-controlled `docker-compose.yml` file.
- Instructions are provided for starting, stopping, and accessing the Pi-hole service.
