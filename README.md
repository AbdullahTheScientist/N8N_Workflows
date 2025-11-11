# Abandoned Cart Recovery Workflow (n8n + AI)

This project provides an **automated abandoned cart recovery workflow** using [n8n](https://n8n.io/) and an AI language model (Google Gemini / OpenAI). It helps eCommerce stores recover sales by sending **personalized reminder emails** to customers who left items in their shopping cart.

## Features

- Detect abandoned carts automatically from Google Sheets or CRM.
- Compare last cart update with the current time to identify abandonment.
- Generate personalized and friendly email content using AI.
- Include cart items, checkout link, and small discounts in emails.
- Send emails via Gmail node in HTML format.
- Fully automated workflow — runs every minute to catch abandoned carts promptly.

## How It Works

1. **Google Sheets Trigger**: Watches for new or updated cart entries.
2. **Checkout Cart Items**: Filters carts with status `pending`.
3. **Function Node**: Converts cart timestamps to JS Date objects and calculates `oneHourAgo`.
4. **IF Node**: Checks if the cart was abandoned (not updated for more than 1 hour).
5. **AI Agent Node**: Generates personalized email content.
6. **Structured Output Parser**: Formats AI-generated email in HTML.
7. **Gmail Node**: Sends the email to the customer.

## Setup Instructions

1. **Install n8n**  
   - Local: `npm install n8n -g`  
   - Cloud: [n8n Cloud](https://n8n.io/cloud)

2. **Create Google Sheets & Gmail credentials** in n8n.

3. **Import Workflow JSON**  
   - Go to n8n Editor → `Import` → Paste JSON file.

4. **Configure Nodes**  
   - Google Sheets Trigger → set document ID & sheet.  
   - Gmail Node → add your email credentials.  
   - AI Agent → configure your AI model API key.

5. **Activate Workflow**  
   - Turn workflow active → runs automatically every minute.

## Customization

- Change **abandoned cart time** in the Function Node (`oneHourAgo` calculation).  
- Update **discount codes** in the AI prompt.  
- Modify email HTML template in AI prompt for branding.

## Example Output

```html
<p>Hey Abdullah,</p>
<p>We noticed you left some great items — a T-Shirt and Jeans — waiting in your cart. 👕👖</p>
<p>Complete your order now and enjoy <strong>10% off</strong> with code <b>CART10</b>.</p>
<p><a href="https://yourstore.com/cart/123" style="background-color:#007BFF;color:white;padding:10px 20px;text-decoration:none;border-radius:6px;">Complete Your Purchase</a></p>
<p>Hurry — your cart will expire soon!</p>
<p>Warm regards,<br>Your Store Team ❤️</p>
