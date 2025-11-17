# Xtreme Fitness — Real-Time Nutrition Plan Generator

This repository contains the core architecture and codebase for the Xtreme Fitness Nutrition Platform: a system designed to securely generate, edit, and manage custom nutrition plans in real time.

The platform combines secure data handling with a fast, coach-focused editing experience built around Firebase, Stitch, and N8N.

---

## Overview

The system provides:

- A custom real-time nutrition plan editor  
- Automated nutrition plan generation using client intake data  
- A master food database sourced from the USDA  
- Secure storage and real-time syncing through Firebase Firestore  
- A Stitch-based UI for the client and coach dashboards

---

## System Architecture

The platform uses a dual-hub architecture to separate marketing, client experience, and backend automation.

### Wix (Marketing Hub)
- Public-facing website  
- Branding and checkout  

### Stitch (Client & Coach UI)
- Client intake screens  
- Coach dashboards  
- Triggers N8N workflows via webhooks  

### N8N (Automation Engine)
- Flow A: Nutrition plan generation  
- Flow B: USDA food ingestion  
- Connects Stitch to Firebase  

### Firebase Firestore (Real-Time Database)
- Stores nutrition plans  
- Stores the Food Master List  
- Powers the live editing engine in the custom editor  

---

## Real-Time Nutrition Plan Editor

The `/editor` directory contains the custom single-page application used by coaches to edit plans in real time.

Key capabilities include:

- Live macro and calorie calculations  
- Instant auto-save  
- Real-time Firestore updates  
- Tailwind CSS styling  
- Fast, coach-focused workflow  

This editor is custom-built and separate from Stitch due to its need for direct, real-time database performance.

---

## Data Workflows

### Flow A: Nutrition Plan Generation
1. Client submits intake data through Stitch  
2. Stitch sends webhook to N8N  
3. N8N computes calorie and macro targets  
4. N8N builds a draft plan using the Food Master List  
5. N8N saves the plan to Firestore  
6. Coach edits the plan through the real-time editor  

### Flow B: Food Library Ingestion
1. Manual trigger in N8N  
2. USDA data fetched via API  
3. Data normalized and cleaned  
4. Food items stored in Firestore for plan generation  

---

## Getting Started

### 1. Firebase Setup
- Create a Firebase project  
- Enable Authentication  
- Configure Firestore  
- Apply security rules found in `SECURITY.md`  

### 2. Deploy the Real-Time Editor
Deploy the `/editor` folder to Firebase Hosting using your Firebase CLI.

### 3. Configure N8N
- Import Flow A and Flow B from the `/n8n` folder  
- Connect Stitch webhooks to Flow A  
- Connect Firebase credentials for data read/write  

---

## Security

Details on Firestore rules, access control, and PII/PHI handling are documented in: SECURITY.md


