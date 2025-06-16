
# 📘 Project Description: New Employee Orientation Email Automation

This document explains the steps taken to build a Power Automate flow that automates sending a personalized HTML welcome email to new hires at your desired Company, without including proprietary code or credentials.

---

## 🛠️ Step-by-Step Overview

### 1. Setup Recurrence Trigger
- Configured a **Recurrence** trigger to run **daily at 5:00 PM EST**.
- This ensures that new users created within the last 24 hours are included in the process.

---

### 2. Retrieve Leadership Images from SharePoint
- Used multiple **Get file content using path** actions to retrieve image files.
- Each action points to a **SharePoint document library** that contains profile photos.
- The files are referenced by their exact path, such as:
  - **Site Address**: `https://yourcompany.sharepoint.com/sites/YourSite/`
  - **File Path**: `/Shared Documents/YourList/UserPhoto.png`

---

### 3. HTTP Call to Microsoft Graph API
- Added an **HTTP** action to call the Microsoft Graph API.
- The request used the **GET** method to query for users created in the past day.
- Created an App Registration inside of Microsoft Entra with the following permissions:
  - `User.Read.All`
  - `Directory.Read.All`
  - *(Adjust based on your org’s needs)*

---

### 4. Parse JSON Response
- Inserted a **Compose** action to capture the HTTP response body.
- Used **Parse JSON** to extract an array of new user data.

<details>
  <summary>Click to view Parse JSON schema</summary>

```json
{
  "type": "object",
  "properties": {
    "@@odata.context": {
      "type": "string"
    },
    "value": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "displayName": {
            "type": "string"
          },
          "mail": {},
          "createdDateTime": {
            "type": "string"
          }
        },
        "required": [
          "displayName",
          "mail",
          "createdDateTime"
        ]
      }
    }
  }
}
```

</details>

- Parsed fields include `displayName`, `mail`, and `createdDateTime`.

---

### 5. Loop Through New Users
- Added an **Apply to Each** loop to iterate over all parsed users.

---

### 6. Send Personalized Welcome Email
- Inside the loop, configured a **Send an email (V2)** action from Outlook.
- The email body is a formatted **HTML** message that includes:
  - Personalized greeting using `displayName`
  - A leadership introduction section with embedded base64 images from SharePoint
  - Mission, vision, and values of the organization
  - Contact information and photos of each leader

---

## 🔐 Notes
- All sensitive information (emails, GUIDs, tenant IDs, client secrets, and file paths) have been redacted from the public version of this workflow.
- Images were dynamically inserted using base64 content from SharePoint file outputs.
