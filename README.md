# Swipe MCP Server

Connect your AI assistant directly to your Swipe Billing App — create invoices, query transactions, manage inventory, and run reports, all through natural language.

---

## Supported Features

- 📄 **Document Management** — Create, edit and cancel invoices, purchase orders, estimates, delivery challans, and more.
- 📊 **Transaction Queries** — Fetch and filter sales, purchases, returns, and pro-forma invoices across any date range.
- 📈 **Analytics & Reports** — Run detailed financial and product-level analysis for your business.
- 🛒 **Inventory Control** — Record stock-in and stock-out movements and track product levels.
- 🏪 **Master Data** — Add and update customers, vendors, and products.
- 💸 **Expense Tracking** — Log and categorise business expenses.
- ⚙️ **Settings Management** — Update company profile, GSTIN, invoice preferences, and other settings.
- 🔍 **GST & HSN Lookup** — Search HSN codes and look up GST rate changes.

---

## Installation Guide

> **Authentication:** Swipe MCP uses OAuth2 with PKCE. When prompted, sign in with your Swipe account and select the company you want to connect.

### Install in VS Code

**One-click installation**

[![Install in VS Code](https://img.shields.io/badge/Install%20in-VS%20Code-blue)](https://insiders.vscode.dev/redirect?url=vscode://saoudrizwan.claude-dev/openMcpServer?config={"mcpServers":{"swipe-mcp":{"url":"https://app.getswipe.in/api/mcp/sse","type":"http"}}})

**Manual installation**

Add this to your `mcp.json` file:

```json
{
  "servers": {
    "swipe-mcp": {
      "url": "https://app.getswipe.in/api/mcp/sse",
      "type": "http"
    }
  }
}
```

---

### Install on Claude Desktop

Claude Desktop does not support remote HTTP MCP servers natively, so you need to proxy through `mcp-remote`. Make sure [Node.js](https://nodejs.org) (v18+) is installed first.

1. Open Claude Desktop.
2. Go to **Settings → Developer → Edit Config**.
3. Open `claude_desktop_config.json` in a text editor.
4. Add the following configuration:

```json
{
  "mcpServers": {
    "swipe-mcp": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://app.getswipe.in/api/mcp/sse"
      ]
    }
  }
}
```

5. Save the file and restart Claude Desktop.
6. On first launch, a browser window will open for OAuth sign-in — log in with your Swipe account and select your company.

---

### Install on Claude.ai (Web / Subscription)

**Using Connectors** *(requires a Claude Pro or Team subscription)*

1. Open [Claude.ai](https://claude.ai).
2. Go to **Settings → Connectors → Add custom connector**.
3. Enter the URL: `https://app.getswipe.in/api/mcp/sse`
4. Save. Claude will redirect you through the Swipe OAuth flow — sign in with Swipe when prompted.

**Using Manual Configuration** *(available on free plan)*

1. Go to **Settings → Developer → Edit Config**.
2. Add the `mcp-remote` config the same way as Claude Desktop above.

---

### Install in Other MCP Clients (ChatGPT, Cursor, Windsurf, etc.)

For any MCP client that supports remote HTTP/SSE servers, enter:

```
https://app.getswipe.in/api/mcp/sse
```

The client will walk you through an OAuth sign-in. When prompted, **sign in with Swipe** (using your registered mobile number + OTP). After login, select the company you want the AI to operate on.

---

## Available Tools

### 📋 Querying & Search

| Tool | What it does |
|---|---|
| `get_transactions` | List and filter invoices, purchases, estimates, delivery challans, and returns by date, payment status, or search term |
| `get_document_details` | Get full details of any specific document by its ID or number |
| `search_item` | Search your product/item catalogue |
| `search_party` | Search customers or vendors |
| `get_expense_categories` | List all available expense categories |
| `hsn_code_search` | Look up HSN codes for GST classification |
| `gst_rate_changes_search` | Find recent or historical GST rate changes for a product |

### 📊 Analytics & Reports

| Tool | What it does |
|---|---|
| `detailed_report_analysis` | Run deep analytical reports on financials — revenue, outstanding, trends |
| `detailed_product_analysis` | Analyse product-level performance — top sellers, movement, margins |

### 📝 Create Documents

| Tool | What it does |
|---|---|
| `create_document` | Create an invoice, purchase order, estimate, pro-forma, delivery challan, sales return, or purchase return |
| `create_expense` | Log a business expense entry |

### ✏️ Edit & Update

| Tool | What it does |
|---|---|
| `edit_document_details` | Modify fields on an existing document (items, amounts, dates, notes, etc.) |
| `cancel_document` | Cancel a document |
| `document_affix` | Attach notes, e-way bill numbers, or other affixed data to a document |

### 🏪 Master Data Management

| Tool | What it does |
|---|---|
| `add_product` | Add a new product to your catalogue |
| `add_customer` | Add a new customer |
| `add_vendor` | Add a new vendor |
| `update_product` | Update an existing product's details |
| `update_customer` | Update an existing customer's details |

### 📦 Inventory

| Tool | What it does |
|---|---|
| `stock_in` | Record incoming stock for a product |
| `stock_out` | Record outgoing stock for a product |

### ⚙️ Company & Settings

| Tool | What it does |
|---|---|
| `update_company_name` | Update your company's display name |
| `update_company_gstin` | Update your company's GSTIN |
| `update_settings` | Update general company settings |
| `update_invoice_settings` | Configure invoice-specific settings (prefix, terms, etc.) |
| `get_swipe_invoice` | Retrieve your Swipe subscription invoice |

---

## Example Prompts

Get started with these prompts:

**Transactions & Documents**
- *"Show me all unpaid invoices from last month"*
- *"Get details of invoice INV-1042"*
- *"List all purchase orders raised this quarter"*
- *"Show my top 5 sales by amount this year"*

**Creating Documents**
- *"Create an invoice for Rahul Enterprises for 10 units of Steel Pipes at ₹500 each"*
- *"Make a purchase order for Tata Steel for 50 kg of MS Angle"*
- *"Generate an estimate for ABC Ltd for the items in our last order"*

**Inventory & Products**
- *"Add 200 units of stock for product SKU-101"*
- *"Search for all products with 'pipe' in the name"*
- *"Find the HSN code for cotton fabric"*

**Analytics**
- *"Give me a revenue breakdown by customer for this financial year"*
- *"Which are my top 10 selling products this month?"*
- *"Show outstanding receivables older than 30 days"*

**Settings & Master Data**
- *"Add a new customer: Mehta Trading Co, GST 27AAECM1596K1Z8, Mumbai"*
- *"Update the price of product SKU-205 to ₹1,200"*
- *"Change our invoice prefix to 'SWP'"*

---

## Whitelisted OAuth Redirect URIs

The following redirect URIs are pre-approved for OAuth authentication:

- `claude://claude.ai/settings/connectors`
- `https://claude.ai/api/mcp/auth_callback`
- `https://chatgpt.com/connector_platform_oauth_redirect`
- `https://insiders.vscode.dev/redirect`
- `https://vscode.dev/redirect`
- `https://oauth.pstmn.io/v1/callback`
- `http://localhost` *(any port — for native desktop clients)*

If your client's redirect URI is not on this list, contact the Swipe team to get it whitelisted.

---

## Authentication Notes

- Authentication is via **OTP on your registered Swipe mobile number**.
- After OTP verification, you select the company you want the AI to work with.
- Access tokens are valid for **30 days**.
- PKCE (Proof Key for Code Exchange) is used throughout — no client secrets are stored by your AI client.

---

*Swipe MCP is intended for use by authorised Swipe account holders only.*
