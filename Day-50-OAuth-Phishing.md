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

Why OAuth phishing bypasses traditional defenses:
```
- No fake login page — victim authenticates on the REAL platform
- MFA is completely bypassed — victim completes it themselves
- Password change doesn't revoke access — token persists
- Looks legitimate — real Google/Microsoft consent screen shown
- Email security tools don't flag OAuth consent URLs as malicious
```
## Real-World Example
In 2017 a massive OAuth phishing campaign targeted over one million Gmail users. Victims received emails appearing to be from a known contact sharing a Google Doc. Clicking opened a real Google OAuth consent screen for an app called "Google Docs" — but it was a malicious third-party app, not the real Google Docs. Victims saw the familiar Google interface, granted permissions, and the attacker's app immediately gained access to their Gmail contacts and sent the same phishing email to everyone in their contact list — self-propagating like a worm entirely through legitimate OAuth grants. Google shut it down within an hour but not before it spread to over a million accounts.

## Why It Matters
From an attacker's side, OAuth phishing is one of the most sophisticated modern phishing techniques because it completely bypasses password theft and MFA — the two most commonly recommended defenses against phishing. Persistent access tokens mean the attacker maintains access even after the victim resets their password, and the attack leaves minimal traces in traditional security logs since all authentication was legitimate.

From a defender's side, organizations should restrict which OAuth apps employees can grant access to — enterprise Google Workspace and Microsoft 365 both have admin controls to whitelist approved apps and block unapproved ones. Users should carefully read OAuth consent screens before clicking Allow — check the app name, the developer, and specifically what permissions are being requested. Periodically reviewing and revoking OAuth app permissions in your account settings removes any previously granted malicious access.

## Key Terms
- OAuth (Open Authorization): a standard protocol allowing third-party applications to access user accounts without sharing passwords
- OAuth Consent Screen: the page shown by Google, Microsoft, or other platforms listing what permissions a third-party app is requesting
- Access Token: a credential issued after OAuth authorization that allows the app to act on the user's behalf within granted permissions
- Consent Phishing: another name for OAuth phishing — tricking users into granting malicious app permissions through legitimate consent screens
- Token Persistence: OAuth tokens remain valid even after password changes, giving attackers persistent access until the token is explicitly revoked

## One Tip / Tool

Tool: Regularly audit and revoke OAuth app permissions through your account security settings

```
How to review and revoke OAuth app access:

Google:
1. Go to myaccount.google.com/security
2. Scroll to "Third-party apps with account access"
3. Review every app listed — revoke anything unrecognized or unused

Microsoft:
1. Go to myapps.microsoft.com
2. Click on any app → Manage your application
3. Review permissions and revoke as needed
