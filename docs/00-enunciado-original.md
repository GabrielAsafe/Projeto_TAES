# SmartPantry — Enunciado original

> Transcrição do enunciado fornecido pelo utilizador, em inglês. Foram removidos apenas os números soltos de paginação (`1`, `2`) e reformatadas as quebras de linha.

## 1. Introduction

Inefficient household grocery management and food waste remain prevalent everyday challenges. This project involves developing a self-contained, mobile-first application named SmartPantry. The application serves as a kitchen assistant that helps users manage household food inventories, monitor expiration dates, discover recipes based on available stock, and generate custom dishes for leftover ingredients using AI. The system is designed to operate autonomously on mobile devices.

## 2. Application’s Features and Flow

### Onboarding Setup and Household Profiles

On the initial launch, the application guides users through a setup flow to define their default household profile, configuring parameters such as typical serving counts, dietary lifestyles (e.g., vegetarian, vegan), food allergies, and excluded ingredients. Multiple household profiles can be created and managed; users can switch between them at any time directly from the dashboard header. While the pantry inventory, shopping list, and recipe book are shared across the household, switching the active profile ensures that all recipe searches and AI culinary suggestions automatically adapt to the dietary constraints and serving needs of whoever is eating.

### Smart Pantry Dashboard

The smart pantry allows users to track their food inventory by logging item names, storage categories, quantities, units, and expiration dates. To accommodate diverse ingredients, users can select from common food categories or create custom categories on-the-fly directly within the item modal. Ingredients nearing their expiration date (within 48 hours) are automatically highlighted in a prominent alert tray to prioritize them for upcoming meals.

### Product Insertion and Lookup

To streamline pantry entry and eliminate tedious manual typing, users can scan packaged food barcodes using their mobile device camera. The application queries public product databases to auto-populate the item name, category, and standard size into the entry form, allowing users to make adjustments before saving. If camera access is restricted, unsupported, or a barcode is unlisted, the system offers an immediate image upload or manual entry fallback.

### Recipe Discovery

Users can search for catalog recipes matched against their current pantry stock via public recipe APIs. The discovery engine calculates an ingredient overlap percentage for each dish, clearly distinguishing between items currently in stock and missing ingredients while prioritizing recipes that utilize expiring goods. Recipes violating the active profile's dietary lifestyles, allergens, or excluded ingredients are automatically filtered out. Users can also push missing ingredients directly from recipe cards to their shopping list with a single click.

### Recipe Book

The application includes a personal recipe book where users can bookmark, view details, and organize favorite catalog recipes or AI creations into custom collections and folders. Each saved recipe tracks and displays the number of times it has been prepared, remaining accessible offline.

### “GenAI Sous-Chef”

When users wish to combine arbitrary scraps or find meals that catalog searches cannot satisfy, they can invoke the “GenAI Sous-Chef”. By passing selected leftover ingredients alongside the active profile's dietary constraints and serving size to a GenAI API, the assistant generates an original, structured recipe complete with preparation times, required portions, ingredient measurements, and step-by-step instructions.

### Cook Mode

Cook Mode offers a focused interface designed specifically for use in the kitchen. It presents recipe instructions sequentially in a step-by-step carousel, highlighting only the ingredients and measurements required for the active step. Built-in countdown timers (with start, pause, and reset controls) can be triggered for timed actions, displaying a clear visual alert when time runs out.

### Meal Completion

Upon completing a recipe in Cook Mode, a summary screen presents the quantities of ingredients consumed during preparation. Users can confirm or fine-tune these amounts before the system automatically decrements their pantry stock, removing depleted goods and updating remaining quantities (or optionally skip stock depletion). Confirming meal completion also allows saving unsaved recipes to the Recipe Book and automatically increments the recipe's cooking counter.

### Grocery Shopping List

Accessible from the top header across the main views, the shopping list collects items needed for upcoming meals. Users can manually add groceries or push missing ingredients directly from recipe discovery cards. Once shopping is finished, checked items can be batch-transferred straight into the pantry inventory with user-defined categories, quantities, and expiration dates.

### Settings, Profile Management and Data Portability

The settings hub enables full administration of household profiles, including creating, editing, and deleting profiles (updating dietary restrictions, serving sizes, and excluded ingredients). Because the application operates without a mandatory backend server, users have full data ownership: they can export their entire application state (profiles, pantry stock, custom categories, shopping lists, and recipe book) as a structured JSON file, or restore data via file import with overwrite and merge options.
