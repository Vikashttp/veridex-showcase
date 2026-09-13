# Veridex — ESG Intelligence Platform

**Live demo:** https://veridex.streamlit.app
**Login:** admin@veridex.com / Admin@2024

> **This is a prototype.** Veridex was built as my final year Computer Science project at the University of Plymouth. It is a working proof of concept, not a finished product. The real, production-grade version of this idea is **Kivor**, currently in active development. See the section below for details on that.

## What this is

Veridex is a machine learning powered ESG intelligence platform. It gives small and medium businesses a way to get a real ESG assessment without paying for an expensive consultant or waiting weeks for a report, and gives anyone a way to explore and compare the ESG performance of large global companies.

## What it does

**Company analytics dashboard**
Tracks 17 global companies across 16 ESG metrics from 2020 to 2024. A Random Forest model predicts ESG scores from raw company data (R² of 0.833), there is a strategy simulator for what-if analysis, a 5 year ESG forecast, and AI generated recommendations and summaries powered by Groq.

**SME assessment tool**
A four step guided flow where a small business uploads its own documents (utility bills, payroll, financial statements). The platform extracts the data automatically using OCR and PDF parsing, then scores the business against sector peers using VESGA, a scoring algorithm I built that combines K-Means clustering with Bayesian shrinkage.

**Live financial data**
Revenue, net income and market cap are pulled live from Yahoo Finance for companies with a public ticker, rather than relying only on the static dataset. ESG scores themselves stay based on the hand curated dataset below, since there is no reliable free source for real ESG scoring.

## Try it yourself

You can log in with the demo admin account above, or register your own account and pick a role (Admin, Analyst, or Viewer) to see how access differs between them.

**Important: account data is not guaranteed to persist.** User accounts are stored in a simple JSON file rather than a real database. If the app restarts, goes to sleep from inactivity, or gets redeployed, any accounts created after the last deployment will be wiped and reset back to just the default admin account. This is a known and accepted limitation of the prototype, not a bug. A real database (Supabase) is one of the things fixed in Kivor.

## Tech stack

Python, Streamlit, scikit-learn, Groq (Llama based models), yfinance, pytesseract, pdfplumber, fpdf2, Plotly

## Dataset

Built manually from public annual reports and sustainability disclosures: 17 companies, 7 sectors, 5 years, 16 metrics per company.

## Known limitations

- Account storage is temporary, as explained above
- ESG scores for the 17 tracked companies are only as current as the last dataset update, not live
- Built and tested as a desktop experience, not optimised for mobile
- AI generated content (recommendations, summaries, outlook analysis) can occasionally be wrong or generic, like any LLM output, and should be treated as a starting point rather than financial or compliance advice

---

## What's next: Kivor

Veridex was the proof of concept. I am now rebuilding the entire platform from scratch as **Kivor**, aiming to take it from a university project to an actual business.

The scope is a lot bigger. Kivor moves off Streamlit onto a FastAPI backend with a React frontend and Supabase handling auth and data properly, so the account persistence issue above simply does not exist. The scoring engine is a five layer pipeline: raw company data runs through GHG Protocol and DEFRA conversion factors, then a transparent, config driven rubric scoring layer (no black box deciding the actual number), then a machine learning layer for forecasting and peer benchmarking, before finally mapping the output to standard reporting frameworks. That means Kivor can properly handle **Scope 1, 2 and 3 emissions tracking and Net Zero trajectory reporting**, which Veridex's original scoring never attempted.

The business model is a four tier structure: a free tier for individual carbon tracking, a micro business finance health dashboard, a full SME ESG assessment tier, and an enterprise tier where large companies pull aggregated, benchmarked data from their own SME suppliers. Enterprises invite their suppliers onto the platform, which is what creates the underlying data asset: real UK SME data that gets more valuable and more accurate the more businesses join.

Kivor is still in active development. Veridex stays here as the original prototype and the proof that the core scoring approach works.

---

Built by Vikash, BSc Computer Science, University of Plymouth
