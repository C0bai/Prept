Prept: AI-Enhanced Weekly Meal Planner Production Document (Local Storage Edition)
1. Project Overview
Attribute
	Details
	App Name
	Prept (Meal Prep Simplified)
	Goal
	To create a single-page, local web application that allows users to plan meals weekly, store a personal recipe collection, and generate smart shopping lists, with no login required.
	Key AI Feature
	Recipe ingestion via image OCR using the Gemini API.
	Technical Stack
	React (Single File Component - App.jsx), Tailwind CSS (for modern aesthetics and responsiveness), Local browser storage (LocalStorage) for all data persistence.
	2. Core Data Model Definition (Local Storage)
All application data is stored locally in the user's browser using the following LocalStorage keys. Data must be stringified (JSON.stringify) before saving and parsed (JSON.parse) after retrieving.
LocalStorage Key
	Data Structure
	Notes
	prept_recipes
	JSON Array of Recipes
	Stores the user's personal recipe collection. Each recipe must have a unique id generated via crypto.randomUUID().
	prept_weekly_plan
	JSON Object of Meal Slots
	Stores which recipe id is mapped to which day/meal. Structure is { "monday": { "breakfast": null, "lunch": "recipe_id_1", "dinner": "recipe_id_2" }, "tuesday": {...}, ... }.
	Recipe and Ingredient Structure:
A Recipe object must look like this:
{
 "id": "unique-uuid-string",
 "name": "Spicy Chicken Stir-fry",
 "description": "Quick weeknight meal.",
 "servings": 4,
 "prepTime": "20 minutes",
 "instructions": "Step 1: Prep veggies. Step 2: Cook chicken...",
 "ingredients": [
   { "name": "Chicken Breast", "quantity": "2 large" },
   { "name": "Soy Sauce", "quantity": "1/4 cup" }
 ]
}

3. Development Phases, Tasks, and Acceptance Tests
Phase 1: Core Setup and Local Storage Integration
Goal: Establish the single-file React application, responsive layout, and persistence via LocalStorage.
User Story
	Technical Tasks
	Acceptance Criteria (Tests)
	US 1.1 (Setup)
	Initialize the React component (App) in a single file and load Tailwind CSS and necessary Lucide React icons.
	The app renders successfully with a clean, responsive layout.
	US 1.2 (Persistence Hook)
	Implement a custom hook (e.g., useLocalStorageState) or useEffect logic to handle: 1. Initial load from LocalStorage on mount (using prept_recipes and prept_weekly_plan), providing default empty arrays/objects if keys are missing. 2. Saving the current state to LocalStorage anytime the core state variables change.
	The app displays data loaded from LocalStorage or the default state on first run. Data changes persist after a browser refresh.
	US 1.3 (Navigation)
	Create the main tab navigation (Plan, Recipes, List) and the state (activeView) to switch between them.
	Clicking a tab button correctly changes the content displayed in the main section.
	Phase 2: Recipe Book (CRUD)
Goal: Allow users to manage (Create, Read, Update, Delete) their personal recipe collection.
User Story
	Technical Tasks
	Acceptance Criteria (Tests)
	US 2.1 (Read & Detail)
	Implement the RecipeBookView component to display recipes. Recipes should be filterable by name. Implement the RecipeDetailModal to view full details.
	All existing recipes are rendered and searchable. Clicking a card opens a modal showing a formatted ingredients list.
	US 2.2 (Create UI/Logic)
	Implement the AddRecipeModal with a form. The addRecipe function must assign a unique ID (crypto.randomUUID()) and update the local recipes state.
	The user can successfully add a new recipe, and it appears immediately in the RecipeBookView.
	US 2.3 (Update Logic)
	Implement the updateRecipe function to modify an existing recipe object in the local recipes state array.
	Changes to an existing recipe are saved and reflected immediately.
	US 2.4 (Delete Logic)
	Implement the deleteRecipe function. This function must update the local recipes state, and importantly, must iterate through the weekly_plan state to clear any references to the deleted recipe ID before saving both state structures.
	Deleting a recipe requires confirmation and correctly removes the recipe from the book and the planning calendar.
	Phase 3: Weekly Meal Planning
Goal: Create an interactive, week-based calendar where users can schedule recipes.
User Story
	Technical Tasks
	Acceptance Criteria (Tests)
	US 3.1 (Calendar View)
	Implement the WeeklyPlanView component showing 7 day columns with 3 meal slots (Breakfast, Lunch, Dinner) each.
	The calendar renders correctly and is responsive (using Tailwind's grid/flex features).
	US 3.2 (Selection & Update)
	Create the MealSelectorModal. When a slot is clicked, this modal opens. Implement the updateMealSlot function, which modifies the relevant day/mealType key in the weeklyPlan state to the new recipeId.
	Selecting a recipe updates the calendar slot visually and persists the change to LocalStorage.
	US 3.3 (Clear Slot)
	Add an option within the MealSelectorModal to explicitly clear a meal slot (set the recipe ID to null in the weeklyPlan state).
	The "Clear Meal Slot" option successfully removes the recipe from the calendar.
	Phase 4: Shopping List Generation
Goal: Aggregate ingredients from all planned meals to create a consolidated shopping list.
User Story
	Technical Tasks
	Acceptance Criteria (Tests)
	US 4.1 (Aggregation Logic)
	Implement the ShoppingListView. Create a function (preferably a useMemo hook) that calculates a consolidated list by iterating through the weeklyPlan and looking up ingredients in the recipes state. Group ingredients by name, showing all unique quantities for that item (e.g., "Chicken Breast: 2 large, 1 lb").
	The list correctly aggregates all unique ingredients required for the week based on the current state.
	US 4.2 (Check-off)
	Use component local state (not LocalStorage) to manage which items on the generated shopping list have been "checked off."
	Clicking an item toggles its checked state. A "Clear Checkmarks" button resets the local check state.
	Phase 5: AI Integration (Image OCR)
Goal: Implement structured recipe creation from image uploads using the Gemini API.
User Story
	Technical Tasks
	Acceptance Criteria (Tests)
	US 5.1 (Schema & Utility)
	Define the RECIPE_JSON_SCHEMA strictly matching the data model defined in Section 2. Implement the withRetry utility for robust API calls.
	The JSON schema is correctly defined for structured recipe output.
	US 5.2 (Image UI)
	Add an "Add from Image" button/tab to the recipe creation flow. Implement a file input that converts the image to a Base64 string upon submission and displays a preview.
	A user can select a local image file (e.g., a photo of a recipe card) and see a preview.
	US 5.3 (Image API Logic)
	Implement handleAIImageUpload. Use the Gemini API (gemini-2.5-flash-preview-05-20 or gemini-2.5-flash-image-preview) with the Base64 image data and the structured responseSchema to extract and structure the recipe from the photo.
	Clicking "Process Image" shows a loading indicator and successfully returns a structured JSON recipe.
	US 5.4 (Review Flow)
	Upon successful AI generation, the app must automatically switch to the Manual Entry form and pre-fill the form with the generated JSON data for user review before the recipe is officially saved to the application state.
	The AI-generated recipe data is presented in the editable form, ready for the user to confirm and save.
