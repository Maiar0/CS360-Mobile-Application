# StockSense

StockSense is a rudimentary Android application developed for **CS360**, designed to manage and monitor inventory items with integrated low-stock alerting functionality via SMS. The app emphasizes simple usability, item-level editing, and basic authentication features.

---

## Purpose

The application enables users to:
- View inventory in **grid** and **list** formats.
- Create, update, or delete inventory items.
- Monitor inventory levels and receive SMS alerts when items fall below a predefined threshold.
- Register/login and optionally enroll for SMS-based notifications.

---

## Implementation Details

### Architecture
- Follows a basic MVVM-inspired structure using Room for persistence.
- Activities handle UI logic and data interaction directly.
- Database and entity handling are abstracted using DAOs via Room ORM.

### Core Features
- **User Authentication:** Basic login/registration using Room database.
- **Inventory Management:** Full CRUD for inventory items with ID, name, quantity, location, and alert threshold.
- **SMS Alerts:** Periodic background checks trigger alerts using Android's `SmsManager` if inventory is low and the user is enrolled.
- **Data Persistence:** Local SQLite database via Room with auto-initialized sample data.
- **UI Views:**
  - `InventoryGridViewActivity`: grid format with inline quantity increment/decrement
  - `DatabaseViewActivity`: list format with delete controls
  - `ItemDetailsActivity`: editable detail view
- **Background Work:** `LowInventoryWorker` runs hourly using WorkManager to inspect inventory and send SMS alerts.

---

## Tools & Libraries Used

- **Android SDK**
- **Java**
- **Room Persistence Library** (`androidx.room`)
- **WorkManager** (`androidx.work`)
- **RecyclerView** (`androidx.recyclerview`)
- **SharedPreferences** for session and SMS enrollment tracking
- **Android SMS API** for notifications (`SmsManager`)
- **Material Components** for dialogs and input fields

---

## Key Components

### Activities
- `LoginActivity.java`: Authenticates users; manages first-run SMS permissions and preferences.
- `MainActivity.java`: Base launcher activity and entry point for navigation.
- `DatabaseViewActivity.java`: List-style database visualization.
- `InventoryGridViewActivity.java`: Grid-based UI with in-place quantity modification.
- `ItemDetailsActivity.java`: Detailed view for item updates or deletion.

### Database (Room)
- **Entities**:
  - `Items`: Represents inventory entries.
  - `User`: Stores login credentials and SMS enrollment info.
- **DAOs**:
  - `ItemsDao`: Handles all inventory operations.
  - `UserDao`: Manages user records.
- **AppDatabase**: Singleton Room database instance with fallback strategy.
- **StarterData**: Preloads users and inventory on first launch.

### Background Worker
- `LowInventoryWorker`: Sends SMS alerts for low-stock items (threshold configurable per item) at fixed intervals (24 hrs default).

---

## Notes

- This is an intentionally minimal implementation for academic demonstration.
- No encryption or network capability included; credentials and data are stored in plaintext in local storage.
- If you would like to see a better implementaion please visit https://github.com/Maiar0/StockSense
