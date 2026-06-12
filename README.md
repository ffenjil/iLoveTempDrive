<div align="center">

<img src="https://cdn.discordapp.com/attachments/1482773726608097361/1514967686189289512/ilovetempdrive.png?ex=6a2d4b1b&is=6a2bf99b&hm=147618a545038411ee4d2fd379f21139eeed86be1d0547de59284e831a811aa5" alt="iLoveTempDrive Banner" width="100%" />

<br/>
<br/>

[![Live](https://img.shields.io/badge/Live-ilovetempdrive.xyz-ba0914?style=for-the-badge&logo=google-chrome&logoColor=white)](https://ilovetempdrive.xyz)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)](https://mongodb.com)
[![License](https://img.shields.io/badge/License-Proprietary-ba0914?style=for-the-badge)](#)

**Upload files. Create a private temporary drive. Share instantly.**
<br/>
No accounts. No tracking. Everything self-destructs in 5 hours.

<br/>

[Try It Live](https://ilovetempdrive.xyz) · [Status Page](https://ilovetempdrive.xyz/status)

</div>

---

## What is iLoveTempDrive?

iLoveTempDrive is a **zero-trace temporary file storage and instant sharing platform**. Users can upload files up to 1 GB per session, share them via a unique room link, and everything gets permanently deleted after 5 hours. No sign-ups, no persistent accounts, no recovery possible.

It was born from a simple frustration: every time you need to print a document, you send it to yourself on WhatsApp, open it on another device, and download. Convenient, but not secure. Sensitive files like ID proofs, bank statements, and medical records end up floating around in messaging apps forever.

iLoveTempDrive fixes that. Upload, share, and it's gone.

<br/>

## Features

<table>
<tr>
<td width="50%">

### Core
- **Zero-Trace Design** - No accounts, no cookies for tracking, no persistent data
- **5-Hour Auto-Destruct** - Rooms and all files are permanently purged after 5 hours
- **1 GB Per Session** - Upload multiple files up to 1 GB total per room
- **Password-Protected Rooms** - Every room is locked with a unique password
- **Multi-Device Access** - Up to 5 devices can join a single room simultaneously

</td>
<td width="50%">

### Technical
- **Direct Browser Uploads** - Files stream directly to object storage via presigned URLs
- **Multipart Uploads** - Large files are split into chunks and uploaded in parallel
- **Multi-Node Storage** - Automatic overflow from Cloudflare R2 to Tencent COS to AWS S3
- **CloudFront CDN** - Downloads served via signed CloudFront URLs for speed
- **Real-Time Status** - Live health monitoring dashboard at `/status`

</td>
</tr>
</table>

## How It Works

1. **Create a Room** - User lands on the homepage, selects files, and clicks upload
2. **Room Generated** - Server creates a room with a unique ID, password, and 5-hour expiry timer
3. **Direct Upload** - Files are uploaded directly from the browser to object storage using presigned URLs
4. **Node Selection** - The server picks the best storage node based on available capacity, automatically overflowing to backup nodes when the primary is full
5. **Share the Link** - The room URL and password are shared with others who can join and download files
6. **Auto-Purge** - A background cleanup thread continuously checks for expired rooms and permanently deletes all associated files from storage

<br/>

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Backend** | Python + Flask | Web framework and API server |
| **Server** | Gunicorn | Production WSGI server with multi-threading |
| **Database** | MongoDB (Atlas) | Room metadata, file records, analytics |
| **Primary Storage** | Cloudflare R2 | S3-compatible object storage (zero egress fees) |
| **Secondary Storage** | Tencent COS | Fallback overflow node |
| **Tertiary Storage** | AWS S3 | Additional overflow with CloudFront CDN for downloads |
| **CDN** | AWS CloudFront | Signed URL downloads for S3-stored files |
| **Reverse Proxy** | Apache | TLS termination, HTTP/2, request routing |
| **Styling** | Tailwind CSS | Utility-first CSS framework |
| **Frontend** | Vanilla JavaScript | Direct upload client with multipart chunking |
<br/>

## Security

- **CSRF Protection** - All forms and API calls are protected with CSRF tokens
- **Rate Limiting** - Per-IP rate limits on room creation, joining, and API calls
- **Brute Force Protection** - IP lockout after repeated failed room join attempts
- **Secure Sessions** - HttpOnly, SameSite=Lax, Secure (in production) cookies
- **No Persistent Data** - Zero redundant backups; once purged, recovery is impossible
- **Password Hashing** - Room passwords are hashed with Werkzeug's secure hasher
- **Signed Downloads** - CloudFront and S3 downloads use time-limited signed URLs


<br/>

## Use It Live

iLoveTempDrive is live and free to use at:

<div align="center">

### [https://ilovetempdrive.xyz](https://ilovetempdrive.xyz)

</div>

No sign-up required. Just open the site, drag your files, and share.

<br/>

## Contributors

<table>
<tr>
<td align="center">
<a href="https://github.com/mainaloohun">
<img src="https://github.com/mainaloohun.png" width="100px;" alt="Asad" style="border-radius: 50%;"/>
<br/>
<sub><b>Asad</b></sub>
</a>
<br/>
<sub>Ideator & Backend Developer</sub>
<br/>
<sub>Proposed the zero-trace concept and architected the backend infrastructure</sub>
</td>
<td align="center">
<a href="https://github.com/ffenjil">
<img src="https://github.com/ffenjil.png" width="100px;" alt="Jil" style="border-radius: 50%;"/>
<br/>
<sub><b>Jil</b></sub>
</a>
<br/>
<sub>Designer & Developer</sub>
<br/>
<sub>Designed the UI from the ground up and brought the visual identity to life</sub>
</td>
</tr>
</table>

<br/>

---

<div align="center">

**Made with :heart: by [Asad](https://github.com/mainaloohun) & [Jil](https://github.com/ffenjil)**

<br/>

<sub>iLoveTempDrive &copy; 2026. All rights reserved.</sub>

</div>
