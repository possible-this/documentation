# 🚀 Link-in-Bio UTM Implementation Guide (Biosites/Linktree)

This document provides a step-by-step guide for implementing the defined UTM tracking schema on any Link-in-Bio platform (e.g., Biosites, Linktree, Beacons).

Following this guide ensures you capture a **two-stage funnel** in Google Analytics:

* **Stage 1:** Which social platform drives users **TO** the Bio Site.
* **Stage 2:** Which button on the Bio Site drives users **TO** the final destination.

---

## Step 1: Tracking Traffic TO Your Bio Site ➡️

This set of parameters is placed directly into the **Profile Settings** of your social media accounts (e.g., the "Website" field in your Instagram profile).

**Goal:** Identify the origin of the profile click.

| Parameter | Value | Standardized Example |
| :--- | :--- | :--- |
| **`utm_source`** | (Social Platform Name) | `instagram`, `tiktok`, `twitter` |
| **`utm_medium`** | `social_bio` | Always use this to signify a profile link click. |
| **`utm_campaign`** | `bio_sites_funnel` | Standardized name for this initial tracking phase. |

### Implementation Examples

*Replace* `https://biosites.com/yourhandle` *with your actual Bio Site URL.*

| Social Platform | URL to be Placed in Profile Settings |
| :--- | :--- |
| **Instagram** | `https://biosites.com/yourhandle?utm_source=instagram&utm_medium=social_bio&utm_campaign=bio_sites_funnel` |
| **TikTok** | `https://biosites.com/yourhandle?utm_source=tiktok&utm_medium=social_bio&utm_campaign=bio_sites_funnel` |
| **Twitter/X** | `https://biosites.com/yourhandle?utm_source=twitter&utm_medium=social_bio&utm_campaign=bio_sites_funnel` |

---

## Step 2: Tracking Traffic FROM Your Bio Site ⬅️

This set of parameters is applied to **every button/link** you create within the Link-in-Bio platform's editor.

**Goal:** Identify the specific offer or button that drove the final click.

| Parameter | Value | Standardized Value |
| :--- | :--- | :--- |
| **`utm_source`** | `bio_sites` | Always use this, as the Bio Site is the immediate source of the click. |
| **`utm_medium`** | (Content Type) | `blog_link`, `lead_capture`, `ecommerce`, `portfolio` |
| **`utm_campaign`** | (Offer/Promo Name) | `latest_post_august`, `holiday_promo`, `free_guide_v2` |
| **`utm_content`** | (Button Differentiator) | `signup_button_top`, `read_article_btn`, `shop_collection_link` |

### Implementation Examples

| Button Text (On Bio Site) | Destination URL to Input into Bio Site Editor |
| :--- | :--- |
| **New Blog Post** | `https://yourdomain.com/blog/new-article?utm_source=bio_sites&utm_medium=blog_link&utm_campaign=latest_post_q4&utm_content=read_article_btn` |
| **Free Ebook Download** | `https://yourdomain.com/landing/ebook?utm_source=bio_sites&utm_medium=lead_capture&utm_campaign=free_ebook_2025&utm_content=download_ebook_btn` |
| **YouTube Channel** | `https://youtube.com/yourchannel?utm_source=bio_sites&utm_medium=social_external&utm_campaign=evergreen_youtube&utm_content=youtube_link` |

---

## 💡 Analytics Insight

By following this two-stage implementation:

* **To analyze Stage 1 (Platform Performance):** Look in Google Analytics for traffic where **`utm_campaign`** is equal to **`bio_sites_funnel`**. The **`utm_source`** dimension will tell you the top-performing social platform.
* **To analyze Stage 2 (Button Performance):** Look in Google Analytics for traffic where **`utm_source`** is equal to **`bio_sites`**. The **`utm_campaign`** and **`utm_content`** dimensions will show which links on the Bio Site are driving the best conversions.
