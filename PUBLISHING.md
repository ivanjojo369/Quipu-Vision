# Publishing checklist

1. Confirm you are using the intended GitHub account (repository owner).
2. Create an EMPTY public repository `Quipu-Vision` in that account. Do not initialize
   it with README, .gitignore, or LICENSE (all of these are handled locally, except LICENSE).
3. Review every file staged here. In particular, make sure documentation, image files,
   and Python sources contain no passwords, private data, payment details, or keys.
4. Keep the source project inside `AegisForge_agent/Quipu-Vision/` unchanged.
   This directory is only a release snapshot, not a second development source.
5. From PowerShell in this publication directory:

```powershell
git init -b main
git add .
git status --short
git diff --cached --stat
# Inspect content before proceeding:
git diff --cached --check
# Only after reviewing:
git commit -m "Publish Quipu Vision 0.4.0 local MVP"
git remote add origin https://github.com/ivanjojo369/Quipu-Vision.git
git push -u origin main
```

If the repository owner is NOT `ivanjojo369`, replace the remote URL before pushing.
The `git push` requires you to authenticate to the correct GitHub account.

This standalone package does not include the full AegisForge server; to publish the
verified A2A web integration, push the corresponding tested changes to the original
AegisForge repository and link the exact release/commit from this README.
