# ARCHITECTURE DECISION: Hosting and Data Pipeline

This document outlines the architectural rationale for website hosting and the data pipeline connecting the operational database to the analytical platform for modeling.

---

## 1. Website Hosting and Operational Database (Task 1.2)

### The Decision: Robust Hosting for High Traffic

* **Choice:** Select and purchase **robust website hosting** (VPS, Managed WordPress, or Cloud Hosting like IONOS) capable of handling **high-traffic content volume**.
* **Rationale:** For a high-frequency, content-driven site involving user submissions and voting, shared hosting is inadequate. A dedicated-resource solution (VPS/Cloud) ensures **performance, uptime, and scalability** are maintained even during traffic spikes, preventing the live website from slowing down.

### Role of the Operational Database

The primary database, which resides on this hosting, is the **Source of Truth** for the live site's operations.

* **Content:** All CMS-managed pages, articles, and media files.
* **UGC & Interaction:** All user submissions, comments, and the results of the **Gamification Voting (Possible/Not)**.
* **System Data:** User accounts, platform settings, and CMS metadata.

---

## 2. Analytical Data Pipeline for Modeling

### The Strategy: Separation of Workload via ETL

The architecture mandates separating the transactional, user-facing database from the analytical database used for LLM modeling and research.

* **Approach:** Implement an **ETL (Extract, Transform, Load)** pipeline.
* **Rationale:** This is a crucial best practice. **Modeling and analysis** (which involve complex, long-running queries) must **not** occur on the live website's operational database. Running intensive analytics directly on the CMS database will severely degrade the user experience and site speed.

### Target Analytical Platform

* **Target:** Google **Cloud SQL** (or a similar analytical database service).

### The ETL Process

This pipeline moves the data from the live site to the analysis environment in a structured way:

1.  **Extract (E)**
    * **Action:** Pull raw, relevant data (e.g., content, voting activity, comment logs, user interaction metrics) from the CMS's operational database.
2.  **Transform (T)**
    * **Action:** This is the most critical step for modeling. The raw data is **cleaned, standardized, and enriched**.
    * **Examples:** Data cleansing (removing duplicates, handling missing values), data standardization (consistent date/time formats), and **Feature Engineering** (calculating new fields like "Comment Velocity" or "Engagement Score") that are necessary for the LLM and analytical models.
3.  **Load (L)**
    * **Action:** Load the transformed, clean dataset into the highly optimized Google **Cloud SQL** analytical database, making it available for running machine learning models, creating dashboards, and conducting research.
