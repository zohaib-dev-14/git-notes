# Nginx Reverse Proxy Setup Guide (React & Ubuntu)

Yeh guide aapko Ubuntu par Nginx install karne, React app ke liye reverse proxy configure karne, aur website ko properly handle aur manage karne ke poore steps asaan alfaaz mein samjhati hai.

---

## 🚀 1. Installation & Initial Setup

Sab se pehle Ubuntu ke package manager ko update karein aur Nginx install karein:

```bash
sudo apt update
sudo apt install nginx
```

Check karein ke Nginx successfully chal raha hai ya nahi:
```bash
sudo systemctl status nginx
```

---

## 📂 2. Core Concepts (Folders & Permissions)

### Linux Control Room (`/etc`)
*   **/etc:** Yeh operating system ka setting/control room hai. Tamam software ki configuration settings yahan hoti hain.
*   **/etc/nginx:** Yeh Nginx server ka ghar aur uska dimaag hai.

### Storage vs Active Area
*   **sites-available/ (Almari):** Yahan aap apni websites ya proxies ki settings files bana kar save karte hain. Yahan file rakhne se Nginx use direct run nahi karta.
*   **sites-enabled/ (Shop Front):** Nginx sirf is folder ke andar majood files ko read aur run karta hai.

### File Permissions (`chmod +x`)
Agar terminal `sh: 1: vite: Permission denied` jaisa error de, to file ko executable banane ke liye yeh command chalate hain:
```bash
chmod +x node_modules/.bin/vite
```

---

## 🛠️ 3. Creating Nginx Configuration

`sites-available` folder mein apne project ke naam ki ek nayi file banayein (Yaad rahe: `nginx.conf` naam ki multiple files nahi banani, har project ka alag naam rakhein):

```bash
sudo nano /etc/nginx/sites-available/educational-institute.conf
```

Niche diya gaya complete aur optimized code paste karein (Is mein local testing ke liye headers aur auto-refresh dono fully working hain):

```nginx
server {
    listen 80;
    server_name localhost; # Agar public IP ya domain ho to yahan likhein

    location / {
        proxy_pass http://localhost:5173; # Address jahan aapki React app chal rahi hai

        # 1. Client Identity Headers (Backend ke liye zaroori hain)
        proxy_set_header Host \$host;
        proxy_set_header X-Real-IP \$remote_addr;
        proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto \$scheme;

        # 2. WebSocket Support (React/Vite ke Auto-Refresh / HMR ke liye zaroori hain)
        proxy_http_version 1.1;
        proxy_set_header Upgrade \$http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```
*File save karne ke liye: `Ctrl+O` phir `Enter`, aur baahir aane ke liye `Ctrl+X` dabein.*

---

## 🔗 4. Activating the Site (Symlink)

File banane ke baad use active karne ke liye uska ek shortcut (symlink) `sites-enabled` mein banana zaroori hai:

```bash
sudo ln -s /etc/nginx/sites-available/educational-institute.conf /etc/nginx/sites-enabled/
```

### ⚠️ Crucial Step: Default File Delete Karein
Nginx ki apni ek `default` file pehle se port 80 ko block karke rakhti hai. Use active area se hatana lazmi hai taake aapka naya code chale:

```bash
sudo rm /etc/nginx/sites-enabled/default
```

---

## ⚙️ 5. Testing & Running Nginx

Nginx ki configuration file mein koi syntax error hai ya nahi, yeh test karne ke liye:
```bash
sudo nginx -t
```
*Agar output mein `syntax is ok` aur `test is successful` aaye, to sab sahi hai.*

Ab changes ko apply karne ke liye Nginx ko **Reload** karein:
```bash
sudo systemctl reload nginx
```

---

## 🎯 6. Site Management & Operations

### Website ko Temporarily Band (Stop) Karna
Agar aap chahte hain ke aapki website band ho jaye lekin uska code safe rahe, to sirf active area se shortcut delete kar dein:
```bash
sudo rm /etc/nginx/sites-enabled/educational-institute.conf
sudo systemctl reload nginx
```

### Website ko Dobara Chalu (Run) Karna
Jab website ko dobara live karna ho, to bas shortcut dobara bana kar reload kar dein:
```bash
sudo ln -s /etc/nginx/sites-available/educational-institute.conf /etc/nginx/sites-enabled/
sudo systemctl reload nginx
```

### DevOps Tip: Restart vs Reload
*   `sudo systemctl reload nginx` 👉 **Best Option.** Server ko bina band kiye background mein nayi settings load karta hai. Users ka connection drop nahi hota.
*   `sudo systemctl restart nginx` 👉 **Hard Reset.** Pure Nginx service ko aik dafa mukammal band karke shuru se start karta hai.

---

## 🔍 Verification
Ab aapko browser mein `localhost:5173` likhne ki zaroorat nahi. Aap seedha sirf **`http://localhost`** enter karenge aur aapki React App chal paregi!
