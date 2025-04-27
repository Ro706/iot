# Google Cloud

## APIs Required
- Google Drive API
- Google Sheets API

## Steps to Complete This Experiment

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create a project with the name **IOT123**.
3. Select the newly created project (it may take a few seconds to appear).
4. Open **API & Services**.
5. In **API & Services**, click **Enable APIs and Services**.
6. Search for **Google Drive API**.
7. Click **Enable**.
8. Repeat the same steps to enable **Google Sheets API**.
9. Go to **Credentials** -> **Create Credentials** -> **Service Account**.
10. Under **Role**, select **Basic** -> **Editor**.
11. Click **Done**.
12. Click on the created Service Account email and go to **Keys**.
13. Under **Add Key**, click **Create New Key**.
14. Choose **JSON** format and download the key.
15. Open your Python editor and write the provided code. Run it with the proper values (e.g., your sheet ID, range, credentials path).
16. You will see the Google Sheet getting updated.

