# Bradken® Device Compliance Pages

Public-facing equipment certification pages hosted via GitHub Pages for Bradken® IoT devices sold in Chile, served as required by SUBTEL (Subsecretaría de Telecomunicaciones).

The index.html page is a single, self-contained HTML file that meets SUBTEL's requirement for publicly accessible, login-free device certification information. Pages are bilingual (Spanish primary, English secondary) and act as a Declaration of Conformance under Chilean telecommunications regulations.

---

## Repository structure

```
/
├── README.md
└── index.html
```

## Adding a new device

1. Copy the template file from `_template/index.html` into a new folder under `devices/`.
2. Rename the folder to match the device model (e.g. `devices/wcms-headunit-rev1/`).
3. Open `index.html` and replace all placeholder values (see **Fields to update** below).
4. Commit and push to `main` — the page goes live within ~2 minutes.

### Fields to update

Search the file for the following placeholders and replace them:

| Placeholder | Description |
|---|---|
| `SUBTEL-XXXX-XXXX` | SUBTEL certificate number |
| `DD/MM/AAAA` | Certification date, expiry date, lab name |
| `Gateway Rev1.0` / `Head_Unit Rev1.1` | Model designations |
| `MODEL-NAME` | Folder/URL slug |
| `v1.0` in footer | Document version |

---

## Current devices

| Product | Model — Gateway | Model — End Node | Folder | Status |
|---|---|---|---|---|
| Wireless Condition Monitoring System | Gateway Rev1.0 | Head_Unit Rev1.1 | `devices/wcms-rev1/` | 🟡 Pending certification |

Update this table whenever a new device is added or a certificate number is confirmed.

---

## RF summary

The current device family operates in the Sub-1 GHz ISM band using IEEE 802.15.4 with Frequency Hopping Spread Spectrum (FHSS).

| Parameter | Value |
|---|---|
| Frequency band | 902 – 927 MHz |
| Active channels | 64–128 (915.0 – 927.8 MHz, 200 kHz spacing) |
| Protocol | IEEE 802.15.4 — TI 15.4 Stack (FHSS mode) |
| PHY | 5 kbps SimpleLink Long Range (SLR) |
| TX power | +13 dBm (~20 mW) — end nodes |
| EIRP | 6 dBm |
| Emission designation | 32K0F1D |
| Duplex | Half-duplex |
| Duty cycle | Low (~4 hr measurement/transmit interval per node) |
| Chipset | Texas Instruments CC1352R1 |

---

## Hosting

This repository is served via **GitHub Pages** from the `main` branch, root directory.

**Settings → Pages → Source:** Deploy from branch `main`, folder `/`

The live base URL is:
```
https://[org].github.io/device-compliance/
```

### QR code generation

QR codes printed on device labels should point to the specific device folder URL, e.g.:

```
https://[org].github.io/device-compliance/devices/wcms-rev1/
```

Generate QR codes using error correction level **M or Q** to ensure reliable scanning on labels that may be exposed to scratches or dust in industrial environments. Minimum printed size is **1.5 cm × 1.5 cm**.

To generate programmatically:

```python
pip install qrcode[pil]
```

```python
import qrcode

url = "https://[org].github.io/device-compliance/devices/wcms-rev1/"

qr = qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_M)
qr.add_data(url)
qr.make(fit=True)
img = qr.make_image()
img.save("wcms-rev1-qr.png")
```

---

## Updating an existing page

Because the QR code URL never changes, you can update the page content at any time without reprinting labels:

1. Edit the relevant `devices/[model]/index.html` directly in GitHub (pencil icon) or via a local clone.
2. Commit to `main`.
3. Changes are live within ~2 minutes.

This is the recommended approach when a SUBTEL certificate number or expiry date needs updating after initial label production.

---

## Brand

Pages use the Bradken® brand system per the corporate style guide:

- **Colours:** Bradken Blue `#005596`, Dark Navy `#00305F`, Grey `#939598`, Orange `#F47B29`
- **Typography:** Arial (web-safe, per Bradken style guide web guidance)
- **Logo:** Bradken® landscape logo embedded as base64 (no external dependencies)

All pages are fully self-contained — no CDN, no external fonts, no JavaScript. This ensures they remain accessible even in low-connectivity environments such as mine sites.

---

## Contact

Technical queries: digitalsupport@bradken.com  
Chilean importer: BRADKEN CHILE LTDA. — RUT 76.980.920-1  
Manufacturer: Bradken® Pty Limited — ABN 33 108 693 009 — 20 McIntosh Drive, Mayfield West NSW 2304, Australia
