# 🐧 Linux Server Typography & Font Cache Installation Guide

A production-grade guide for installing, configuring, and caching open-source fonts across Linux distributions, Docker containers, and headless browser clusters (Puppeteer, Playwright, Chromium).

---

## 🚀 1. Ubuntu / Debian / Raspberry Pi OS

```bash
# 1. Update fontconfig and curl
sudo apt-get update && sudo apt-get install -y fontconfig curl unzip

# 2. Create the system font directory
sudo mkdir -p /usr/local/share/fonts/opentypography

# 3. Download and extract any archive (e.g. Bangla or English)
curl -L -o bangla-fonts.zip https://github.com/mohammadgolamrabbii/Bangla-Fonts-Mega-Collection/archive/refs/tags/v1.0.0.zip
sudo unzip -j bangla-fonts.zip "*.ttf" "*.otf" -d /usr/local/share/fonts/opentypography/

# 4. Set secure read permissions
sudo chmod 644 /usr/local/share/fonts/opentypography/*

# 5. Refresh fontconfig cache
sudo fc-cache -f -v

# 6. Verify installation
fc-list : family | grep -E "SolaimanLipi|Kalpurush|Inter"
```

---

## 🏔️ 2. Alpine Linux (Ultra-light Docker Images)

```dockerfile
FROM alpine:latest

# Install fontconfig & freetype
RUN apk add --no-cache fontconfig freetype curl

# Install Open Typography Fonts
RUN mkdir -p /usr/share/fonts/truetype/opentypography && \
    curl -L -o /tmp/english.zip https://github.com/mohammadgolamrabbii/English-Fonts-Mega-Archive/archive/refs/tags/v1.0.0.zip && \
    unzip -q /tmp/english.zip -d /tmp/ && \
    find /tmp/ -name "*.ttf" -o -name "*.otf" | xargs -I {} cp {} /usr/share/fonts/truetype/opentypography/ && \
    fc-cache -f && \
    rm -rf /tmp/*
```

---

## 🎩 3. Red Hat / CentOS / AlmaLinux / Rocky Linux

```bash
sudo yum install -y fontconfig curl unzip
sudo mkdir -p /usr/share/fonts/opentypography
# (Extract fonts into /usr/share/fonts/opentypography)
sudo fc-cache -f -v
```

---

## 🧪 4. Headless Puppeteer / Chromium Verification
For PDF generators, screenshot bots, and SSR services:
```javascript
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch({
    args: ['--no-sandbox', '--font-render-hinting=medium']
  });
  const page = await browser.newPage();
  await page.setContent('<h1 style="font-family: \'Kalpurush\', sans-serif;">আমার সোনার বাংলা আমি তোমায় ভালোবাসি</h1>');
  await page.pdf({ path: 'typography-test.pdf', format: 'A4' });
  await browser.close();
  console.log('PDF rendered with native typography successfully.');
})();
```

Maintained by **[Mohammad Golamrabbii](https://linktr.ee/golamrabbii)**.
