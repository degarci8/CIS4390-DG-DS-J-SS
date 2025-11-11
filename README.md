Real-Time Nutrition Plan Generator

This repository contains the architecture and core code for Xtreme Fitness, a professional coaching platform specializing in high-performance training and custom nutrition planning.

This project solves the challenge of integrating legal compliance (PII/PHI) with a high-performance, custom-built, real-time nutrition plan generator. 



I. System Architecture: The Dual-Hub Approach

The system uses a "Best-of-Breed" architecture, ensuring the business is both fully functional and legally secure.


- Wix

Primary Role: Marketing Hub

Core Function: Public-facing website, branding, and secure e-commerce checkout.


- Practice Better

Primary Role: Compliance & Client Hub

Core Function: CRITICAL: Securely manages PII/PHI (health history), client files, and handles billing/scheduling.


- N8N

Primary Role: Automation Engine

Core Function: Runs Flow A (Generator) and Flow B (Data Ingestion) to connect the two hubs.


- Firebase Firestore

Primary Role: Real-Time Database

Core Function: The Custom Engine: Stores the clean Food Master List and powers the real-time editing feature.



II. Custom Feature: Real-Time Editor

The core value proposition is the ability for the coach to adjust meal plans instantly, seeing macro and calorie totals update live.

The Tool: The editor.html file is a single-page application (SPA) that acts as the custom editor.

The Engine: It uses Firebase Firestore's onSnapshot listener to maintain a live connection to the plan data. Any change made by the coach is saved instantly and reflected immediately for calculation.


III. Technical Stack

- Frontend

Component: Custom HTML/JS/Tailwind

Purpose: Coach's Real-Time Editor (editor.html).



- Database

Component: Firebase Firestore

Purpose: Secure storage for plans and the public Food Master List.



- Automation

Component: N8N (Self-Hosted/Cloud)

Purpose: Orchestrates data movement, computation, and PDF generation.



- Data Ingestion

Component: USDA API

Purpose: Source of raw food nutrient data (Flow B).



- Styling

Component: Tailwind CSS

Purpose: Ensures the UI is modern, responsive, and matches the Black/Red/White Xtreme Fitness brand.




IV. Data Flow Schematics


The system is defined by three critical workflows.


A. Coach Workflow (The Seamless Experience)

This process minimizes the coach's technical burden by making Practice Better the main hub.

Coach receives alert in Practice Better.

Coach clicks the custom link: "Edit Nutrition Plan."

The link launches the custom editor.html (powered by Firebase).

Coach edits the plan live and saves the final version.


B. Backend Automation (Flow A: Plan Generation)

This flow runs the instant a client finishes their intake form.

$$\text{Practice Better Webhook} \rightarrow \text{N8N} \rightarrow \text{Compute Targets} \rightarrow \text{Read Food Master List} \rightarrow \text{Assemble Plan Draft} \rightarrow \text{Write Securely to Firebase}$$


C. Data Ingestion (Flow B: Master Food Library)

This flow runs manually to populate the database with clean, unique food facts for Flow A to use.

$$\text{Manual Trigger} \rightarrow \text{USDA API Fetch} \rightarrow \text{Normalize Data} \rightarrow \text{Generate Unique ID} \rightarrow \text{Sequential Write to Firebase}$$



V. Getting Started

To run this project locally and deploy the full system:

Firebase Setup: Create a Firebase Project and configure Authentication (for the coach's UID) and Firestore (with the correct Security Rules).

Code Deployment: Deploy the editor.html file to your Firebase Hosting URL.

N8N Integration: Configure Flow B to populate the public /artifacts/{appId}/public/data/FoodItems collection.

System Activation: Configure Flow A with the Practice Better Webhook Trigger to begin generating live plans.

For detailed security information, including the exact rules used, please refer to the SECURITY.md file.
