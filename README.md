# Removing Git Credentials from Stretch Before Customer Deployment

Use this guide before handing a robot to a customer to remove all GitHub authentication and personal Git credentials.

---

## 1. Log Out of GitHub CLI

Check status:

```bash
gh auth status
```

If logged in, log out:

```bash
gh auth logout
```

Verify:

```bash
gh auth status
```

You should see that you are not logged in.

## 2. Remove Stored HTTPS Credentials

Check if a credential helper is configured:

```bash
git config --global credential.helper
```

If it returns:

```bash
store
```

Then credentials are saved in `~/.git-credentials`. Remove them:

```bash
rm ~/.git-credentials
```

Remove the credential helper:

```bash
git config --global --unset credential.helper
```

Verify:

```bash
git config --global credential.helper
```

It should return nothing.

## 3. Remove SSH Keys (If Present)

Check SSH directory:

```bash
ls ~/.ssh
```

If you see private keys such as:

```bash
id_rsa
id_ed25519
```

Remove them:

```bash
rm ~/.ssh/id_rsa*
rm ~/.ssh/id_ed25519*
```

Do NOT remove:

```bash
known_hosts
```

## 4. Remove Global Git Identity (If Present)

Check configured name and email:

```bash
git config --global user.name
git config --global user.email
```

If they show your credentials, remove them:

```bash
git config --global --unset user.name
git config --global --unset user.email
```

## 5. Final Verification Checklist

Run:

```bash
gh auth status
git config --global credential.helper
ls ~/.ssh
git config --global user.name
git config --global user.email
```

Confirm:

* Not logged into GitHub CLI

* No credential helper configured

* No private SSH keys present

* No Git `user.name` or `user.email` set# Remove-Git-Credentials
