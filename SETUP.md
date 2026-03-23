# Snowflake Intelligence for Excel - Setup Guide

## Step 1: Copy the Add-in File

1. Download or copy `SnowflakeIntelligence.xlam` from the `VBA/` folder
2. Place it in a permanent location on your machine, for example:
   - **macOS:** `~/Library/Group Containers/UBF8T346G9.Office/User Content/Add-Ins/`
   - **Windows:** `C:\Users\<YourName>\AppData\Roaming\Microsoft\AddIns\`

   Or any folder you prefer -- just remember where you put it.

## Step 2: Enable Macros

**macOS:**
1. Open Excel
2. Go to **Excel > Preferences > Security & Privacy**
3. Under **Macro Security**, select **Enable all macros**
4. Close Preferences

**Windows:**
1. Open Excel
2. Go to **File > Options > Trust Center > Trust Center Settings...**
3. Click **Macro Settings** and select **Enable all macros**
4. Click **OK**

## Step 3: Install the Add-in

1. Open any workbook (or create a new one)
2. Open the Add-ins dialog:
   - **macOS:** **Tools > Excel Add-ins...**
   - **Windows:** **File > Options > Add-ins > Manage: Excel Add-ins > Go...**
3. Click **Browse...** and navigate to where you saved `SnowflakeIntelligence.xlam`
4. Check the box next to **SnowflakeIntelligence**
5. Click **OK**

Three small toolbar buttons will appear at the bottom-right of your worksheet:
- **Settings** (blue) -- open the settings panel
- **Chat** (green) -- open the chat panel
- **Debug** (gray) -- toggle debug mode

> If buttons don't appear, run the `CreateToolbarButtons` macro:
> - **macOS:** **Tools > Macro > Macros...**
> - **Windows:** **View > Macros > View Macros**

## Step 3: Configure Your Connection

Click the **Settings** button (or run the `ShowSettingsPanel` macro). A **CortexSettings** sheet will be created with the following fields:

### Account Details

| Field | Description | Example |
|-------|-------------|---------|
| **Account URL** | Your Snowflake account URL | `https://myorg-myaccount.snowflakecomputing.com` |
| **User Name** | Your Snowflake username | `jsmith` |
| **Auth Method** | Choose from: `pat`, `oauth`, `keypair`, or `sso` | `pat` |
| **Auth Token** | Your PAT, OAuth token, or keypair JWT (not needed for SSO) | |
| **Role** | Snowflake role to use | `ANALYST_ROLE` |
| **Warehouse** | Snowflake warehouse to use | `COMPUTE_WH` |

### Auth Method Details

- **pat** -- Programmatic Access Token. Paste your token in the Auth Token field.
- **oauth** -- OAuth token. Paste your Bearer token in the Auth Token field.
- **keypair** -- Keypair JWT. Paste your signed JWT in the Auth Token field.
- **sso** -- Browser-based SSO. Click the **SSO Login** button to authenticate via your browser. No token needed.

> For `pat`, `oauth`, and `keypair`, click **Refresh Lists** after saving to populate the Role and Warehouse dropdowns from your account.  
> For `sso`, your default role and warehouse are auto-filled from the login response.

### Agent Configuration

| Field | Description | Example |
|-------|-------------|---------|
| **Use Inline Agent** | `No` to use a named agent object, `Yes` to provide a JSON spec | `No` |
| **Agent Database** | Database where the agent lives | `MY_DB` |
| **Agent Schema** | Schema where the agent lives | `MY_SCHEMA` |
| **Agent Name** | Name of the Cortex Agent object | `MY_AGENT` |
| **Inline Spec (JSON)** | Only if Use Inline Agent = Yes. Full agent JSON spec. | |

### Save and Test

1. Fill in your account details and agent configuration
2. Click **Save Settings**
3. Click **Test Connection** to verify everything works
4. Click **Open Chat** to start chatting

## Using the Chat

1. Click the **Chat** button to open the chat panel
2. Type your question in the **MESSAGE** box
3. Optionally include worksheet data:
   - Set **Include Data** to `Full Sheet` or `Range`
   - Enter the sheet name or cell range (e.g., `Sheet1` or `A1:D50`) in the **Source** field
4. Click **SEND**
5. Responses appear in the chat history below, color-coded by sender
6. If the agent returns tables, click **EXPORT** to write them into Excel
7. Click **New Chat** to clear the conversation and start over

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Macros disabled | **macOS:** Excel > Preferences > Security & Privacy. **Windows:** File > Options > Trust Center > Macro Settings. |
| Buttons don't appear | Run `CreateToolbarButtons` from the Macros dialog (see Step 3) |
| "Operation not permitted" (macOS) | The Mac sandbox blocks some executables. The add-in uses `/usr/bin/curl` which is allowed. |
| HTTP errors | Check your Account URL is correct and you have network access |
| Empty response | Verify your auth token is valid and the agent exists |
| SSO login fails | Make sure Account URL and User Name are filled in before clicking SSO Login |
