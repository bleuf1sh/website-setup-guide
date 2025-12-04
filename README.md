# website-setup-guide

## Cloudflare + Gmail 
https://community.cloudflare.com/t/solved-how-to-use-gmail-smtp-to-send-from-an-email-address-which-uses-cloudflare-email-routing/382769

Note about updating the SPF record too
```
"v=spf1 include:_spf.mx.cloudflare.net include:_spf.google.com ~all"
```

### Details (in case link above doesn't work)
When the "Send Verification" option doesn't appear for an external, non-Gmail address like test@example.com, it means Gmail is no longer automatically trusting its own forwarding system to handle the verification and requires you to use a secure SMTP (Outgoing Mail Server) connection instead.

Since you're using a Cloudflare forwarder and not a full email hosting provider, the professional way to proceed is to explicitly configure Gmail to send the email using its own SMTP server, but using an App Password for security.

Here is the revised, professional process to add your address:

1. Prepare Your Google Account (Create an App Password)
To use your Gmail account's outgoing mail servers (smtp.gmail.com) for a custom address, you must be using a special, one-time password called an App Password for security, especially if you have 2-Step Verification (which is highly recommended).

    A. Enable 2-Step Verification (If not already enabled)

        Go to your Google Account Security Settings: myaccount.google.com/security
   
        Under "How you sign in to Google," make sure 2-Step Verification is ON.
        If it's not, you must enable it first.
    
    B. Generate an App Password

        Stay in the Security settings and find the "App passwords" option
        (it only appears if 2-Step Verification is on).
        
        Click "App passwords." You'll be asked to sign in again.
        
        In the next window:
        
        Select app: Choose "Mail".
        
        Select device: Choose "Other (Custom Name)" and enter a name like test@example.com SMTP.
        
        Click "Generate."
        
        Google will display a 16-character password (e.g., abcd efgh ijkl mnop).
        Copy this password immediately. You will not see it again.

3. Configure "Send mail as" in Gmail (Using SMTP)
    
        Now you will manually tell Gmail to use the SMTP server with your new App Password.
        
        Go back to your Gmail Settings: Settings (gear icon) > "See all settings" > "Accounts and Import" tab.
        
        In the "Send mail as" section, click "Add another email address."
        
        Enter the details:
        
        Name: Your name (e.g., "Bob Example")
        
        Email address: test@example.com
        
        Click "Next Step."
        
        Crucially, the next window should ask you for SMTP settings. Fill in the details:
        
        SMTP Server: smtp.gmail.com
        
        Port: 587 (or 465 if you prefer SSL, but 587/TLS is standard)
        
        Username: Your full primary Gmail address (e.g., bob@gmail.com)
        
        Password: Paste the 16-character App Password you generated in Step 1.
        
        Check "Secured connection using TLS" (if using Port 587) or "Secured connection using SSL" (if using Port 465).
        
        Click "Add Account."
        
        This method bypasses the on-the-fly verification step because you are explicitly authenticating with Google using the App Password.
        Your address test@example.com should now appear in the list under "Send mail as," ready to use.

## Cloudflare Pages + Private Github Repo
