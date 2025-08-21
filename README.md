# 📖 Project Documentation StreamCast – Live Streaming Platform for Casino "Hollywood"

## Table of Contents
- [1. Introduction](#1-introduction)
- [2. System Architecture](#2-system-architecture)
  - [Main Components](#main-components)
  - [Architecture Diagram (Simplified)](#architecture-diagram-simplified)
- [3. User Flow](#3-user-flow)
- [4. Installation and Configuration](#4-installation-and-configuration)
  - [Prerequisites](#prerequisites)
  - [Backend](#backend)
  - [Frontend](#frontend)
  - [RTMP Server (Nginx)](#rtmp-server-nginx)
- [5. User Guide](#5-user-guide)

---

## 1. Introduction

This project is a **live streaming platform** designed for a casino.  
The system allows authenticated users to create live broadcasts, stream from OBS, view live streams on the website, and display configurable ads during the broadcast.

The goal is to provide a smooth and secure streaming experience by integrating authentication, stream management, and ad administration into a single system.

**Main Technologies:**

* **Frontend:** React  
* **Backend:** NestJS + PostgreSQL  
* **RTMP Server:** Nginx with RTMP module  
* **Infrastructure:** Dedicated VPS  
* **Streaming Client:** OBS Studio  

---

## 2. System Architecture

### Main Components

* **Frontend (React):**  
  Web interface that allows users to register, authenticate, create streams, and watch live content. It also includes the ads section.

* **Backend (NestJS + PostgreSQL):**  
  Handles authentication, stream creation and validation, and ad management. All user, stream, and ad data is stored in **PostgreSQL**.

* **RTMP Server (Nginx):**  
  Receives streams sent from OBS and validates the stream key with the backend before allowing publication.

* **VPS:**  
  Environment where all services are deployed (backend, frontend, and RTMP server).

### Architecture Diagram (Simplified)

```mermaid
flowchart LR
    User["User (Web/Browser)"] -->|HTTP/HTTPS| Frontend["Frontend (React)"]
    Frontend -->|API Requests| Backend["Backend (NestJS)"]
    Backend -->|Queries| DB[(PostgreSQL)]
    OBS["OBS Studio"] -->|RTMP Stream| RTMP["Nginx RTMP"]
    RTMP -->|on_publish Validate Key| Backend
...
---

## 3. User Flow

![Flow Diagram](/images/diagrama.jpg)

1. The user registers or logs in on the website.  
2. Creates a stream by entering a **name and description**.  
3. The system generates an **RTMP URL + stream key**.  
4. The user opens OBS and enters the provided configuration.  
5. When starting the stream, **Nginx RTMP** executes the `on_publish` hook, calling the backend to validate the key.  
6. If the key is valid, the stream starts and is displayed on the website.  
7. During viewing, if ads are configured, they appear according to their order and duration.  

---

## 4. Installation and Configuration

### Prerequisites

* Node.js (>= 18)  
* pnpm  
* PostgreSQL  
* Nginx with RTMP module  
* OBS Studio (for client streaming)  

### Backend  

For the complete backend documentation, click [here.](/BACKEND.md)

### Frontend  

For the complete frontend documentation, click [here.](/FRONTEND.md)

### RTMP Server (Nginx)  

For the complete RTMP server documentation and configurations, check [here.](/RTMP.md)

---

## 5. User Guide

1. Go to the website and log in.  
2. Create a new stream → obtain the stream key and URL.  
3. Configure OBS with the provided details.  
4. Start streaming on OBS → the stream will be displayed on the website.  
5. In the ads section, add ads with:  
   * Name  
   * Description  
   * File (image or video)  
   * Display order  
   * Duration  
