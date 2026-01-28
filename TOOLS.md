# TOOLS.md - Local Notes

## What Goes Here

Things like:
- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras
- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH
- home-server → 192.168.1.100, user: admin

### TTS
- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

---

## GitHub Tokens

### BrunoBianchi/ObsidianNotesync
- **Personal Access Token:** [REMOVED - Use GitHub token storage or environment variable]
- **Created:** 2026-01-27
- **Permissions:** repo (full control)
- **Note:** Token removed for security. Use `git credential-store` or environment variables.
- **Action:** Generate new token when needed via GitHub Settings > Developer Settings

---

## Clawdbot Configuration

### Google Calendar Integration (AWS)
The Clawdbot can create calendar events automatically.

#### Environment
- **Platform:** AWS (remote server)
- **Bot Location:** Running on cloud instance
- **Authentication:** Google OAuth 2.0

#### Step 1: Install Dependencies
```bash
# In AWS terminal where Clawdbot is running
npm install googleapis
```

#### Step 2: Create credentials.json
Create `credentials.json` file with your OAuth credentials:

```json
{
  "installed": {
    "client_id": "your-client-id.apps.googleusercontent.com",
    "project_id": "your-project-id",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_secret": "your-client-secret"
  },
  "tokens": {
    "access_token": "your-access-token",
    "refresh_token": "your-refresh-token",
    "token_type": "Bearer",
    "expiry_date": 1234567890000
  }
}
```

**Create on AWS:**
```bash
# Method 1: Create file directly
nano credentials.json
# Paste content, save (Ctrl+O), exit (Ctrl+X)

# Method 2: Use heredoc
cat > credentials.json << 'EOF'
{ paste JSON here }
EOF
```

#### Step 3: Create setup-auth.js
Create `setup-auth.js` for initial authorization:

```javascript
const fs = require('fs');
const path = require('path');
const { google } = require('googleapis');

// SCOPES
const SCOPES = ['https://www.googleapis.com/auth/calendar'];

const TOKEN_PATH = path.join(__dirname, 'token.json');
const CREDENTIALS_PATH = path.join(__dirname, 'credentials.json');

function authorize(credentials) {
  const { client_secret, client_id, redirect_uris } = credentials.installed;
  const oAuth2Client = new google.auth.OAuth2(
    client_id,
    client_secret,
    redirect_uris[0]
  );

  console.log('⚠️  AUTH REQUIRED ⚠️');
  console.log('1. Open this link in your local browser:');
  console.log(oAuth2Client.generateAuthUrl({
    access_type: 'offline',
    scope: SCOPES,
  }));
  console.log('2. Login with bruno.riadianobianchi@gmail.com');
  console.log('3. If "App not verified", click Advanced -> Go to Clawdbot (unsafe)');
  console.log('4. Paste the code that appears and click below:');

  const rl = require('readline').createInterface({
    input: process.stdin,
    output: process.stdout
  });

  rl.question('Paste code here: ', (code) => {
    rl.close();
    oAuth2Client.getToken(code, (err, token) => {
      if (err) return console.error('Error getting token:', err);
      oAuth2Client.setCredentials(token);
      fs.writeFileSync(TOKEN_PATH, JSON.stringify(token));
      console.log('✅ Success! token.json file created. Bot now has vital access.');
    });
  });
}

authorize(JSON.parse(fs.readFileSync(CREDENTIALS_PATH)));
```

**Execute on AWS:**
```bash
node setup-auth.js
```

Follow the prompts to authorize and create `token.json`.

#### Step 4: Create calendar-module.js
Create `calendar-module.js` for calendar operations:

```javascript
const fs = require('fs');
const path = require('path');
const { google } = require('googleapis');

const TOKEN_PATH = path.join(__dirname, 'token.json');
const CREDENTIALS_PATH = path.join(__dirname, 'credentials.json');

async function getAuth() {
  const credentials = JSON.parse(fs.readFileSync(CREDENTIALS_PATH));
  const { client_secret, client_id, redirect_uris } = credentials.installed;
  const token = JSON.parse(fs.readFileSync(TOKEN_PATH));

  const oAuth2Client = new google.auth.OAuth2(
    client_id,
    client_secret,
    redirect_uris[0]
  );
  oAuth2Client.setCredentials(token);
  return oAuth2Client;
}

async function scheduleEvent(titulo, descricao, dataInicio) {
  try {
    const auth = await getAuth();
    const calendar = google.calendar({ version: 'v3', auth });

    // Set duration (30 min example)
    const start = new Date(dataInicio);
    const end = new Date(start.getTime() + 30 * 60000); // +30 min

    const event = {
      summary: `🤖 ${titulo}`,
      description: descricao,
      start: { dateTime: start.toISOString() },
      end: { dateTime: end.toISOString() },
      colorId: '5', // 5 = Yellow (easy to see)
    };

    const res = await calendar.events.insert({
      calendarId: 'primary', // Use your main calendar
      resource: event,
    });

    console.log(`📅 Event created: ${res.data.htmlLink}`);
    return res.data.htmlLink;

  } catch (error) {
    console.error('Error creating event:', error);
    throw error;
  }
}

// Export for use in main script
module.exports = { scheduleEvent };
```

#### Step 5: Use in Main Bot Script
In your `linkedin-automation.js` (or main bot script):

```javascript
const { scheduleEvent } = require('./calendar-module');

// ... your existing code ...

// Example usage
if (followSuccessful) {
  console.log("Follow successful. Scheduling reminder...");

  // Schedule reminder 3 days from now
  const dataLembrete = new Date();
  dataLembrete.setDate(dataLembrete.getDate() + 3);

  const eventLink = await scheduleEvent(
    "Verificar conexão LinkedIn: Tech Recruiter",
    "O Clawdbot seguiu este perfil há 3 dias. Verifique se aceitou para enviar mensagem.",
    dataLembrete
  );

  console.log(`📅 Calendar event created: ${eventLink}`);
}
```

---

## Cron Job Configuration

The `Git Sync Check - ObsidianNotesync` cron job checks for changes every 5 minutes.

### Location
- **System:** Clawdbot
- **Job Name:** Git Sync Check - ObsidianNotesync
- **Schedule:** Every 5 minutes
- **Function:** Check for Git changes and notify

### Command
```bash
cd /home/ubuntu/clawd/ObsidianNotesync && git pull origin main
```

### Notification
If changes detected, notify via Telegram (channel=telegram, target=7683172303).

---

Add whatever helps you do your job. This is your cheat sheet.
