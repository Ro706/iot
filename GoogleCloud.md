# Google Cloud

## APIs Required
- Google Drive API
- Google Sheets API

## Steps to Complete This Experiment

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create a project with the name **IOT123**.
   ![image](https://github.com/user-attachments/assets/303dad42-47a4-482b-8645-22cfc209241d)
3. Select the newly created project (it may take a few seconds to appear).
4. Open **API & Services**.
5. In **API & Services**, click **Enable APIs and Services**.
6. Search for **Google Drive API**.
7. Click **Enable**.
   ![image](https://github.com/user-attachments/assets/09a3405f-b98b-4c50-83c2-648188561b36)
8. Repeat the same steps to enable **Google Sheets API**.
    ![image](https://github.com/user-attachments/assets/6a3cf819-52e4-4c69-8b08-9c060156085c)
9. Go to **Credentials** -> **Create Credentials** -> **Service Account**.
    ![image](https://github.com/user-attachments/assets/4d4b1324-8737-41a3-be62-ff42c46b7378)
10. Under **Role**, select **Basic** -> **Editor**.
11. Click **Done**.
12. Click on the created Service Account email and go to **Keys**.
13. Under **Add Key**, click **Create New Key**.
    ![image](https://github.com/user-attachments/assets/78d945a1-c03e-4158-9a87-03fbfd6c3309)
14. Choose **JSON** format and download the key.
    ![image](https://github.com/user-attachments/assets/55ef112c-d068-4865-bbdd-64ef78e175a8)
15. Open your Python editor and write the provided code. Run it with the proper values (e.g., your sheet ID, range, credentials path).
16. You will see the Google Sheet getting updated.

```python
import gspread
import random
from oauth2client.service_account import ServiceAccountCredentials
from datetime import datetime
import time
# Define the scope and authenticate with Google
scope = ["https://spreadsheets.google.com/feeds", "https://www.googleapis.com/auth/drive"]
creds = ServiceAccountCredentials.from_json_keyfile_name('<name>.json', scope)
client = gspread.authorize(creds)

# Open the Google Spreadsheet by title or by key
spreadsheet = client.open("<name>")  # or use .open_by_key("your_spreadsheet_key")

# Select the sheet to work with (e.g., the first sheet)
sheet = spreadsheet.sheet1

#Upload some data (example: adding rows to the sheet)

data = [
    ["Name", "Age", "City"],
    ["ABC", str(datetime.now()), "Nagpur"],
    ["XYZ", "65", "Mumbai"],
]

# Update the sheet with the data
for row in data:
    sheet.append_row(row)

print("Data uploaded successfully!")
```

