# Complete Guide: Fix SSL Error - Connect Hostinger Domain to Vercel

## The Problem
You're seeing: **"THIS SITE CAN'T PROVIDE A SECURE CONNECTION"**

This means your domain `examupdl.com` is not properly connected to Vercel's servers.

---

## Solution: Configure DNS in Hostinger

### Step 1: Login to Hostinger

1. Go to: https://hpanel.hostinger.com/
2. Login with your credentials
3. Click on **"Domains"** in the left sidebar

### Step 2: Select Your Domain

1. Find `examupdl.com` in the list
2. Click on it to open domain settings
3. Look for **"DNS / Name Servers"** or **"Manage DNS"**
4. Click on it

### Step 3: Check Current DNS Records

You'll see a list of DNS records. Look for:
- Any **A records** (Type: A)
- Any **CNAME records** (Type: CNAME)
- Any **AAAA records** (Type: AAAA)

### Step 4: Delete Conflicting Records

**DELETE these if they exist:**
- ❌ Any A record pointing to Hostinger's IP (not 76.76.21.21)
- ❌ Any CNAME record for @ (root domain)
- ❌ Any AAAA records
- ❌ Any old A records for www

**KEEP these:**
- ✅ MX records (for email)
- ✅ TXT records (for verification)
- ✅ NS records (nameservers)

### Step 5: Add Vercel DNS Records

Click **"Add Record"** or **"Add New Record"** button.

#### Record 1: Root Domain (examupdl.com)
```
Type: A
Name: @ (or leave blank, or type "examupdl.com")
Value: 76.76.21.21
TTL: 3600 (or Auto/Default)
```

Click **"Add"** or **"Save"**

#### Record 2: WWW Subdomain (www.examupdl.com)
```
Type: CNAME
Name: www
Value: cname.vercel-dns.com
TTL: 3600 (or Auto/Default)
```

Click **"Add"** or **"Save"**

### Step 6: Save Changes

1. Make sure both records are added
2. Click **"Save Changes"** or **"Update"** if needed
3. You should see both records in the list now

### Step 7: Disable Cloudflare (If Enabled)

In Hostinger, check if there's a **"Cloudflare"** toggle or **"Proxy"** option:
- If you see an orange cloud icon ☁️ - click it to turn it gray
- If there's a Cloudflare toggle - turn it **OFF**
- We want direct connection to Vercel, not through Cloudflare

### Step 8: Refresh SSL in Vercel

1. Go back to Vercel Dashboard: https://vercel.com/dashboard
2. Select your project: `examupdtsssswebsites-2-0`
3. Go to **Settings** → **Domains**
4. Click **"Refresh"** button next to `examupdl.com`
5. Click **"Refresh"** button next to `www.examupdl.com`
6. Wait 2-3 minutes

### Step 9: Wait for DNS Propagation

DNS changes take time to spread globally:
- **Minimum:** 5-10 minutes
- **Average:** 30 minutes
- **Maximum:** 24-48 hours (rare)

### Step 10: Check DNS Propagation

While waiting, check if DNS is updating:

1. Go to: https://dnschecker.org/
2. Enter: `examupdl.com`
3. Select: **A** record type
4. Click **"Search"**
5. You should see `76.76.21.21` appearing in different locations

Do the same for `www.examupdl.com` with **CNAME** type.

### Step 11: Clear Browser Cache

1. Press `Ctrl + Shift + Delete` (Windows) or `Cmd + Shift + Delete` (Mac)
2. Select **"Cached images and files"**
3. Select **"All time"**
4. Click **"Clear data"**

OR

Open an **Incognito/Private window** and try accessing your site.

### Step 12: Test Your Site

Try these URLs in order:

1. `https://examupdl.com` - Should work now ✅
2. `https://www.examupdl.com` - Should work now ✅
3. `http://examupdl.com` - Should redirect to https ✅

---

## Troubleshooting

### Still Getting SSL Error?

**Check 1: Verify DNS Records**
```bash
# On Windows Command Prompt:
nslookup examupdl.com

# Should show: 76.76.21.21
```

**Check 2: Verify in Vercel**
- Go to Vercel → Settings → Domains
- Both domains should show green checkmark ✅
- Should say "Valid Configuration"

**Check 3: Wait Longer**
- DNS can take up to 24 hours in rare cases
- Try again after 1 hour

**Check 4: Check Hostinger SSL Settings**
- In Hostinger, look for "SSL" settings
- Make sure it's not forcing Hostinger's SSL
- Disable any "Force HTTPS" in Hostinger

### Error: "Domain is already in use"

If Vercel says domain is already in use:
1. Remove the domain from Vercel
2. Wait 5 minutes
3. Add it again
4. Follow the DNS setup steps

### Error: "Invalid Configuration"

If Vercel shows "Invalid Configuration":
1. Double-check DNS records in Hostinger
2. Make sure there are NO conflicting records
3. Click "Refresh" in Vercel
4. Wait 10 minutes and refresh again

---

## Quick Reference: What Should Be in Hostinger DNS

After setup, your Hostinger DNS should look like this:

```
Type    Name    Value                       TTL
----    ----    -----                       ---
A       @       76.76.21.21                3600
CNAME   www     cname.vercel-dns.com       3600
MX      @       (your email server)        3600
TXT     @       (verification codes)       3600
NS      @       (hostinger nameservers)    3600
```

---

## Alternative: Use Vercel's Default Domain

If you can't fix the DNS issue, you can use Vercel's free domain:

Your site is available at:
`https://examupdtsssswebsites-2-0.vercel.app`

This works immediately without any DNS configuration!

---

## Need More Help?

1. **Hostinger Support:** https://www.hostinger.com/contact
   - Ask them to point your domain to Vercel
   - Give them these IPs: `76.76.21.21` and `cname.vercel-dns.com`

2. **Vercel Support:** https://vercel.com/help
   - They can check if your domain is properly configured

3. **Check Vercel Docs:** https://vercel.com/docs/concepts/projects/domains

---

## Summary

1. ✅ Login to Hostinger
2. ✅ Go to DNS settings for examupdl.com
3. ✅ Delete conflicting records
4. ✅ Add A record: @ → 76.76.21.21
5. ✅ Add CNAME record: www → cname.vercel-dns.com
6. ✅ Save changes
7. ✅ Refresh SSL in Vercel
8. ✅ Wait 10-30 minutes
9. ✅ Clear browser cache
10. ✅ Test your site

Good luck! 🚀
