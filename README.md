📋 Ebegba Political Network - Registration System

This project provides a responsive registration form and a secure admin dashboard for managing members of the Ebegba Political Network.
Form submissions are saved automatically into a Google Sheet via a Google Apps Script backend.

🚀 Features

✅ Responsive registration form (index.html)

✅ Fields: Full Name, Email, Phone, Location, Area of Interest

✅ Data stored in Google Sheets

✅ Admin dashboard (admin.html) to view all registered members

✅ Password-protected admin access

📂 Project Structure
.
├── index.html    # Public registration form
├── admin.html    # Admin dashboard (password protected)
├── README.md     # Project documentation

🛠️ Setup Instructions
1. Create a Google Sheet

Open Google Sheets

Add headers in row 1:

Full Name | Email | Phone | Location | Area of Interest | Timestamp

2. Add Google Apps Script

In Google Sheets → Extensions → Apps Script

Delete default code and paste:

function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);

  sheet.appendRow([
    data.fullname,
    data.email,
    data.phone,
    data.location,
    data.interest,
    new Date()
  ]);

  return ContentService
    .createTextOutput(JSON.stringify({status:"success", message:"Registered!"}))
    .setMimeType(ContentService.MimeType.JSON);
}

function doGet(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var rows = sheet.getDataRange().getValues();
  var data = [];

  for (var i = 1; i < rows.length; i++) {
    data.push({
      fullname: rows[i][0],
      email: rows[i][1],
      phone: rows[i][2],
      location: rows[i][3],
      interest: rows[i][4],
      timestamp: rows[i][5]
    });
  }

  return ContentService
    .createTextOutput(JSON.stringify(data))
    .setMimeType(ContentService.MimeType.JSON);
}

3. Deploy the Web App

Click Deploy → New Deployment → Web App

Execute as: Me

Who has access: Anyone

Copy the /exec URL (e.g.
https://script.google.com/macros/s/AKfycb.../exec)

4. Connect Frontend

In index.html and admin.html, replace the API link with your Web App link:

const API_URL = "https://script.google.com/macros/s/AKfycbxiXzpJKcYUXUGFyxPjAuU5R69HzGA5jny1hn2OuXt4AUgYCbuF_8JXPpnLmAk1jAA2XA/exec";

5. Deploy Frontend

Host the files using:

GitHub Pages

Netlify

Vercel

Share the index.html link with members to register.

Use the admin.html link privately to view registrations.

🔑 Admin Access

admin.html is password protected.

Default password is:

Ebegba2025


👉 You can change it in admin.html:

const ADMIN_PASSWORD = "Ebegba2025";

✅ Usage Flow

Member opens registration form (index.html) → fills details → data goes into Google Sheet.

Organizer opens admin dashboard (admin.html) → enters password → views all registered members.

📸 Example

Public form (index.html):
Members see only the registration form.

Admin dashboard (admin.html):
Organizer sees the full table of registrations after logging in.

⚠️ Notes

The first time you deploy the Google Script, Google may warn “This app isn’t verified”.

Click Advanced → Go to Project (unsafe) → Allow.

This appears only to the developer, not to form users.

Make sure your sheet has enough rows to collect responses.
