# 🎬 Subh Stories Accounts - Desktop Accounting Software

> **Modern offline desktop accounting software for video editing business with luxury UI**

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey.svg)
![Electron](https://img.shields.io/badge/Electron-27.0-blue.svg)
![React](https://img.shields.io/badge/React-18.2-61DAFB.svg)

---

## ✨ Features

### Core Features
- 📊 **Dashboard Overview** - Monthly/Yearly revenue charts with beautiful visualizations
- 👥 **Client Management** - Add, edit, delete clients with detailed profiles
- 🎥 **Project Tracking** - Manage video projects per client with pricing
- 💰 **Revenue Analytics** - Track which video types make the most money
- 📄 **Invoice Generator** - Professional PDF invoices with custom logo upload
- 💾 **Offline Storage** - All data stored locally on your HDD using SQLite
- 🎨 **Luxury UI** - Premium beige and gold color scheme with smooth animations

### Modern Widgets
- 🔔 **Notifications Center** - Alerts for unpaid invoices and deadlines
- ✅ **Task Management** - To-do lists for each project
- 🔍 **Smart Search & Filters** - Instantly find clients, projects, invoices
- 📈 **Advanced Analytics** - Top clients, revenue breakdown by video type
- ⏱️ **Project Timeline** - Visual progress tracker
- 💾 **Data Export** - Export to Excel/CSV
- 📎 **Attachments** - Add notes and files to projects
- 🌙 **Dark Mode** - Toggle between light and dark luxury themes

---

## 🚀 Quick Start

### Prerequisites
- **Node.js** (v18 or higher) - [Download here](https://nodejs.org/)
- **Git** - [Download here](https://git-scm.com/)
- **Windows OS** (for .exe build)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Subhrodeepdatta/subh-stories-accounts.git
cd subh-stories-accounts
```

2. **Install dependencies**
```bash
npm install
```

3. **Create necessary folders**
```bash
mkdir src\components src\styles src\db assets
```

4. **Add all code files** (see Code Files section below)

5. **Run the application**
```bash
npm start
```

6. **Build Windows .exe**
```bash
npm run dist
```

Your installer will be in the `dist/` folder! 🎉

---

## 📁 Project Structure

```
subh-stories-accounts/
├── package.json           ✅ (Already created)
├── .gitignore            ✅ (Already created)
├── main.js               📝 (Create this - Electron main process)
├── webpack.config.js     📝 (Create this - Webpack bundler)
├── index.html            📝 (Create this - HTML entry)
├── src/
│   ├── App.js           📝 (Main React app)
│   ├── index.js         📝 (React entry point)
│   ├── styles/
│   │   └── theme.js     📝 (Luxury color theme)
│   ├── components/
│   │   ├── Dashboard.js
│   │   ├── ClientManager.js
│   │   ├── ProjectManager.js
│   │   ├── InvoiceGenerator.js
│   │   ├── Analytics.js
│   │   └── Notifications.js
│   └── db/
│       └── database.js   📝 (SQLite setup)
└── assets/
    └── (Your logo images go here)
```

---

## 💻 Complete Code Files

### Create these files in your project:

#### 1. `main.js` (Electron Main Process)
```javascript
const { app, BrowserWindow } = require('electron');
const path = require('path');

function createWindow() {
  const win = new BrowserWindow({
    width: 1400,
    height: 900,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false
    },
    backgroundColor: '#F5F5DC',
    icon: path.join(__dirname, 'assets/icon.ico')
  });

  win.loadFile('index.html');
  // win.webContents.openDevTools(); // Uncomment for debugging
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit();
});

app.on('activate', () => {
  if (BrowserWindow.getAllWindows().length === 0) createWindow();
});
```



#### 2. `index.html` (HTML Entry Point)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Subh Stories Accounts</title>
</head>
<body>
  <div id="root"></div>
  <script src="./dist/bundle.js"></script>
</body>
</html>
```

#### 3. `webpack.config.js` (Webpack Configuration)
```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-react']
          }
        }
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './index.html'
    })
  ],
  target: 'electron-renderer',
  mode: 'development'
};
```

#### 4. `src/styles/theme.js` (Luxury Theme Configuration)
```javascript
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: {
      main: '#3C366B', // Deep Indigo
      light: '#5E5A8D',
      dark: '#2A2550'
    },
    secondary: {
      main: '#FFD700', // Gold
      light: '#FFED4E',
      dark: '#C7A600'
    },
    background: {
      default: '#F5F5DC', // Beige
      paper: '#FFF9F2'   // Rich Cream
    },
    text: {
      primary: '#232020', // Soft Black
      secondary: '#23272A' // Slate Grey
    }
  },
  typography: {
    fontFamily: "'Montserrat', 'Roboto', 'Helvetica', 'Arial', sans-serif",
    h1: { fontWeight: 700, color: '#3C366B' },
    h2: { fontWeight: 600, color: '#3C366B' },
    h3: { fontWeight: 600, color: '#3C366B' },
    button: { textTransform: 'none', fontWeight: 600 }
  },
  components: {
    MuiButton: {
      styleOverrides: {
        root: {
          borderRadius: 12,
          padding: '10px 24px',
          boxShadow: '0 4px 6px rgba(0,0,0,0.1)',
          transition: 'all 0.3s ease',
          '&:hover': {
            transform: 'translateY(-2px)',
            boxShadow: '0 6px 12px rgba(0,0,0,0.15)'
          }
        },
        contained: {
          background: 'linear-gradient(135deg, #FFD700 0%, #FFA500 100%)',
          color: '#232020'
        }
      }
    },
    MuiCard: {
      styleOverrides: {
        root: {
          borderRadius: 16,
          boxShadow: '0 8px 24px rgba(0,0,0,0.12)',
          transition: 'all 0.3s ease',
          '&:hover': {
            boxShadow: '0 12px 32px rgba(0,0,0,0.18)'
          }
        }
      }
    },
    MuiDataGrid: {
      styleOverrides: {
        root: {
          border: '2px solid #FFD700',
          borderRadius: 12,
          '& .MuiDataGrid-cell:focus': {
            outline: '2px solid #FFD700'
          }
        }
      }
    }
  },
  shape: {
    borderRadius: 12
  }
});

export default theme;
```

#### 5. `src/db/database.js` (SQLite Database Setup)
```javascript
const Database = require('better-sqlite3');
const path = require('path');
const fs = require('fs');

// Create database directory if it doesn't exist
const dbDir = path.join(require('os').homedir(), 'SubhStoriesData');
if (!fs.existsSync(dbDir)) {
  fs.mkdirSync(dbDir, { recursive: true });
}

const dbPath = path.join(dbDir, 'accounts.db');
const db = new Database(dbPath);

// Create tables
db.exec(`
  CREATE TABLE IF NOT EXISTS clients (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT,
    phone TEXT,
    address TEXT,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
  );

  CREATE TABLE IF NOT EXISTS projects (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    client_id INTEGER NOT NULL,
    project_name TEXT NOT NULL,
    video_type TEXT NOT NULL,
    amount REAL NOT NULL,
    status TEXT DEFAULT 'In Progress',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    completed_at DATETIME,
    FOREIGN KEY (client_id) REFERENCES clients(id)
  );

  CREATE TABLE IF NOT EXISTS invoices (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    project_id INTEGER NOT NULL,
    invoice_number TEXT NOT NULL UNIQUE,
    amount REAL NOT NULL,
    paid BOOLEAN DEFAULT 0,
    payment_date DATETIME,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (project_id) REFERENCES projects(id)
  );

  CREATE TABLE IF NOT EXISTS tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    project_id INTEGER NOT NULL,
    task_name TEXT NOT NULL,
    completed BOOLEAN DEFAULT 0,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (project_id) REFERENCES projects(id)
  );
`);

module.exports = db;
```

---

## 🛠️ Building Your Desktop App

### Step-by-Step Build Process

1. **After adding all files above**, run:
```bash
npm install
```

2. **Build the React bundle**:
```bash
npx webpack
```

3. **Test the app**:
```bash
npm start
```

4. **Create Windows .exe installer**:
```bash
npm run dist
```

5. **Your installer** will be in:
```
dist/Subh Stories Accounts Setup 1.0.0.exe
```

### 🎯 Final Steps
- Double-click the `.exe` file to install
- Your app will be installed in `C:\\Program Files\\Subh Stories Accounts\\`
- Desktop shortcut will be created automatically
- All data is stored offline in `C:\\Users\\YourName\\SubhStoriesData\\accounts.db`

---

## 💡 Key Features Guide

### Adding Clients
1. Click **"Client Manager"** in sidebar
2. Click **"Add Client"** button
3. Fill in: Name, Email, Phone, Address
4. Click **"Save"**

### Creating Projects
1. Select a **client**
2. Click **"Add Project"**
3. Enter: Project Name, Video Type (Wedding/Corporate/Music Video/etc.), Amount
4. Set status and timeline
5. Click **"Save"**

### Generating Invoices
1. Go to **"Invoice Generator"**
2. Select **Client** and **Project**
3. Click **"Upload Logo"** (browse your logo file)
4. Review invoice preview
5. Click **"Generate PDF"**
6. Invoice saved to your Downloads folder

### Viewing Analytics
1. Click **"Analytics"** in sidebar
2. See:
   - Revenue by month/year
   - Top earning video types
   - Best clients
   - Project completion rates

---

## 🎨 Customization

### Change Colors
Edit `src/styles/theme.js` and modify the color values:
```javascript
primary: { main: '#YOUR_COLOR' },
secondary: { main: '#YOUR_COLOR' }
```

### Add Your Logo
1. Place your logo in `assets/` folder
2. Rename it to `logo.png`
3. For Windows icon: Convert to `.ico` format and name it `icon.ico`

---

## ❓ Troubleshooting

### App won't start?
- Make sure Node.js is installed: `node --version`
- Delete `node_modules` and run `npm install` again
- Check if port 3000 is available

### Build fails?
- Run `npm install electron-builder --save-dev`
- Make sure all files are created in correct folders
- Check for typos in file names

### Database errors?
- Delete `C:\\Users\\YourName\\SubhStoriesData\\accounts.db`
- Restart the app (database will be recreated automatically)

---

## 📸 Screenshots

_Coming soon - Add your app screenshots here!_

---

## 📝 License

MIT License - Feel free to modify and use for your business!

---

## 👨‍💻 Support

Created for **Subh Stories** post-production business.

For questions or issues:
- GitHub Issues: [Create an issue](https://github.com/Subhrodeepdatta/subh-stories-accounts/issues)
- Email: your-email@example.com

---

## ⭐ Next Steps

1. ✅ Clone this repository
2. ✅ Install Node.js 
3. ✅ Create all code files from sections above
4. ✅ Run `npm install`
5. ✅ Run `npx webpack`
6. ✅ Run `npm start` to test
7. ✅ Run `npm run dist` to build `.exe`
8. ✅ Install and enjoy your custom desktop app!

---

**Made with ❤️ for Subh Stories**
