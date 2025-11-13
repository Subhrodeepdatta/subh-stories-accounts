# 🚀 Quick Setup Guide - Subh Stories Accounts

**Download this repo as ZIP and follow these simple steps to get your desktop app running!**

---

## 📋 What's Already Created

✅ `package.json` - All dependencies
✅ `main.js` - Electron main process
✅ `.gitignore` - Node ignores
✅ `README.md` - Full documentation

---

## 📦 Step 1: Download as ZIP

1. Click the green **"Code"** button at the top
2. Click **"Download ZIP"**
3. Extract the ZIP to your Desktop
4. Open the folder in VS Code or any code editor

---

## 📁 Step 2: Create These Files

Copy-paste the code below into new files:

### File: `index.html`
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

### File: `webpack.config.js`
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

### File: `.babelrc`
```json
{
  "presets": ["@babel/preset-react"]
}
```

### Create Folder: `src/`

### File: `src/index.js`
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

### File: `src/App.js`
```javascript
import React, { useState } from 'react';

function App() {
  const [clients, setClients] = useState([]);
  const [showAddClient, setShowAddClient] = useState(false);
  const [newClient, setNewClient] = useState({ name: '', email: '', phone: '' });

  const addClient = () => {
    if (newClient.name) {
      setClients([...clients, { ...newClient, id: Date.now(), projects: [] }]);
      setNewClient({ name: '', email: '', phone: '' });
      setShowAddClient(false);
    }
  };

  return (
    <div style={{
      background: 'linear-gradient(135deg, #F5F5DC 0%, #FFF9F2 100%)',
      minHeight: '100vh',
      padding: '40px',
      fontFamily: 'Arial, sans-serif'
    }}>
      <div style={{ maxWidth: '1200px', margin: '0 auto' }}>
        <header style={{
          background: 'linear-gradient(135deg, #3C366B 0%, #5E5A8D 100%)',
          padding: '30px',
          borderRadius: '16px',
          marginBottom: '30px',
          boxShadow: '0 8px 24px rgba(0,0,0,0.15)'
        }}>
          <h1 style={{color: '#FFD700', margin: 0, fontSize: '32px'}}>
            🎬 Subh Stories Accounts
          </h1>
          <p style={{color: '#FFF9F2', margin: '10px 0 0 0'}}>
            Modern Desktop Accounting Software
          </p>
        </header>

        <div style={{
          display: 'grid',
          gridTemplateColumns: 'repeat(auto-fit, minmax(250px, 1fr))',
          gap: '20px',
          marginBottom: '30px'
        }}>
          <div style={{
            background: 'white',
            padding: '25px',
            borderRadius: '16px',
            boxShadow: '0 4px 12px rgba(0,0,0,0.1)'
          }}>
            <h3 style={{color: '#3C366B', marginTop: 0}}>👥 Total Clients</h3>
            <p style={{fontSize: '36px', fontWeight: 'bold', color: '#FFD700', margin: 0}}>
              {clients.length}
            </p>
          </div>
          <div style={{
            background: 'white',
            padding: '25px',
            borderRadius: '16px',
            boxShadow: '0 4px 12px rgba(0,0,0,0.1)'
          }}>
            <h3 style={{color: '#3C366B', marginTop: 0}}>💰 Total Projects</h3>
            <p style={{fontSize: '36px', fontWeight: 'bold', color: '#FFD700', margin: 0}}>
              {clients.reduce((acc, c) => acc + c.projects.length, 0)}
            </p>
          </div>
        </div>

        <div style={{
          background: 'white',
          padding: '30px',
          borderRadius: '16px',
          boxShadow: '0 8px 24px rgba(0,0,0,0.12)'
        }}>
          <div style={{display: 'flex', justifyContent: 'space-between', alignItems: 'center', marginBottom: '20px'}}>
            <h2 style={{color: '#3C366B', margin: 0}}> Client Manager</h2>
            <button
              onClick={() => setShowAddClient(!showAddClient)}
              style={{
                background: 'linear-gradient(135deg, #FFD700 0%, #FFA500 100%)',
                color: '#232020',
                border: 'none',
                padding: '12px 24px',
                borderRadius: '12px',
                fontSize: '16px',
                fontWeight: 'bold',
                cursor: 'pointer',
                boxShadow: '0 4px 12px rgba(255,215,0,0.3)'
              }}
            >
              {showAddClient ? 'Cancel' : '+ Add Client'}
            </button>
          </div>

          {showAddClient && (
            <div style={{
              background: '#F5F5DC',
              padding: '20px',
              borderRadius: '12px',
              marginBottom: '20px'
            }}>
              <input
                type="text"
                placeholder="Client Name"
                value={newClient.name}
                onChange={(e) => setNewClient({...newClient, name: e.target.value})}
                style={{
                  width: '100%',
                  padding: '12px',
                  marginBottom: '10px',
                  borderRadius: '8px',
                  border: '2px solid #FFD700',
                  fontSize: '16px'
                }}
              />
              <input
                type="email"
                placeholder="Email"
                value={newClient.email}
                onChange={(e) => setNewClient({...newClient, email: e.target.value})}
                style={{
                  width: '100%',
                  padding: '12px',
                  marginBottom: '10px',
                  borderRadius: '8px',
                  border: '2px solid #FFD700',
                  fontSize: '16px'
                }}
              />
              <input
                type="tel"
                placeholder="Phone"
                value={newClient.phone}
                onChange={(e) => setNewClient({...newClient, phone: e.target.value})}
                style={{
                  width: '100%',
                  padding: '12px',
                  marginBottom: '10px',
                  borderRadius: '8px',
                  border: '2px solid #FFD700',
                  fontSize: '16px'
                }}
              />
              <button
                onClick={addClient}
                style={{
                  background: '#3C366B',
                  color: 'white',
                  border: 'none',
                  padding: '12px 24px',
                  borderRadius: '8px',
                  fontSize: '16px',
                  cursor: 'pointer'
                }}
              >
                Save Client
              </button>
            </div>
          )}

          {clients.length === 0 ? (
            <p style={{textAlign: 'center', color: '#666', padding: '40px'}}>
              No clients yet. Click "Add Client" to get started!
            </p>
          ) : (
            <div style={{display: 'grid', gap: '15px'}}>
              {clients.map(client => (
                <div key={client.id} style={{
                  background: '#FFF9F2',
                  padding: '20px',
                  borderRadius: '12px',
                  border: '2px solid #FFD700'
                }}>
                  <h3 style={{color: '#3C366B', margin: '0 0 10px 0'}}>{client.name}</h3>
                  <p style={{margin: '5px 0', color: '#666'}}>✉️ {client.email}</p>
                  <p style={{margin: '5px 0', color: '#666'}}>📞 {client.phone}</p>
                </div>
              ))}
            </div>
          )}
        </div>

        <footer style={{textAlign: 'center', marginTop: '40px', color: '#666'}}>
          <p>Made with ❤️ for Subh Stories</p>
        </footer>
      </div>
    </div>
  );
}

export default App;
```

