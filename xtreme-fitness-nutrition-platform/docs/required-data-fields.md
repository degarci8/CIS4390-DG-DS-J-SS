# Required Data Fields for Nutrition Plan Calculation
This document identifies the *minimum set* of intake fields needed for the automated nutrition plan generator (N8N Flow A).  
These fields are extracted from:  
- Peak Fitness interview notes  
- The Client Profile Questionnaire  
- Health History Questionnaire  
- Existing manual plan templates  

The fields here are the ones required for **calorie target**, **macro split**, **meal plan selection**, and **exclusions filtering**.

---

## 1. Client Identity (Non-sensitive)
Used for identifying plan owner in Firebase.

| Field | Type | Purpose |
|-------|------|----------|
| clientId | string | Firebase doc ID |
| name | string | Label on plan/PDF |

---

## 2. Physical Stats
Used to compute BMR and calorie targets.

| Field | Type | Required | Purpose |
|-------|------|----------|----------|
| age | number | yes | BMR formula |
| gender | string | yes | BMR factor |
| height_cm | number | yes | BMR |
| weight_kg | number | yes | BMR |
| body_fat_percent | number | optional | Alternate formulas (Katch-McArdle) |

---

## 3. Activity & Lifestyle
Used to compute the TDEE multiplier.

| Field | Type | Purpose |
|-------|------|----------|
| lifestyle_activity_level | enum | Determines TDEE |
| exercise_days_per_week | number | Adjusts multiplier |
| exercise_minutes_per_session | number | Optional additional factor |

---

## 4. Goals
Used for macro ratios and caloric adjustments.

| Field | Type | Purpose |
|-------|------|----------|
| primary_goal | enum | Weight loss / gain / maintain |
| goal_weight_kg | number | Optional reference |
| body_type | enum | Optional macro modifier |

---

## 5. Protein Requirement Category
Impacts protein targets.

| Category | Typical Range |
|-----------|----------------|
| sedentary adult | 0.8 g/kg |
| exercising adult | 1.2 g/kg |
| competitive athlete | 1.6+ g/kg |
| muscle building | 1.8–2.2 g/kg |

---

## 6. Food Restrictions & Preferences
Used to filter the Food Master List.

| Field | Purpose |
|--------|---------|
| allergies[] | Removes restricted foods |
| disliked_foods[] | Removes undesired foods |
| favorite_foods[] | Used as positive weighting |

---

## 7. Schedule / Lifestyle Timing (Optional)
Useful for meal timing or plan personalization.

| Field | Purpose |
|--------|---------|
| wake_time | Optional |
| bedtime | Optional |

---

## 8. Free-Text Intake (Ignored by Generator)
These are **not** used for auto-generation but may be stored for coach reference.

- 24-hour food log  
- Previous nutrition programs  
- Smoking/alcohol details  
- Misc medical history (unless we manually map later)

These items are excluded from Flow A.

---

# Summary
Only the fields listed in sections 1–6 are required for the automatic plan generator.  
This file is referenced by:

- **Issue 4 (Required Data Fields)**
- **Issue 8 (Database Schema)**  
- **Issue 10 (Intake Form Design)**  
- **Issue 24/26 (Rules Engine)**  


