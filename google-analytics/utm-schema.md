# 🔗 UTM Schema & Link-in-Bio Strategy Guide

This document defines the standardized **Universal Tracking Module (UTM)** parameter schema for tracking marketing links across various channels, with a specific focus on implementing a trackable **Link-in-Bio funnel** integrated with Google Analytics.

---

## 1. Naming Conventions (The Rules) 📏

All UTM parameter values **MUST** adhere to the following conventions to ensure consistency and readability in Google Analytics:

* **Case:** Always use **lowercase** (e.g., `instagram`, not `Instagram`).
* **Spacing:** Replace spaces with **underscores** (`_`) (e.g., `blog_post_title`, not `blog post title`).
* **Special Characters:** Avoid special characters, punctuation, or symbols. Use only **letters, numbers, and underscores**.
* **Date/Time:** Do not include full dates in the campaign name unless absolutely necessary for a single-day event. Use the **quarter or month** (e.g., `q4_launch`).

---

## 2. Core UTM Parameter Definitions 🏷️

| Parameter | Required? | Purpose | Naming Guidelines & Examples |
| :--- | :--- | :--- | :--- |
| **`utm_source`** | Mandatory | Identifies the platform or origin of the traffic. | **Source (Platform Name)**. Use the root platform.<br> *e.g.,* `instagram`, `tiktok`, `linkedin`, `email`, `google`, `facebook` |
| **`utm_medium`** | Mandatory | Identifies the mechanism or type of marketing effort (e.g., social, email, paid). | **How the link was delivered or accessed.**<br> *e.g.,* `social_bio`, `story`, `post`, `newsletter`, `cpc`, `referral`, `display` |
| **`utm_campaign`** | Mandatory | Identifies the specific strategic promotion, product launch, or initiative. | **Goal or Initiative**. Use the promotion's name or theme.<br> *e.g.,* `product_launch_q4`, `black_friday_2025`, `evergreen_blog`, `free_guide_v2` |
| **`utm_content`** | Optional | Used to differentiate multiple links within the same source and campaign (A/B testing, different CTA buttons). | **Link Differentiator**. Use to specify position or visual element.<br> *e.g.,* `button_top`, `link_footer`, `image_cta`, `text_ad_headline2` |
| **`utm_term`** | Optional | Used primarily for paid search to record keywords. For social, use to record specific features. | **Specific Targeting Detail.**<br> *e.g.,* `podcast_guest_name`, `reel_music_challenge`, `pinterest_pin_id` |

---

## 3. Link-in-Bio (Bio Sites) Strategy 📱

The Link-in-Bio page itself acts as a central routing hub.

### A. Tracking the Traffic TO the Bio Site

This schema is used on the social platform when linking to the Link-in-Bio URL (e.g., the link placed in your Instagram profile settings).

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| `utm_source` | (Platform Name) | e.g., `instagram`, `tiktok`, `twitter` |
| `utm_medium` | `social_bio` | This signifies the click came from the platform's profile description link. |
| `utm_campaign` | `bio_sites_funnel` | Standardized name for all Link-in-Bio profile clicks. |

**Example Link:**
`https://yourdomain.com/bio?utm_source=instagram&utm_medium=social_bio&utm_campaign=bio_sites_funnel`

### B. Tracking the Traffic FROM the Bio Site

Every link on the Link-in-Bio page should have its own set of UTM parameters. The Link-in-Bio page is now the **source** of the click.

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| `utm_source` | `bio_sites` | The Link-in-Bio page itself is the source of the click. |
| `utm_medium` | (Destination Type) | What is the destination content type? e.g., `blog_link`, `landing_page` |
| `utm_campaign` | (Offer Name) | The specific offer the button promotes. e.g., `latest_post_august` |
| `utm_content` | (Button Name) | The exact button text or position. e.g., `read_my_new_article` |

**Example (Button on Bio Site)**

| Parameter | Value |
| :--- | :--- |
| Final Destination: | `https://yourdomain.com/blog/latest-post` |
| `utm_source` | `bio_sites` |
| `utm_medium` | `blog_link` |
| `utm_campaign` | `latest_post_august` |
| `utm_content` | `read_my_new_article` |

**Final Link:**
`https://yourdomain.com/blog/latest-post?utm_source=bio_sites&utm_medium=blog_link&utm_campaign=latest_post_august&utm_content=read_my_new_article`

---

## 4. Troubleshooting and Analysis 📈

### Analyzing the Funnel

In Google Analytics, you can analyze your funnel in two stages:

* **Profile Click Performance:** Filter by **`utm_campaign = bio_sites_funnel`** to see which social platforms (`utm_source`) drive the most users to the Bio Site.
* **Conversion Performance:** Filter by **`utm_source = bio_sites`** to see which specific offers/buttons (`utm_campaign` and `utm_content`) on your Bio Site lead to the highest conversions after they've landed on the page.

### Best Practice: URL Builders

Always use a reliable **UTM URL builder tool** (like Google's Campaign URL Builder) to construct links. This prevents human error and ensures proper encoding.
