# StreamCast - RTMP Docker

![Docker](https://img.shields.io/badge/Docker-303030?style=flat-square&logo=docker&logoColor=2496ED)
![Nginx](https://img.shields.io/badge/Nginx-303030?style=flat-square&logo=nginx&logoColor=009639)
![RTMP](https://img.shields.io/badge/RTMP-303030?style=flat-square&logo=nginx&logoColor=FF4500)

A Dockerized RTMP (Real-Time Messaging Protocol) server setup using Nginx, designed to facilitate live video streaming for the StreamCast platform. This setup provides a robust and easily deployable solution for ingesting and serving live streams.

## Features

- **Dockerized Environment**: Easily deployable and scalable using Docker and Docker Compose.
- **Nginx RTMP Module**: Configured with the Nginx RTMP module for efficient live stream handling.
- **HLS Support**: Supports HTTP Live Streaming (HLS) for broader compatibility with various devices and players.
- **Simple Setup**: Quick and straightforward setup process for local development and testing.

## Getting Started

Follow these instructions to set up and run the RTMP server locally.

### Prerequisites

Make sure you have the following installed on your system:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Installation

1.  Clone the repository (if you haven't already):

    ```bash
    git clone https://github.com/your-username/stream-cast.git
    cd stream-cast/docker-rtmp
    ```

2.  Copy `.env.sample` to `.env` (if it exists and is needed for configuration):

    ```bash
    cp .env.sample .env
    ```

3.  Start the Docker containers:

    ```bash
    docker-compose up -d
    ```

4.  To check see in a browser

    ```bash
    firefox index.html
    ```

### Usage

Once the containers are running, you can:

- **Push RTMP Stream**: Push your live stream to `rtmp://localhost/live/STREAM_KEY` (replace `STREAM_KEY` with your desired stream key).
- **View HLS Stream**: Access the HLS stream at `http://localhost:8080/hls/STREAM_KEY.m3u8`.
- **View Live Page**: Open `http://localhost:8080/index.html` in your browser to see a basic live stream player.

### Stopping the Server

To stop and remove the Docker containers:

```bash
docker-compose down
```
## INSTALLATION GUIDE
Access the guide to environment variables and parameter configuration with nginx.
[Guide](/INSTALLATION.md)
## Project Structure

```bash
.
├── 📄 .env.sample             # Example environment variables
├── 📄 .gitignore              # Files and directories to ignore in Git
├── 📄 docker-compose.yml      # Docker Compose setup for Nginx RTMP
├── 📄 index.html              # Simple HTML page to view the stream
├── 📄 README.md               # Project README file
├── 📁 hls/                    # Directory for HLS segments
│   └── 📄 .gitkeep
└── 📁 nginx/                  # Nginx configuration
    └── 📄 nginx.conf.template # Nginx RTMP configuration template
```

## License

This project is UNLICENSED. Please refer to the `package.json` for more details. (Note: Consider adding a specific license for open-source projects.)