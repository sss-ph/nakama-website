# NAKAMA5666 — Website

Static website สำหรับแบรนด์ผลิตภัณฑ์ดูแลรถยนต์ NAKAMA5666

🌐 **Live:** [nakamaauto.com](https://nakamaauto.com)

---

## โครงสร้างไฟล์

```
nakama5666/
├── index.html              → หน้าหลัก
├── products.html           → สินค้าทั้งหมด + Interactive Diagram
├── find-wiper.html         → ค้นหาขนาดใบปัด
├── about.html              → เกี่ยวกับเรา
├── components.html         → Navbar + Footer (inject ผ่าน JS)
├── assets/
│   ├── style.css           → CSS ทั้งหมด (Section 1–20)
│   ├── main.js             → JS หลัก (slider, products, modal)
│   ├── diagram.js          → Interactive Car/Moto Diagram
│   ├── wiper.js            → Wiper Size Finder
│   ├── i18n.js             → ระบบภาษา ไทย/EN (infrastructure พร้อม ยังไม่ได้ wire)
│   ├── data/
│   │   ├── products.json   → ข้อมูลสินค้า 18 รายการ
│   │   └── wiper-data.json → ข้อมูลขนาดใบปัด 108 รุ่น
│   └── images/
│       ├── logo/           → โลโก้แบรนด์ + โลโก้แพลตฟอร์ม
│       ├── hero/           → รูปพื้นหลัง Hero Slider (slide-1.png ถึง slide-4.png)
│       ├── merchant/       → รูปสินค้า
│       └── diagram/        → รูปรถ + มอไซค์ + หมวกกันน็อก
└── fonts/
    ├── DB Helvethaica X *.ttf     → Body font (Thai)
    └── Euclid Circular A *.ttf    → Display font (EN)
```

---

## Brand

| | |
|---|---|
| **สี** | `#d51428` (red), `#7e2100` (red-dark) |
| **Gradient** | `linear-gradient(135deg, #d51428, #7e2100)` |
| **Display Font** | Euclid Circular A (h1, h2, h3, ตัวเลข) |
| **Body Font** | DB Helvethaica X (ข้อความทั่วไป) |
| **Logo** | `assets/images/logo/NAKAMA TRANSPA@300x.png` |

---

## CSS Sections (style.css)

| Section | เนื้อหา |
|---------|---------|
| 1 | Variables & Reset |
| 2 | Typography (@font-face) |
| 3 | Utilities (btn, badge, divider) |
| 4 | Navbar (3-col layout: brand \| center \| shopee) |
| 5 | Footer |
| 6 | Hero Slider |
| 7 | Product Cards |
| 8 | Spray Highlight |
| 9 | Diagram Teaser |
| 10 | CTA Banner |
| 11 | Responsive |
| 11.5 | Products Page |
| 12 | Diagram (hotspot, popup, toggle) |
| 13 | Wiper Finder |
| 14 | Product Modal |
| 15 | About Page (av-*) |
| 16 | Index Skew Wrappers (ix-*) |
| 17 | Footer Platform Links |
| 18 | Find-Wiper Additions (custom dropdown, animation) |
| 19 | Modal Single Variant Full Button |
| 20 | Modal Dual Platform Buttons (Shopee + TikTok) |

---

## JS Files

### main.js
| Section | ฟังก์ชัน |
|---------|---------|
| 1 | `loadComponents()` — inject navbar/footer |
| 2 | `setActiveNav()` |
| 3 | `initHamburger()` |
| 4 | `buildSlider()` — SLIDES array อยู่ที่นี่ |
| 5 | `loadProducts(containerId, filter, limit, badgeFilter)` |
| 6 | `loadSprayHighlight()` |
| 7 | `showProductModal(id)` / `closeProductModal()` |
| 8 | `loadProductSections()` — products.html |
| 9 | Init — DOMContentLoaded |

### diagram.js
| ฟังก์ชัน | ใช้ที่ |
|---------|--------|
| `initDiagramFull()` | products.html |
| `initDiagramTeaser()` | index.html |
| `diagramSetMode('car'\|'moto')` | toggle รถ/มอไซค์ |
| `diagramShowPopup(key)` | เปิด popup hotspot |

### wiper.js
| ฟังก์ชัน | หมายเหตุ |
|---------|---------|
| `initWiperFinder()` | find-wiper.html |
| `buildWiperHTML()` | สร้าง HTML + custom dropdown + car animation |

---

## products.json structure

```json
{
  "id": "wiper-standard",
  "name": { "th": "ใบปัดน้ำฝน", "en": "Wiper Blade" },
  "category": "wiper",
  "subcategory": "standard",
  "badge": ["best-seller"],
  "image": "assets/images/merchant/...",
  "shopee_url": "#",
  "description": { "th": "...", "en": "..." },
  "variants": [
    {
      "name": { "th": "Toyota", "en": "Toyota" },
      "shopee_url": "#",
      "tiktok_url": "#"
    }
  ]
}
```

**Badge ที่รองรับ:** `"best-seller"` → 🔥 ขายดี / `"new"` → ✨ ใหม่

**Modal behavior:**
- variants 1 รายการ → ปุ่ม Shopee + TikTok เต็มแถว
- variants หลายรายการ → แสดงชื่อ + ปุ่ม 2 ปุ่มต่อแถว

---

## wiper-data.json structure

```json
{
  "wipers": [
    {
      "brand": "Toyota",
      "model": "CAMRY",
      "year": "2012-ปัจจุบัน",
      "front1": "26",
      "front2": "18",
      "rear": "",
      "rearType": "",
      "shopee_url": "#",
      "tiktok_url": "#"
    }
  ]
}
```

**rearType:** `"A"` หรือ `"B"` = ประเภทขั้วต่อใบปัดหลัง / `""` = ไม่มีข้อมูล

---

## Navbar Layout

```
Desktop:  NAKAMA5666  |  [Logo] หน้าหลัก สินค้า ค้นหาใบปัด เกี่ยวกับเรา  |  ช้อปที่ Shopee
Mobile:   [Logo]  ช้อปที่ Shopee  ☰
```

---

## Channel URLs (ต้องอัปเดต)

| ช่องทาง | ไฟล์ที่ต้องแก้ |
|---------|--------------|
| Shopee store | `components.html`, `products.json` (ทุก shopee_url) |
| Lazada store | `components.html` |
| TikTok Shop | `components.html`, `products.json` (ทุก tiktok_url), `wiper-data.json` |
| TikTok | `components.html` |
| LINE Official | `components.html`, `about.html`, `find-wiper.html` |

---

## งานที่เหลือ

- [ ] ใส่ URL จริงทุกจุด (Shopee, TikTok, LINE)
- [ ] รูปสินค้า — ตรวจ path ใน `products.json` และ `diagram.js`
- [ ] รูป Hero Slider — `assets/images/hero/slide-1.png` ถึง `slide-4.png`
- [ ] Brand Photo สำหรับ about.html — `assets/images/about/brand-photo.jpg`
- [ ] i18n UI — เพิ่มปุ่มสลับภาษาใน navbar (`toggleLang()` พร้อมใช้)
- [ ] Deploy บน GitHub Pages + เชื่อม `nakamaauto.com`

---

## การ Deploy (GitHub Pages)

```bash
# 1. สร้าง repo บน GitHub
# 2. Push ไฟล์ทั้งหมด
git init
git add .
git commit -m "initial deploy"
git remote add origin https://github.com/username/nakama5666.git
git push -u origin main

# 3. เปิด GitHub Pages
# Settings → Pages → Deploy from branch → main → / (root)
```

**DNS Settings ที่ GoDaddy (nakamaauto.com):**

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | username.github.io |

---

## Known Issues

- `set-wiper-brake` — category เป็น `set` ยังไม่ขึ้นใน products.html (ต้องแก้ PRODUCTS_CONFIG หรือ products.json)
- i18n ยังไม่ได้ wire เข้า about.html และ find-wiper.html
- bfcache — แก้แล้วด้วย `pageshow` reload ใน main.js
