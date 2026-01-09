# SMS Email Android App

An Android application that manages SMS messages received via email (from sms@dubline.com) with Microsoft 365 integration.

## Features

- 📧 Microsoft 365 email integration
- 📱 Receive SMS messages as email notifications
- 💬 View all SMS messages in an inbox
- ↩️ Reply to SMS using native Android SMS functionality
- 🔔 Push notifications for new messages
- 💾 Offline storage with Room database
- 🔄 Background email monitoring

## Prerequisites

- Android Studio Arctic Fox or later
- Android SDK 24 or higher
- Microsoft 365 account
- Azure AD app registration

## Setup

### 1. Azure AD App Registration

1. Go to [Azure Portal](https://portal.azure.com)
2. Navigate to **Azure Active Directory** > **App registrations**
3. Click **New registration**
4. Configure:
   - Name: "SMS Email App"
   - Supported account types: "Accounts in any organizational directory and personal Microsoft accounts"
   - Redirect URI: `msauth://com.example.smsemailapp/[YOUR_SIGNATURE_HASH]`
5. Grant API permissions:
   - `Mail.Read`
   - `User.Read`
6. Copy your **Application (client) ID**

### 2. Configure the App

1. Clone the repository: 
   ```bash
   git clone https://github.com/WeAreCode045/sms-email-android-app.git
   cd sms-email-android-app
   ```

2. Update `app/src/main/res/raw/auth_config.json` with your Azure AD client ID: 
   ```json
   {
     "client_id": "YOUR_CLIENT_ID_HERE",
     "redirect_uri": "msauth://com.example.smsemailapp/YOUR_SIGNATURE_HASH"
   }
   ```

3. Open the project in Android Studio

4.  Sync Gradle and build the project

### 3. Generate Signature Hash for Redirect URI

Run this command to get your signature hash: 

```bash
keytool -exportcert -alias androiddebugkey -keystore ~/. android/debug.keystore | openssl sha1 -binary | openssl base64
```

Default password for debug keystore: `android`

### 4. Permissions

The app requires the following permissions:
- `INTERNET` - For email API calls
- `SEND_SMS` - To send SMS replies
- `READ_SMS` - Optional, for SMS functionality
- `POST_NOTIFICATIONS` - For Android 13+ notification permissions

## Project Structure

```
app/
├── src/
│   ├── main/
│   │   ├── java/com/example/smsemailapp/
│   │   │   ├── data/
│   │   │   │   ├── SmsMessage.kt
│   │   │   │   ├── SmsMessageDao.kt
│   │   │   │   └── AppDatabase. kt
│   │   │   ├── service/
│   │   │   │   └── EmailService.kt
│   │   │   ├── worker/
│   │   │   │   └── EmailMonitorWorker.kt
│   │   │   ├── ui/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── InboxActivity.kt
│   │   │   │   ├── InboxViewModel.kt
│   │   │   │   ├── MessageDetailActivity.kt
│   │   │   │   └── SettingsActivity.kt
│   │   │   └── SmsEmailApplication.kt
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   ├── raw/
│   │   │   │   └── auth_config.json
│   │   │   └── values/
│   │   └── AndroidManifest.xml
│   └── test/
└── build.gradle.kts
```

## Usage

1. Launch the app
2. Go to **Settings**
3. Click **Sign in with Microsoft**
4. Grant permissions
5. The app will start monitoring your email for SMS messages from `sms@dubline.com`
6. Receive notifications for new SMS messages
7. View messages in the **Inbox**
8. Tap a message to view details and reply

## Technologies Used

- **Kotlin** - Programming language
- **Microsoft Graph API** - Email integration
- **MSAL (Microsoft Authentication Library)** - Authentication
- **Room Database** - Local storage
- **WorkManager** - Background tasks
- **Coroutines** - Asynchronous programming
- **LiveData & ViewModel** - MVVM architecture
- **Material Design** - UI components

## Architecture

The app follows MVVM (Model-View-ViewModel) architecture: 

- **Model**: Room database entities
- **View**: Activities and layouts
- **ViewModel**: Business logic and data management

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Microsoft Graph API documentation
- Android Developers documentation

## Roadmap

- [ ] Add message search functionality
- [ ] Implement message threading
- [ ] Add support for MMS attachments
- [ ] Dark mode support
- [ ] Multiple account support
- [ ] Export/backup messages

## Support

For issues and questions, please open an issue on GitHub. 

## Author

WeAreCode045

---

**Note**: This app requires a valid Microsoft 365 account and proper Azure AD app registration to function. 
