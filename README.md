# website-setup-guide

## Cloudflare + Brevo + Gmail

Since you're using a Cloudflare forwarder and not a full email hosting provider, the professional, free way to proceed is to explicitly configure Gmail to send the email using Brevo SMTP server.

Here is the revised, professional process to add your address:

1. Setup a free Brevo Account and Authenticate DNS

        Sign up for a free Brevo account and follow all Brevo directions to authenticate the domain via DNS.

        While updating DNS, set the following TXT record "v=spf1 include:spf.brevo.com include:_spf.mx.cloudflare.net ~all"
        
        NEXT, [Brevo SMTP Settings](https://app.brevo.com/settings/keys/smtp)
        
        Click "Generate."
        
        Copy this password immediately. You will not see it again. You'll need it in the next steps


3. Configure "Send mail as" in Gmail (Using SMTP)
    
        Now you will manually tell Gmail to use the SMTP server with your new Brevo SMTP Key.
        
        Go back to your Gmail Settings: Settings (gear icon) > "See all settings" > "Accounts and Import" tab.
        
        In the "Send mail as" section, click "Add another email address."
        
        Enter the details:
        
        Name: Your name (e.g., "Bob Example")
        
        Email address: test@example.com

        Select "Alias"
        
        Click "Next Step."
        
        Crucially, the next window should ask you for SMTP settings. Fill in the details from Brevo SMTP page
        
        Check "Secured connection using TLS" (if using Port 587) or "Secured connection using SSL" (if using Port 465).
        
        Click "Add Account."
        
        Your address test@example.com should now appear in the list under "Send mail as," ready to use.

        Send a test email to check@dmarcly.com with the subject test, wait for a response to verify.

## Cloudflare Pages + Private Github Repo
