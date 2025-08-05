---
title : "AWS Services In The Lab"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---


## Backend
### Elastic Beanstalk
- Hosts the **Spring Boot backend app** (`MusicApp.jar`) built with **Java 21 + Maven**.  
- Deployment flow:  
  1. Code → `mvn clean package` → generates `.jar` in `target/`.  
  2. `Procfile` runs the `.jar` on EB instances.  
  3. `eb deploy` uploads and provisions the app.  
- Environment variables (`DB_URL`, `DB_USER`, `DB_PASS`, Gmail SMTP creds, etc.) are set via `eb setenv`.  
- Provides **load balancing + auto-scaling** so the backend scales with user demand.  

### S3
- Bucket is created for **file storage** (future usage in music app).  
- Planned use cases:  
  - Store **music files** uploaded by artists.  
  - Store **album covers / profile images**.  
  - Serve files directly to frontend with **pre-signed URLs** (secure download).  
- Backend can generate S3 pre-signed URLs for controlled access.  

### Aurora and RDS
- Currently using **Amazon RDS (MySQL 8.0)** in `ap-southeast-2`.  
  - Example connection:  
    ```
    spring.datasource.url=jdbc:mysql://musicapp-db.c7a64kgsc9iz.ap-southeast-2.rds.amazonaws.com:3306/music_app
    spring.datasource.username=admin
    spring.datasource.password=******
    ```
- Stores:  
  - **User accounts** (id, email, username, password hash).  
  - **Profiles** (full name, phone, etc.).  
  - **Password reset codes & tokens**.  
  - Will later hold **music metadata (songs, playlists, likes, etc.)**.  


---

## Frontend

### Amplify
- Integrated into **Android frontend (Java)** with **Amplify Android v2.23.0**.  
- **Amplify Plugins in `MyApplication`:**  
  - `Auth` → Cognito User Pools for **sign-up / login / token refresh**.  
  - `API` (configured, but backend still uses Retrofit for REST).  
- **How it works in your app now:**  
  1. User logs in via Amplify → Cognito issues **ID + access tokens**.  
  2. Retrofit APIs use these tokens (JWT) to call backend endpoints on Elastic Beanstalk.  
  3. Backend validates the token, processes request, and queries RDS.  
- Amplify also manages **session persistence** (so users stay logged in after reopening the app).  


---

## Flow Summary
- **Android App (Amplify Cognito)** → Authenticates user.  
- **App uses Retrofit APIs** → Calls Spring Boot backend hosted on **Elastic Beanstalk**.  
- **Backend talks to RDS** (user + app data) and **S3** (media storage).  
  
