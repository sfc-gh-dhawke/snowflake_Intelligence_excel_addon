# Snowflake Intelligence for Excel

An Excel Add-in (.xlam) that lets you chat with a Snowflake Cortex Agent directly from your spreadsheet. Ask questions in natural language, get answers, and export result tables back into Excel with one click.

## What It Does

- **Chat with a Cortex Agent** from inside Excel using a built-in chat panel
- **Send worksheet data** alongside your questions so the agent can analyze your spreadsheet context
- **Export result tables** returned by the agent directly into new or existing Excel sheets
- **Multiple auth methods** including SSO (browser-based), PAT, OAuth, and keypair
- **Works with any Cortex Agent** -- point it at a named agent object or provide an inline agent spec

## Features

| Feature | Description |
|---------|-------------|
| Settings Panel | Configure your Snowflake account URL, credentials, role, warehouse, and agent |
| SSO Login | Browser-based single sign-on for macOS (no tokens to paste) |
| Role/Warehouse Dropdowns | Auto-populated from your account via SHOW ROLES / SHOW WAREHOUSES |
| Chat Panel | Multi-turn conversation with your Cortex Agent |
| Include Data | Attach full sheet or cell range data as markdown context with your question |
| Export to Excel | Write agent-returned tables to a new sheet or append below existing data |
| Debug Mode | Toggle raw API response output for troubleshooting |

## Requirements

- Microsoft Excel on Windows or macOS with VBA macro support
- A Snowflake account with a Cortex Agent configured
- One of: PAT, OAuth token, keypair JWT, or SSO access

## Quick Start

See [SETUP.md](/SETUP.md) for installation and configuration instructions.

## Project Structure

```
xlam_source/
  SETUP.md                          # Installation & configuration guide
  VBA/
    SnowflakeIntelligence.xlam      # The compiled add-in (install this)
    ModConfig.bas                   # Configuration, auth headers, settings storage
    ModHTTP.bas                     # HTTP transport (curl), SSO login, SQL API calls
    ModSheetUI.bas                  # Settings sheet, chat panel, dropdowns
    ModChatUI.bas                   # Chat UI helpers
    ModJsonParser.bas               # JSON parsing utilities
    ModExcelWriter.bas              # Write result sets to Excel sheets
    ModSetup.bas                    # Toolbar button creation, installation verification
    ModMain.bas                     # Entry points
    ThisWorkbook.cls                # Workbook open/close event handlers
```
