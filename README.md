📋 Ebegba Political Network – Registration System

This is a responsive web-based registration system for Ebegba Political Network.
It allows members and intending attendees to register their interest and automatically stores the data in a Google Sheet using Google Apps Script.

An admin dashboard is also included for viewing registered members securely.

🚀 Features

Responsive registration form (mobile + desktop friendly).

Collects: Full Name, Email, Phone, Location, Area of Interest.

Dropdown with multiple Areas of Interest:

Media and Publicity

Contact and Mobilization

Jobs

Digital Innovation and Technology

Others

Data automatically saved to Google Sheet via Apps Script.

Admin-only page (admin.html) to view registered members.

Interactive and modern styling with hover effects and transitions.

📂 Project Structure
/project-root
│── index.html   # Public registration form
│── admin.html   # Admin dashboard (view registrations)
│── README.md    # Documentation

⚙️ Setup Instructions
1. Create Google Sheet

Open Google Drive → Create a new Google Sheet.

Rename it: Ebegba Political Network Members.

Add the following headers in row 1:

Full Name | Email | Phone | Location | Area of Interest | Timestamp

2. Google Apps Script

In the sheet → Extensions > Apps Script.

Paste this code:

function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);

  sheet.appendRow([
    data.name,
    data.email,
    data.phone,
    data.location,
    data.interest,
    new Date()
  ]);

  return ContentService.createTextOutput(
    JSON.stringify({ result: "success" })
  ).setMimeType(ContentService.MimeType.JSON);
}

function doGet() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = sheet.getDataRange().getValues();
  var result = [];

  for (var i = 1; i < data.length; i++) {
    result.push({
      name: data[i][0],
      email: data[i][1],
      phone: data[i][2],
      location: data[i][3],
      interest: data[i][4],
      timestamp: data[i][5],
    });
  }

  return ContentService.createTextOutput(
    JSON.stringify(result)
  ).setMimeType(ContentService.MimeType.JSON);
}


Deploy → New Deployment → Web App

Execute as: Me

Who has access: Anyone

Copy the Web App URL

✅ Your App Link:

https://script.google.com/macros/s/AKfycbz4N6pMgjRQQjmUG3xruQk-CPbKpkLWQcFgW3YcfXLbFq8LWl751SRGAsakZMmzVGTcfg/exec

3. Update HTML Files

In both index.html and admin.html, update the script section:

const scriptURL = "https://script.google.com/macros/s/AKfycbz4N6pMgjRQQjmUG3xruQk-CPbKpkLWQcFgW3YcfXLbFq8LWl751SRGAsakZMmzVGTcfg/exec";

4. Deploy Your Website

You can host on GitHub Pages, Netlify, or Vercel.

Upload both index.html and admin.html.

Share index.html link publicly.

Keep admin.html private for organizers only.

🔑 Access

index.html → Public registration form.

admin.html → Admin dashboard (organizers only).

📌 Notes

If members report Google App not verified, you (the script owner) can proceed by clicking Advanced > Go to [App Name] (unsafe).

To fully remove the warning, you’d need to publish the app verification with Google Cloud, which is optional.

✅ With this setup:

Members only see the form.

Organizers (you) see the full list via admin.html.
