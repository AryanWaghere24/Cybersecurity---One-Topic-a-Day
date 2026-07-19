# Day 50 - OAuth Phishing

## What It Is
OAuth Phishing is a modern phishing technique that abuses the OAuth authorization framework — the system that powers "Sign in with Google", "Sign in with Microsoft", and "Connect with Facebook" buttons across the web. Instead of stealing your password directly, OAuth phishing tricks you into granting a malicious third-party application access to your account. Since you authorize the app through a legitimate OAuth consent screen on the real platform, no fake login page is needed — the victim authenticates on the genuine website and MFA passes normally. The attacker ends up with persistent access to the victim's account without ever knowing their password.

## How It Works
OAuth is a legitimate authorization protocol that lets you grant third-party apps limited access to your accounts without sharing your password. OAuth phishing abuses the consent grant step of this process.

```
How legitimate OAuth works:
1. You click "Sign in with Google" on a third-party app
2. Google shows you a consent screen listing what the app wants access to
3. You click "Allow"
4. The app receives an access token — can act on your behalf within those permissions
5. Your password was never shared with the third-party app

How OAuth phishing works:
1. Attacker registers a malicious app with a convincing name
   "Google Drive File Viewer", "Office 365 Security Scanner"
2. Sends victim a phishing email or message:
   "Your shared document is ready — click to view"
3. Victim clicks and is taken to a REAL Google/Microsoft consent screen
4. Consent screen shows the malicious app requesting permissions:
   "This app wants to: Read your emails, Access your contacts,
    Send emails on your behalf"
5. Victim sees a real Google URL, passes MFA normally, clicks Allow
6. Attacker now has persistent OAuth token — full account access
   without ever knowing the victim's password or MFA code
7. Access persists even if victim changes their password
```
