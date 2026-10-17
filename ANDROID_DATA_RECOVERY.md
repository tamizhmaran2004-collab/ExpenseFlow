# Android data recovery

ExpenseFlow stores its records in the Android app's private WebView storage. The Android manifest enables Auto Backup and includes app-private files for cloud backup and device-to-device transfer.

## Automatic recovery

- For an ordinary update, install the new APK over the existing app. Do not uninstall first; an in-place update keeps the app's private data.
- For an uninstall/reinstall or a new phone, enable Android/Google device backup and use the same Google account or Android device-transfer flow. Android controls when backups run and whether they are available to restore.
- Android only accepts an APK update when its package ID and signing certificate match the installed app. Keep the release keystore safe and use it for every later build.

## Portable backup

Before uninstalling, open **More → Back up data** and save the JSON file somewhere outside the app, such as Drive or Documents. After reinstalling, use **More → Restore backup** and select that file. The file contains ExpenseFlow data, including locally stored settings and API keys; keep it private.

## Persistent GitHub Actions signing

The APK workflow uses a persistent release keystore when these GitHub Actions repository secrets are configured:

- `EXPENSEFLOW_KEYSTORE_BASE64`
- `EXPENSEFLOW_KEYSTORE_PASSWORD`
- `EXPENSEFLOW_KEY_ALIAS`
- `EXPENSEFLOW_KEY_PASSWORD`

Store the keystore itself in a secure place and do not commit it. When these secrets are absent, CI falls back to a debug APK; debug APK signing is not suitable as a long-term update identity. A new release key cannot replace the signing key of an already installed build without a one-time uninstall/migration.
