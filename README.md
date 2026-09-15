# Cebroid 2k26 Reception QR Verification

This project is a web-based QR code scanner and manual entry system used for managing attendance at the reception of Cebroid 2k26. It interfaces with a Google Sheet to verify participant details and mark them as present.

## Architecture

1.  **Frontend (`index.html`)**: A mobile-responsive web page using `html5-qrcode` to scan QR codes or accept manual ticket number entry.
2.  **Proxy API (`api/attendance.js`)**: A Vercel serverless function that proxies requests from the frontend to the Google Apps Script. This is necessary to bypass CORS restrictions when calling Google Apps Script directly from the browser.
3.  **Backend (`app script.txt`)**: A Google Apps Script that serves as the REST API to interact with the Google Sheet where registration data is stored.

## Setup Instructions

### 1. Google Sheets & Apps Script Setup

1.  Create a Google Sheet and name the primary tab exactly `Registrations`.
2.  Ensure your columns match the expected layout (e.g., Column 2 is Name, Column 9 is Ticket Number, Column 10 is Verification Status).
3.  Add a new header named **Attended** in Column 16 (P1).
4.  Open **Extensions > Apps Script** from the Google Sheet.
5.  Copy the contents of `app script.txt` into the script editor.
6.  **Important:** Replace `YOUR_SPREADSHEET_ID_HERE` in the script with your actual Google Sheet ID.
7.  Run the `authorizeScript` function once and grant necessary permissions.
8.  Deploy the script as a **Web App**:
    *   Execute as: Me
    *   Who has access: Anyone
9.  Copy the generated Web App URL (`/exec`).

### 2. Vercel Proxy Setup

1.  Open `api/attendance.js`.
2.  Replace `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` with the Web App URL you copied from the previous step.
3.  Deploy this project to Vercel.

## Usage

Once deployed, open the Vercel app URL on a mobile device or computer with a camera.
- **Scan QR**: Use the camera to scan a participant's QR code.
- **Manual Entry**: Type the ticket number (e.g., `004` for `Cebroid-004`) to manually verify and mark attendance.
