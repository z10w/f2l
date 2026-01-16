# Video Streaming Platform - Deployment Guide

## 🎬 Project Overview

This is a complete video streaming platform built with Next.js 15, featuring:
- Live video streaming with M3U/M3U8 support
- Multiple server options per stream (Server 1, 2, 3, 4)
- Hidden admin panel with secret URL
- Arabic RTL interface
- Ad placement system
- Full CRUD operations for streams, users, and ads

## 🔑 Admin Credentials

**IMPORTANT: Change these credentials after first login!**

- **Admin Panel URL:** `/admin-portal-secure-2025-x7k9m2`
- **Email:** `admin@example.com`
- **Password:** `admin123`

## 🚀 Deployment Instructions for Hostinger

### Option 1: Hostinger VPS (Recommended)

#### Prerequisites
- VPS with Ubuntu 20.04 or higher
- Domain name pointed to your VPS
- SSH access to your VPS

#### Step 1: Install Node.js
```bash
# Update package manager
sudo apt update

# Install Node.js (version 18 or higher)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install Bun (faster than npm)
curl -fsSL https://bun.sh/install | bash

# Reload your shell
source ~/.bashrc
```

#### Step 2: Install Dependencies
```bash
# Clone your repository to the VPS
git clone <your-repo-url> /var/www/streaming-platform
cd /var/www/streaming-platform

# Install dependencies
bun install
```

#### Step 3: Setup Environment Variables
Create a `.env` file in the project root:
```bash
# Database (SQLite for simplicity)
DATABASE_URL="file:./db/custom.db"

# Optional: For production, you might want to use PostgreSQL or MySQL
# DATABASE_URL="postgresql://user:password@localhost:5432/streaming_db"
```

#### Step 4: Initialize Database
```bash
# Push database schema
bun run db:push

# Seed initial data
bun run scripts/seed.ts
```

#### Step 5: Build the Application
```bash
bun run build
```

#### Step 6: Setup PM2 (Process Manager)
```bash
# Install PM2 globally
sudo npm install -g pm2

# Start the application with PM2
pm2 start bun --name "streaming-platform" -- start

# Save PM2 configuration
pm2 save

# Setup PM2 to start on boot
pm2 startup
```

#### Step 7: Setup Nginx Reverse Proxy
```bash
# Install Nginx
sudo apt install nginx

# Create Nginx configuration
sudo nano /etc/nginx/sites-available/streaming-platform
```

Add this configuration:
```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable the site:
```bash
# Enable the site
sudo ln -s /etc/nginx/sites-available/streaming-platform /etc/nginx/sites-enabled/

# Test Nginx configuration
sudo nginx -t

# Restart Nginx
sudo systemctl restart nginx
```

#### Step 8: Setup SSL Certificate (HTTPS)
```bash
# Install Certbot
sudo apt install certbot python3-certbot-nginx

# Get SSL certificate
sudo certbot --nginx -d your-domain.com

# Certbot will automatically configure SSL for you
```

#### Step 9: Setup Firewall
```bash
# Configure UFW firewall
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

#### Step 10: Monitor Your Application
```bash
# Check PM2 status
pm2 status

# View logs
pm2 logs streaming-platform

# Restart application
pm2 restart streaming-platform
```

### Option 2: Hostinger Shared Hosting (Node.js)

If you have a Hostinger shared hosting plan with Node.js support:

1. **Upload Files:**
   - Use FTP or File Manager to upload all project files
   - Exclude: `node_modules`, `.next`, `.git`

2. **Install Dependencies:**
   ```bash
   # SSH into your account
   cd public_html
   bun install
   ```

3. **Setup Environment:**
   - Create `.env` file in your home directory
   - Add your database URL

4. **Initialize Database:**
   ```bash
   bun run db:push
   bun run scripts/seed.ts
   ```

5. **Configure Startup:**
   - Use Hostinger's Node.js setup tool
   - Set startup file: `package.json`
   - Set startup command: `bun run start`

## 🔐 Security Recommendations

1. **Change Admin Password Immediately**
   - Login to admin panel
   - Go to Users tab
   - Update admin password

2. **Change Admin Panel URL**
   - Rename the folder `/admin-portal-secure-2025-x7k9m2` to something only you know
   - Update all references in the code

3. **Use HTTPS**
   - Always use SSL certificates
   - Force HTTPS redirects

4. **Secure Database**
   - Use PostgreSQL or MySQL for production
   - Never commit `.env` file to version control
   - Use strong database passwords

5. **Implement Rate Limiting**
   - Add rate limiting to API routes
   - Prevent brute force attacks

6. **Regular Backups**
   - Backup database regularly
   - Keep backups off-site

## 📊 Managing the Platform

### Adding New Streams

1. Go to Admin Panel: `/admin-portal-secure-2025-x7k9m2`
2. Click "إضافة بث جديد" (Add new stream)
3. Fill in stream details
4. Add servers (up to 4 servers with different URLs)
5. Publish the stream

### Managing Users

1. In Admin Panel, go to "المستخدمون" tab
2. Add new users with appropriate roles
3. Regular users can view streams
4. Admins can access the admin panel

### Managing Ads

1. In Admin Panel, go to "الإعلانات" tab
2. Add ads to different positions:
   - `home-top`: Homepage top banner
   - `home-bottom`: Homepage bottom banner
   - `stream-top`: Stream page top
   - `stream-bottom`: Stream page bottom
   - `stream-sidebar`: Stream page sidebar

## 🎯 Features Overview

### Home Page (/)
- Grid view of all published streams
- Arabic RTL interface
- Ad placements (top and bottom)
- Responsive design

### Stream Pages (/stream/[id])
- HLS video player with M3U8 support
- Server switcher (Server 1, 2, 3, 4)
- Ad placements (top, bottom, sidebar)
- Live streaming indicator

### Admin Panel (/admin-portal-secure-2025-x7k9m2/dashboard)
- Manage streams (CRUD operations)
- Manage servers (add/edit/delete)
- Manage users (CRUD operations)
- Manage ads (CRUD operations)
- Authentication required

## 🛠️ Maintenance Commands

```bash
# Update dependencies
bun update

# Rebuild database schema
bun run db:push

# Generate Prisma Client
bun run db:generate

# Run development server
bun run dev

# Build for production
bun run build

# Start production server
bun run start

# Check code quality
bun run lint
```

## 📱 M3U/M3U8 Stream URLs

When adding streams, use these URL formats:

- **M3U8 (HLS):** `https://example.com/stream.m3u8`
- **M3U:** `https://example.com/playlist.m3u`

The platform automatically detects and plays both formats.

## 🆘 Troubleshooting

### Stream not playing
- Check server URL is correct
- Verify the stream is accessible
- Check browser console for errors
- Ensure CORS is configured on stream server

### Admin panel not accessible
- Verify you're logged in
- Check localStorage for admin user data
- Clear browser cache and cookies
- Verify admin credentials

### Database errors
- Run `bun run db:push` to sync schema
- Check DATABASE_URL in `.env` file
- Ensure database file has write permissions

### Build errors
- Clear `.next` folder: `rm -rf .next`
- Clear cache: `rm -rf node_modules/.cache`
- Reinstall dependencies: `bun install`

## 📞 Support

For issues or questions:
- Check the Next.js documentation: https://nextjs.org/docs
- Prisma documentation: https://www.prisma.io/docs
- HLS.js documentation: https://github.com/video-dev/hls.js

## 📝 License

This project is for personal use. Modify and customize as needed.

---

**Remember:** Never share your admin panel URL or credentials with anyone!
