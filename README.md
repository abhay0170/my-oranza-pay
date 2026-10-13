# My Oranza Pay

An installable web app that shows a UPI payment QR. You set the UPI ID, payee name, amount and note; the QR updates as you type. Settings stay on the device.

## Put it online (needs HTTPS to install)

Upload everything in this folder, as is, to any static host:

- **Netlify Drop**: open app.netlify.com/drop and drag this folder in.
- **GitHub Pages**: push the files to a repo, then Settings > Pages > deploy from the main branch.
- **Firebase Hosting**: `firebase init hosting` (public dir = this folder), then `firebase deploy`.
- **Azure Static Web Apps** or an Azure Storage static website also work.

## Using pay.myoranza.in alongside the Odoo site

1. Deploy this folder to Netlify, Cloudflare Pages or GitHub Pages and add the custom domain `pay.myoranza.in` there.
2. Where the myoranza.in DNS is managed, add a CNAME record: name `pay`, value = the address the host gives you.
3. Optional: in Odoo (developer mode), Website > Configuration > Redirects, add a 301 from `/pay` to `https://pay.myoranza.in`.

The Odoo site at www.myoranza.in is not affected.

## Install on a phone

Open the site in Chrome on Android and tap **Install app** (or menu > Add to Home screen). On iPhone, use Safari > Share > Add to Home Screen.

## Files

- `l/index.html` - the page customers see when they open a pay link
- `index.html` - the whole app, QR generator included, so it works offline
- `manifest.webmanifest` - name, colours and icons for installing
- `sw.js` - service worker that caches the app for offline use
- `icon-*.png`, `apple-touch-icon.png` - home-screen icons

Pay links look like `https://pay.myoranza.in/l/?am=499.00&tn=Bill%201042`. The customer page always pays the UPI ID set in `CONFIG` at the bottom of `l/index.html`.

If you change `index.html` later, bump `CACHE` in `sw.js` (e.g. `v2`) so phones pick up the new version.
