<div align="center">

<img src="https://cdn.discordapp.com/attachments/1482773726608097361/1514967686189289512/ilovetempdrive.png?ex=6a2d4b1b&is=6a2bf99b&hm=147618a545038411ee4d2fd379f21139eeed86be1d0547de59284e831a811aa5" alt="iLoveTempDrive Logo" width="130" />

# iLoveTempDrive

### Zero-Trace Temporary File Storage & Instant Sharing

No registration. No tracking. Auto-destructs after 5 hours.

<br/>

[![Live Website](https://img.shields.io/badge/Live-ilovetempdrive.xyz-ba0914?style=for-the-badge&logo=google-chrome&logoColor=white)](https://ilovetempdrive.xyz)
[![Storage](https://img.shields.io/badge/Storage-Multi--Node-0d1117?style=for-the-badge&logo=cloudflare&logoColor=F38020)](#)
[![Security](https://img.shields.io/badge/Security-Zero--Trace-success?style=for-the-badge&logo=dependabot&logoColor=white)](#)

<br/>

[Try It Live](https://ilovetempdrive.xyz) • [Status Page](https://ilovetempdrive.xyz/status)

</div>

<hr style="border: 0; height: 1px; background: linear-gradient(to right, rgba(0,0,0,0), #ba0914, rgba(0,0,0,0));" />

## <img src="https://img.shields.io/badge/-Info-ba0914?style=flat-square&logo=gitbook&logoColor=white" height="20" align="absmiddle" /> What is iLoveTempDrive?

iLoveTempDrive is a **zero-trace temporary file storage and instant sharing platform**. Users can upload files up to 1 GB per session, share them via a unique room link, and everything gets permanently deleted after 5 hours. No sign-ups, no persistent accounts, no recovery possible.

> **The Backstory**
> It was born from a simple frustration: every time you need to print a document, you send it to yourself on WhatsApp, open it on another device, and download. Convenient, but not secure. Sensitive files like ID proofs, bank statements, and medical records end up floating around in messaging apps forever.
>
> iLoveTempDrive fixes that: upload, share, and it is gone.

<br/>

## <img src="https://img.shields.io/badge/-Features-ba0914?style=flat-square&logo=google-keep&logoColor=white" height="20" align="absmiddle" /> Features

<table width="100%">
<tr>
<td width="50%" valign="top">

### <img src="https://img.shields.io/badge/-Core-ba0914?style=flat-square&logo=shield&logoColor=white" height="18" align="absmiddle" /> Core Experience
* **Zero-Trace Design** : No accounts, no tracking cookies, no persistent data
* **5-Hour Auto-Destruct** : Rooms and all files are permanently purged after 5 hours
* **1 GB Per Session** : Upload multiple files up to 1 GB total per room
* **Password-Protected Rooms** : Every room is locked with a unique password
* **Multi-Device Access** : Up to 5 devices can join a single room simultaneously

</td>
<td width="50%" valign="top">

### <img src="https://img.shields.io/badge/-Specs-ba0914?style=flat-square&logo=probot&logoColor=white" height="18" align="absmiddle" /> Under The Hood
* **Direct Browser Uploads** : Files stream directly to object storage via presigned URLs
* **Multipart Chunking** : Large files are split into chunks and uploaded in parallel
* **Multi-Node Fallback** : Auto-overflow from Cloudflare R2 to Tencent COS to AWS S3
* **CloudFront CDN** : Downloads served via signed CloudFront URLs for fast delivery
* **Real-Time Status** : Live health monitoring dashboard at `/status`

</td>
</tr>
</table>

<br/>

## <img src="https://img.shields.io/badge/-Workflow-ba0914?style=flat-square&logo=git&logoColor=white" height="20" align="absmiddle" /> How It Works

```mermaid
graph TD
    A[Homepage: Select Files] -->|Click Upload| B(Server creates secure room)
    B -->|Generates Room ID & password| C[Direct upload from browser to object storage]
    C -->|Auto-selects optimal storage node| D{Primary R2 capacity?}
    D -->|Available| E[R2 Node]
    D -->|Full| F[Tencent COS Node]
    F -->|Backup Full| G[AWS S3 Node]
    C -->|Share link & password| H[Devices join room and download]
    I[Background worker] -->|Checks expiry continuously| J[Purges expired files permanently]
```

1. **Create a Room** : Select files and click upload on the homepage.
2. **Room Generated** : Server creates a room with a unique ID, password, and a 5-hour TTL timer.
3. **Direct Upload** : Files stream directly from your browser to object storage using presigned URLs.
4. **Node Selection** : The server picks the best storage node based on available capacity, automatically overflowing to backup nodes if the primary is full.
5. **Share the Link** : The room URL and password are shared with others who can join and download files.
6. **Auto-Purge** : A background cleanup thread continuously checks for expired rooms and permanently deletes all associated files from storage.

<br/>

## <img src="https://img.shields.io/badge/-Tech_Stack-ba0914?style=flat-square&logo=codeforces&logoColor=white" height="20" align="absmiddle" /> Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Backend** | <img src="https://cdn.simpleicons.org/python/3776AB" width="16" height="16" align="absmiddle" /> Python + <img src="https://cdn.simpleicons.org/flask/white" width="16" height="16" align="absmiddle" /> Flask | Web framework and API server |
| **Server** | <img src="https://cdn.simpleicons.org/gunicorn/499A4C" width="16" height="16" align="absmiddle" /> Gunicorn | Production WSGI server with multi-threading |
| **Database** | <img src="https://cdn.simpleicons.org/mongodb/47A248" width="16" height="16" align="absmiddle" /> MongoDB (Atlas) | Room metadata, file records, analytics |
| **Primary Storage** | <img src="https://cdn.simpleicons.org/cloudflare/F38020" width="16" height="16" align="absmiddle" /> Cloudflare R2 | S3-compatible object storage (zero egress fees) |
| **Secondary Storage** | <img src="https://cdn.simpleicons.org/tencent/00A4FF" width="16" height="16" align="absmiddle" /> Tencent COS | Fallback overflow node |
| **Tertiary Storage** | <img src="https://cdn.simpleicons.org/amazons3/569A36" width="16" height="16" align="absmiddle" /> AWS S3 | Additional overflow with CloudFront CDN |
| **CDN** | <img src="https://cdn.simpleicons.org/amazoncloudfront/FF9900" width="16" height="16" align="absmiddle" /> AWS CloudFront | Signed URL downloads for S3-stored files |
| **Reverse Proxy** | <img src="https://cdn.simpleicons.org/apache/D22128" width="16" height="16" align="absmiddle" /> Apache | TLS termination, HTTP/2, request routing |
| **Styling** | <img src="https://cdn.simpleicons.org/tailwindcss/06B6D4" width="16" height="16" align="absmiddle" /> Tailwind CSS | Utility-first CSS framework |
| **Frontend** | <img src="https://cdn.simpleicons.org/javascript/F7DF1E" width="16" height="16" align="absmiddle" /> Vanilla JavaScript | Direct upload client with multipart chunking |

<br/>

## <img src="https://img.shields.io/badge/-Security-ba0914?style=flat-square&logo=auth0&logoColor=white" height="20" align="absmiddle" /> Security Protocols

* **CSRF Protection** : All forms and API calls are protected with CSRF tokens.
* **Rate Limiting** : Per-IP rate limits on room creation, joining, and API calls.
* **Brute Force Protection** : IP lockout after repeated failed room join attempts.
* **Secure Sessions** : HttpOnly, SameSite=Lax, Secure (in production) cookies.
* **No Persistent Data** : Zero redundant backups; once purged, recovery is impossible.
* **Password Hashing** : Room passwords are hashed with Werkzeug's secure hasher.
* **Signed Downloads** : CloudFront and S3 downloads use time-limited signed URLs.

<br/>

## <img src="https://img.shields.io/badge/-Live-ba0914?style=flat-square&logo=google-chrome&logoColor=white" height="20" align="absmiddle" /> Use It Live

iLoveTempDrive is live and free to use at:

<div align="center">

### [https://ilovetempdrive.xyz](https://ilovetempdrive.xyz)

</div>

No sign-up required. Just open the site, drag your files, and share.

<br/>

## <img src="https://img.shields.io/badge/-Team-ba0914?style=flat-square&logo=github&logoColor=white" height="20" align="absmiddle" /> Contributors

<table align="center">
<tr>
<td align="center" width="250px">
<a href="https://github.com/mainaloohun">
<img src="https://github.com/mainaloohun.png" width="90px;" alt="Asad" style="border-radius: 50%; border: 2px solid #ba0914;"/>
<br/>
<br/>
<strong>Asad</strong>
</a>
<br/>
<sub>Ideator & Backend Developer</sub>
<br/>
<br/>
<sub>Proposed the zero-trace concept and architected the backend infrastructure.</sub>
</td>
<td align="center" width="250px">
<a href="https://github.com/ffenjil">
<img src="https://github.com/ffenjil.png" width="90px;" alt="Jil" style="border-radius: 50%; border: 2px solid #ba0914;"/>
<br/>
<br/>
<strong>Jil</strong>
</a>
<br/>
<sub>Designer & Developer</sub>
<br/>
<br/>
<sub>Designed the UI from the ground up and brought the visual identity to life.</sub>
</td>
</tr>
</table>

<br/>

---

<div align="center">

**Made with <img src="https://img.shields.io/badge/-Love-ba0914?style=flat-square&logo=heart&logoColor=white" height="15" align="absmiddle" /> by [Asad](https://github.com/mainaloohun) & [Jil](https://github.com/ffenjil)**

<br/>

<sub>iLoveTempDrive &copy; 2026. All rights reserved.</sub>

</div>
