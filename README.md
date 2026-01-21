# Sawata Research Hub - Institutional Repository

A web-based institutional repository for enhancing research accessibility and knowledge management at Sawata National High School.

## Deployment to Vercel - Step-by-Step Guide

This guide will walk you through deploying your research hub to Vercel, a free hosting platform with custom domain support.

---

## Step 1: Create a GitHub Account (If You Don't Have One)

1. Go to https://github.com
2. Click "Sign up" and follow the instructions
3. Choose the free plan
4. Verify your email address

---

## Step 2: Upload Your Project to GitHub

### Option A: Using GitHub Website (Easier)

1. **Create a New Repository:**
   - Go to https://github.com and log in
   - Click the "+" button in the top-right corner
   - Select "New repository"
   - Repository name: `sawata-research-hub`
   - Description: "Institutional Repository for Sawata National High School"
   - Set to "Public" (free tier requires public repos for free hosting)
   - Do NOT check "Add a README file" (we already have files)
   - Click "Create repository"

2. **Upload Your Files:**
   - On your new repository page, click "uploading an existing file"
   - Drag and drop all files from your project folder:
     - index.html
     - assets/ folder (entire folder)
     - package.json
     - vercel.json
     - .gitignore
     - RESEARCH-STATS-POLICIES-GUIDE.md
   - Click "Commit changes"

### Option B: Using Git Command Line

1. **Install Git:**
   - Download from https://git-scm.com
   - Run the installer with default settings

2. **Open Command Prompt/Terminal:**
   ```bash
   # Navigate to your project folder
   cd path/to/sawata-research-hub
   
   # Initialize git
   git init
   
   # Add all files
   git add .
   
   # Create first commit
   git commit -m "Initial commit - Sawata Research Hub"
   
   # Create GitHub repository (from Step 1)
   # Then connect it:
   git branch -M main
   git remote add origin https://github.com/YOURUSERNAME/sawata-research-hub.git
   git push -u origin main
   ```

---

## Step 3: Create a Vercel Account

1. Go to https://vercel.com
2. Click "Sign up"
3. Choose "Continue with GitHub" (easiest)
4. Authorize Vercel to access your GitHub account
5. Complete your profile information

---

## Step 4: Deploy Your Project to Vercel

### Method 1: Import from GitHub (Recommended)

1. **In Vercel Dashboard:**
   - Click "Add New..." → "Project"
   - Click "Import Git Repository"
   - Find and select "sawata-research-hub"
   - Click "Import"

2. **Configure Project:**
   - Framework Preset: "Other" or "Static"
   - Build Command: `npm run build` (already configured)
   - Output Directory: `dist` (already configured)
   - Click "Deploy"

3. **Wait for Deployment:**
   - Vercel will build and deploy your site
   - This takes 1-2 minutes
   - You'll see a success message with your URL

### Method 2: Using Vercel CLI

1. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```

2. **Deploy:**
   ```bash
   # Navigate to your project
   cd path/to/sawata-research-hub
   
   # Login to Vercel
   vercel login
   
   # Deploy (use --prod for production)
   vercel --prod
   ```

3. **Follow Prompts:**
   - Set up and deploy? → Yes
   - Which scope? → Your username
   - Link to existing project? → No
   - Project name? → sawata-research-hub
   - Directory? → Current directory
   - Want to modify settings? → No (everything is configured)

---

## Step 5: Access Your Deployed Website

After deployment, Vercel will provide a URL like:
```
https://sawata-research-hub.vercel.app
```

or

```
https://sawata-research-hub-yourusername.vercel.app
```

Click the link to verify your website is working!

---

## Step 6: Add Custom Domain (Optional)

1. **In Vercel Dashboard:**
   - Click on your project "sawata-research-hub"
   - Go to "Settings" → "Domains"

2. **Add Your Domain:**
   - Enter your domain name (e.g., `research.sawata.edu.ph`)
   - Click "Add"

3. **Configure DNS at Your Registrar:**

   **For apex domain (example.com):**
   - Add an A record pointing to `76.76.21.21`
   
   **For subdomain (www.example.com):**
   - Add a CNAME record pointing to `cname.vercel-dns.com`

4. **Wait for DNS Propagation:**
   - Can take up to 24 hours
   - Usually 15-30 minutes
   - Vercel will show "Valid" when configured

5. **SSL Certificate:**
   - Vercel automatically provisions HTTPS
   - May take a few minutes after DNS verification

---

## Step 7: Automatic Deployments

With GitHub integration, Vercel automatically deploys changes:

1. **Make Changes Locally:**
   - Edit files in your project

2. **Push to GitHub:**
   ```bash
   git add .
   git commit -m "Describe your changes"
   git push
   ```

3. **Vercel Automatically Deploys:**
   - Vercel detects the push
   - Rebuilds your site
   - Updates the live URL
   - Provides a preview URL for review

---

## File Structure

```
sawata-research-hub/
├── index.html              # Main HTML file
├── vercel.json             # Vercel configuration
├── package.json            # Project dependencies
├── .gitignore              # Git ignore rules
├── assets/
│   ├── css/
│   │   └── styles.css      # Main stylesheet
│   ├── images/
│   │   └── sawata-logo.png # Logo image
│   └── js/
│       ├── app.js          # Main application logic
│       └── chart.min.js    # Chart library
├── RESEARCH-STATS-POLICIES-GUIDE.md
└── README.md               # This file
```

---

## Configuration Files Explained

### vercel.json
This file tells Vercel how to build and serve your site:
- **buildCommand**: How to build your site (`npm run build`)
- **outputDirectory**: Where built files are located (`dist`)
- **rewrites**: Routes all requests to index.html (needed for SPA routing)
- **headers**: Sets cache headers for better performance

### package.json
Contains project information and scripts:
- **build**: Creates the dist/ folder with production files
- **test**: Runs the test script

---

## Troubleshooting

### Build Fails

**Problem:** "Command not found" or build timeout

**Solution:**
1. Check that `npm run build` works locally
2. Ensure package.json has the correct build script
3. Verify all dependencies are in package.json

### Page Not Found (404)

**Problem:** Pages return 404 errors

**Solution:**
1. Check vercel.json rewrites configuration
2. Ensure all routes point to /index.html
3. Redeploy after fixing vercel.json

### Assets Not Loading

**Problem:** CSS, JS, or images not appearing

**Solution:**
1. Check file paths in index.html
2. Ensure assets are in the assets/ folder
3. Verify case sensitivity (Linux is case-sensitive)
4. Check browser console for 404 errors

### Custom Domain Not Working

**Problem:** Domain shows "Site not found" or error

**Solution:**
1. Verify DNS records are correct
2. Wait for DNS propagation (up to 24 hours)
3. Check that domain is spelled correctly in Vercel
4. Ensure no conflicting records at your registrar

---

## Maintaining Your Site

### Updating Content

1. Edit files in your local project folder
2. Test locally if possible
3. Push changes to GitHub:
   ```bash
   git add .
   git commit -m "Updated content"
   git push
   ```
4. Vercel automatically deploys within 1-2 minutes

### Adding New Research Papers

1. Upload paper files to Supabase Storage
2. Update your local index.html or admin panel
3. Push changes to GitHub

### Monitoring Traffic

1. Go to Vercel Dashboard
2. Click on your project
3. View "Analytics" for visitor statistics

---

## Supabase Integration

Your site uses Supabase for:
- **research-papers**: Storing research document files
- **user-credentials**: Storing user accounts
- **RESEARCH-STATS**: Tracking views and downloads

Keep your Supabase credentials secure and never commit them to GitHub.

---

## Need Help?

- **Vercel Documentation:** https://vercel.com/docs
- **GitHub Help:** https://help.github.com
- **Git Documentation:** https://git-scm.com/doc

---

## License

This project is for educational use at Sawata National High School.

---

Last Updated: January 2026