---

## 🛠️ Step 3: Install Dependencies

Open Command Prompt in the project folder and run:

```bash
npm install
```

This will install all required packages (React, Electron, etc.)

---

## ⚡ Step 4: Build & Run

### Build the React app:
```bash
npx webpack
```

### Run the desktop app:
```bash
npm start
```

Your app will open! 🎉

---

## 📦 Step 5: Create Windows .exe

```bash
npm run dist
```

Your installer will be in the `dist/` folder:
```
dist/Subh Stories Accounts Setup 1.0.0.exe
```

Double-click to install and enjoy your custom desktop app!

---

## 🐛 Troubleshooting

**App won't start?**
- Make sure Node.js is installed: `node --version`
- Delete `node_modules` and run `npm install` again

**Build fails?**
- Check that all files are created in the right locations
- Make sure `src/` folder exists

**Need more features?**
- Check the full README.md for complete code with database, invoice generator, and analytics

---

## ✨ What's Included

✅ Modern luxury UI (beige + gold + indigo)
✅ Client management
✅ Basic dashboard
✅ Fully offline
✅ Ready for expansion

---

**Ready to expand?** Check README.md for complete features including:
- SQLite database storage
- Invoice PDF generator with logo upload
- Revenue analytics & charts
- Project tracking per client
- And much more!

---

🎉 **Congratulations! You now have a working desktop app!**
