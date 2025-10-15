# Prept: AI-Enhanced Weekly Meal Planner (Local Storage Edition)

Prept is a single-page, local web application designed to simplify meal planning, recipe management, and shopping list generation. It operates entirely within the user's browser, requiring no login or external accounts, and utilizes local storage for all data persistence.

## Key Features

*   **Weekly Meal Planning:** Easily plan your meals for the week, assigning recipes to specific meal slots (breakfast, lunch, dinner).
*   **Personal Recipe Collection:** Store and manage your own recipes with details like ingredients, preparation time, and instructions.
*   **Smart Shopping List Generation:** Automatically aggregates ingredients from your weekly meal plan into a consolidated, checkable shopping list.
*   **AI-Powered Recipe Ingestion:** Utilize the Gemini API for Optical Character Recognition (OCR) to extract recipe details directly from images.
*   **Local-First Approach:** All data is stored securely in your browser's LocalStorage, ensuring privacy and offline accessibility.

## Technical Stack

*   **Frontend:** React (Single File Component - `App.jsx`)
*   **Styling:** Tailwind CSS (for a modern, responsive design)
*   **Data Persistence:** Local browser storage (LocalStorage)
*   **AI Integration:** Gemini API (for image OCR)

## Core Data Model (Local Storage)

All application data is managed using the browser's LocalStorage. Key data structures include:

*   `prept_recipes`: A JSON array storing the user's personal recipe collection. Each recipe has a unique ID.
*   `prept_weekly_plan`: A JSON object mapping recipe IDs to specific days and meal slots (e.g., Monday breakfast, Tuesday lunch).

## Development Phases

The project is structured into five main development phases:

1.  **Core Setup and Local Storage Integration:** Establishing the React app, responsive layout, and robust data persistence.
2.  **Recipe Book (CRUD):** Implementing functionality to Create, Read, Update, and Delete recipes.
3.  **Weekly Meal Planning:** Building an interactive calendar view for scheduling meals.
4.  **Shopping List Generation:** Aggregating ingredients from planned meals into a dynamic shopping list.
5.  **AI Integration (Image OCR):** Enabling recipe creation from images using the Gemini API, with a review and pre-fill flow.

This application aims to provide a seamless and private meal preparation experience, enhanced by AI capabilities.
