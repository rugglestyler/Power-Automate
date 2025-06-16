# 📨 Bi-Weekly New Employee Orientation Email Automation

This Power Automate flow automatically sends a detailed, personalized HTML welcome email to employees. It introduces the leadership team, shares the organization's mission and values, and enhances the onboarding experience with embedded images and personalization.

---

## 📅 Trigger

### **Recurrence**
- This flow is scheduled to run **daily at 5:00 PM (EST)**.
- It checks for new users created within the last 24 hours.


## 🖼️ SharePoint Image Fetching

The flow retrieves members photos from a SharePoint document library. Each image is fetched as Base64 and dynamically inserted into the email:

| Action Name            | Purpose                                   |
|------------------------|-------------------------------------------|
| `Get Members Picture 1  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 2  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 3  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 4  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 5  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 6  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 7  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 8  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 9  | Retrieve Members Picture from Sharepoint |
| `Get Members Picture 10 | Retrieve Members Picture from Sharepoint |

Each image is pulled from the SharePoint path:  
`/sites/[Redacted]/[Redacted]/[Image].png`

---

## 📡 Data Source: Microsoft Graph API

### **HTTP Request**
- Pulls new users via Graph API:
