# 🎬 Video Streaming Platform - Quick Start Guide

## 🔑 Access Credentials

### Admin Panel
- **URL:** `/admin-portal-secure-2025-x7k9m2`
- **Email:** `admin@example.com`
- **Password:** `admin123`

### Public Pages
- **Home:** `/` - Shows all published streams
- **Stream:** `/stream/[id]` - Individual stream page with video player

## ✅ What's Been Built

### 1. Home Page (`/`)
- ✅ Arabic RTL interface
- ✅ Grid of all published streams
- ✅ Ad spaces (top & bottom)
- ✅ Responsive design
- ✅ Beautiful modern UI with shadcn/ui

### 2. Stream Pages (`/stream/[id]`)
- ✅ HLS.js video player
- ✅ M3U/M3U8 support
- ✅ Server selector (Server 1, 2, 3, 4)
- ✅ Ad spaces (top, bottom, sidebar)
- ✅ Live streaming indicator
- ✅ Connection status

### 3. Hidden Admin Panel (`/admin-portal-secure-2025-x7k9m2`)
- ✅ Secret URL (only you know it)
- ✅ Admin authentication
- ✅ Manage streams (create/edit/delete)
- ✅ Manage servers (add up to 4 servers per stream)
- ✅ Manage users (create/edit/delete)
- ✅ Manage ads (create/edit/delete)
- ✅ Beautiful dark theme UI

### 4. Backend API
- ✅ `/api/streams` - Stream CRUD operations
- ✅ `/api/streams/[id]` - Individual stream operations
- ✅ `/api/servers` - Server management
- ✅ `/api/users` - User management
- ✅ `/api/ads` - Ad management
- ✅ `/api/admin/auth` - Admin authentication

### 5. Database
- ✅ Prisma ORM with SQLite
- ✅ User model (with admin role)
- ✅ Stream model
- ✅ Server model (multiple servers per stream)
- ✅ Ad model (multiple ad positions)
- ✅ Seeded with sample data

## 🎯 Key Features

### Multiple Servers Per Stream
Each stream can have up to 4 different servers:
- Users can click to switch between servers
- Perfect for backup streams
- Each server has its own M3U/M3U8 URL
- Priority system for automatic selection

### Ad Management
Ads can be placed in multiple positions:
- **Home Top:** Banner on homepage
- **Home Bottom:** Banner on homepage
- **Stream Top:** Banner above video player
- **Stream Bottom:** Banner below video player
- **Stream Sidebar:** Side banner on stream page

### Hidden Admin Panel
- URL: `/admin-portal-secure-2025-x7k9m2`
- Complex name that only you know
- Not linked anywhere in the public site
- Requires admin login to access
- Complete control over all content

## 🚀 Quick Setup

### 1. Access Admin Panel
Visit: `http://localhost:3000/admin-portal-secure-2025-x7k9m2`

### 2. Login
- Email: `admin@example.com`
- Password: `admin123`

### 3. Create Your First Stream
1. Click "إضافة بث جديد" (Add new stream)
2. Enter title (e.g., "قناة الجزيرة")
3. Add description
4. Add thumbnail URL (optional)
5. Set "نشر الآن" (Publish now) to ON
6. Click "إضافة" (Add)

### 4. Add Servers to Stream
1. On the stream card, click "إضافة خادم" (Add server)
2. Server 1:
   - Name: "الخادم 1" (Server 1)
   - URL: Your M3U/M3U8 stream URL
   - Priority: 0 (highest)
3. Repeat for Server 2, 3, 4 with different URLs
4. Click "إضافة" (Add)

### 5. View Your Stream
1. Go to home page: `http://localhost:3000/`
2. Click on your stream
3. Select different servers to switch between them

## 📝 Example Stream URLs

### Test Streams (M3U8)
- `https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8`
- `https://bitdash-a.akamaihd.net/content/sintel/hls/playlist.m3u8`

### Real Stream Examples
Replace with your actual streaming service URLs.

## 🎨 Customization

### Change Admin Panel URL
1. Rename the folder: `src/app/admin-portal-secure-2025-x7k9m2`
2. Update all references in the code
3. Update the DEPLOYMENT_GUIDE.md

### Change Colors
Edit `tailwind.config.ts` to customize the color scheme.

### Add More Features
The codebase is modular and easy to extend with:
- Categories
- Search functionality
- User registration
- Comments/ratings
- Favorites
- Watch history

## 🔒 Security Notes

### Before Deploying to Production:
1. ⚠️ **CHANGE ADMIN PASSWORD**
   - Login to admin panel
   - Go to Users tab
   - Edit admin user
   - Set a strong password

2. ⚠️ **CHANGE ADMIN PANEL URL**
   - Rename the admin folder to something only you know
   - Update all references in the code

3. ⚠️ **USE HTTPS**
   - Setup SSL certificate
   - Force HTTPS redirects

4. ⚠️ **USE PRODUCTION DATABASE**
   - Switch from SQLite to PostgreSQL or MySQL
   - Update `DATABASE_URL` in `.env`

## 📱 Testing

### Test Video Streaming
1. Create a test stream
2. Add the sample M3U8 URL: `https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8`
3. Publish the stream
4. Open the stream page
5. Try switching between servers

### Test Admin Panel
1. Create a stream
2. Edit the stream
3. Delete the stream
4. Add users
5. Create ads

### Test Ad Placement
1. Create ads in different positions
2. Check homepage for ads
3. Check stream page for ads
4. Deactivate ads and verify they disappear

## 🎓 Next Steps

1. **Change default credentials**
2. **Test all features**
3. **Add your own stream URLs**
4. **Customize the design**
5. **Deploy to Hostinger** (see DEPLOYMENT_GUIDE.md)

## 🆘 Common Issues

### Stream not playing?
- Check the M3U/M3U8 URL is correct
- Verify the stream server is accessible
- Check browser console for errors

### Can't access admin panel?
- Verify URL is correct
- Clear browser cache
- Check credentials

### Ads not showing?
- Verify ads are set to "active"
- Check position is correct
- Ensure image URL is valid

---

**Ready to deploy?** Check out the full DEPLOYMENT_GUIDE.md for Hostinger setup!
