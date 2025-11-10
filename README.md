🥗 Real-Time Nutrition Plan Generator (The "Meal Maestro")

This project is a custom, secure web application designed to automate the process of creating and editing client nutrition plans. It integrates a secure cloud database (Firebase Firestore) with a powerful automation engine (n8n) to streamline client onboarding and provide a real-time editing interface for nutrition coaches.

🚀 Architecture and Technology Stack

This application is built on a "backend-as-a-service" architecture, prioritizing security and real-time performance.

Component

Technology

Purpose

Data Ingestion

Google Forms, n8n (Webhooks)

Collects client intake data and triggers the plan generation workflow.

Plan Generation Logic

n8n (Function Nodes, Java/Code Adapters)

Calculates client targets (TDEE, Macros) and generates the initial meal plan draft.

Database

Firebase Firestore (Standard Edition)

Secure, scalable NoSQL storage for client profiles, nutrition data, and editable meal plans.

Security

Firebase Authentication & Security Rules

Locks client data down, ensuring only the authenticated coach (editor) can view or modify plans.

Editing Interface

editor.html (HTML, Tailwind CSS, JavaScript)

Provides the coach with a real-time UI where changes to food amounts instantly update calorie and macro totals.

PDF Delivery

n8n (Future: PDF/Email Nodes)

Converts the finalized plan into a professional PDF and emails it to the client.

⚙️ Getting Started (For Contributors)

To set up and run this project, you will need access to a Firebase project and an n8n instance.

Prerequisites

Firebase Project: Create a project and enable Firestore Database (Standard Edition, Production Mode) and Firebase Authentication.

n8n Instance: Access to a self-hosted or cloud n8n environment.

Required Tools: Node.js (for n8n development), Git.

Installation & Configuration

Clone the Repository:

git clone [YOUR_REPO_URL]
cd nutrition-plan-generator


Configure Firebase Security:

Create a user account for the primary editor (coach) in Firebase Authentication. Copy the unique User ID (UID).

Paste the security rules (found in SECURITY.md) into the Firestore Rules editor, replacing the placeholder UID with the editor's UID.

Populate Nutrition Data:

Ensure the FoodItems collection is populated with standardized nutrition data (e.g., via the n8n USDA API flow). This collection must be stored in the public path: /artifacts/{appId}/public/data/FoodItems.

Deploy the Editor:

Deploy the src/editor.html file using Firebase Hosting. This will be the URL the coach uses.

Setup n8n Workflows:

Import the Plan Generation workflow into your n8n instance.

Configure the Firebase Firestore nodes to use the correct paths and credentials.

🔑 Security and Data Privacy

Client plan data is highly sensitive. All client-specific plan documents are stored in a private path locked down by Firebase Security Rules.

Only the authenticated coach (editor) whose UID is hardcoded into the Firestore Rules can access or modify client plan data.

For detailed security information, including the exact rules used, please refer to the SECURITY.md file.
