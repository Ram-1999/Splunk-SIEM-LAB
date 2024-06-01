# Splunk Add-on for Azure Active Directory

How to install and configure the Splunk Add-on for Azure Active Directory (Azure AD) to collect and analyze logs.

## Prerequisites

Before you begin, ensure you have the following:

- A Splunk instance (either Splunk Enterprise or Splunk Cloud).
- Admin access to your Azure Active Directory.
- Admin access to your Splunk instance.

## Step 1: Install the Splunk Add-on

1. **Log in to your Splunk instance**:
   - Open your Splunk Web interface in a browser.
   - Log in with your administrative credentials.

2. **Navigate to the Apps section**:
   - Click on the **Apps** dropdown menu at the top left of the Splunk Web interface.
   - Select **Find more apps**.

3. **Search for the Add-on**:
   - In the search bar of the Splunkbase page, type **"Azure Active Directory"** and press Enter.
   - Look for the **Splunk Add-on for Microsoft Cloud Services** in the search results.

4. **Install the Add-on**:
   - Click on the **Splunk Add-on for Microsoft Cloud Services** to open its details page.
   - Click on the **Install** button.
   - If prompted, enter your Splunk.com credentials to download the app.

5. **Restart Splunk (if necessary)**:
   - Some add-ons may require a restart of the Splunk instance to complete the installation.
   - If prompted, click on **Restart Now** to restart Splunk.

# Azure AD Service Principal for Splunk Log Ingestion

How to create a service principal (SP) in Azure Active Directory (Azure AD) and assign the required API permissions for Splunk log ingestion.

## Step 1: Create a Service Principal

### Using Azure Portal

1. Log in to the [Azure Portal](https://portal.azure.com).
2. Navigate to **Azure Active Directory** > **App registrations** > **New registration**.
3. Enter a name for the application (e.g., "Splunk-Log-Ingestion").
4. Select the supported account types. Typically, you can choose "Accounts in this organizational directory only."
5. Optionally, add a redirect URI.
6. Click **Register** to create the application.

After creating the application, note down the Application (client) ID and Directory (tenant) ID from the app's Overview page.

## Step 2: Create a Client Secret

1. Navigate to the app you registered in App registrations.
2. Go to Certificates & secrets.
3. Click on New client secret.
4. Add a description and set an expiry period.
5. Click Add and copy the value of the client secret. This will be used in the Splunk configuration.

## Step 3: Assign API Permissions

1. Go to the registered app in App registrations.
2. Select API permissions > Add a permission.
3. Choose Microsoft Graph.
4. Select Application permissions.
5. Add the following permissions:
6. AuditLog.Read.All
7. Directory.Read.All
8. Click Add permissions.
9. Click on Grant admin consent for [Your Organization].
10. Confirm by clicking Yes.

## Step 4: Configure Splunk

Log in to your Splunk instance.

Navigate to the Splunk Add-on for Microsoft Cloud Services.

Create a new input for Azure AD logs.

Enter the following information:

Client ID: The client ID of your registered app.
Client Secret: The client secret you created.
Save the configuration.

## Step 5: Create an Index in Splunk

1. Log in to your Splunk instance.
2. Click on Settings > Indexes.
3. Click on New Index.
4. Enter a name for the index (e.g., azure_ad_logs).
5. Click Save.

## If everything is set up properly, you should now be able to get the logs.



