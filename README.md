# Restaurant Management System

A clean, responsive, and functional React CRUD web application for managing restaurant menu items, built as a college-level project using modern React hooks and a mock JSON Server backend.

---

## Project Description

The **Restaurant Management System** is designed for restaurant staff and administrators to easily manage their daily menu offerings. It provides an intuitive interface to view current menu items, add new dishes, update pricing and details, mark item availability in real-time, and remove discontinued items. All data interactions are performed asynchronously using the standard `fetch()` API against a local RESTful JSON Server.

---

## Technologies Used

- **React (v18)**: UI component rendering with functional components.
- **React Hooks**: `useState` for UI and form state management, `useEffect` for lifecycle data fetching.
- **Vite**: Ultra-fast build tool and local development server.
- **JavaScript (ES6+)**: Clean, modern syntax with async/await.
- **Fetch API**: Native browser API for performing asynchronous HTTP CRUD requests.
- **JSON Server**: Lightweight mock REST API server running on port 5000.
- **Custom CSS3**: Responsive grid, flexbox layout, modal overlays, badges, and animations without heavy external CSS frameworks.

---

## Project Structure

```text
task1/
├── src/
│   ├── components/
│   │   ├── MenuCard.jsx       # Individual menu card view with Edit/Delete buttons
│   │   ├── MenuForm.jsx       # Controlled modal form for Adding & Editing items
│   │   └── MenuList.jsx       # Grid list wrapper and empty state display
│   ├── services/
│   │   └── menuApi.js         # Dedicated service for all fetch() HTTP operations
│   ├── App.jsx                # Main orchestrator component & global state
│   ├── main.jsx               # React DOM root entry point
│   └── styles.css             # Complete custom styling and responsive rules
├── db.json                    # Mock backend database file
├── index.html                 # Main HTML template
├── package.json               # Dependencies and runner scripts
├── vite.config.js             # Vite configuration
└── README.md                  # Project documentation
```

---

## Installation Steps

1. **Clone or navigate** to the project directory:
   ```bash
   cd task1
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

---

## How to Start JSON Server

Run the JSON Server backend on port `5000`:

```bash
npm run server
```

The mock backend will be available at:
`http://localhost:5000/menuItems`

---

## How to Start React

In a **separate terminal window**, start the Vite React development server:

```bash
npm run dev
```

Open your browser and navigate to the local URL shown in your terminal (typically `http://localhost:3000` or `http://localhost:5173`).

---

## API Endpoints

The mock server exposes the following RESTful endpoint:

- **Base URL**: `http://localhost:5000/menuItems`

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | `/menuItems` | Retrieve all menu items |
| `POST` | `/menuItems` | Create a new menu item |
| `PUT` | `/menuItems/:id` | Update an existing menu item by ID |
| `DELETE` | `/menuItems/:id` | Remove a menu item by ID |

---

## CRUD Operations Flow

1. **Create (POST)**:
   - Click **"+ Add Menu Item"** in the top navigation.
   - Enter item name, category, price, and availability.
   - Click **"Add Menu Item"**.
   - Input is validated; upon success, a `POST` request is sent and the item is appended to the UI immediately.

2. **Read (GET)**:
   - On initial page load, `useEffect` triggers `GET /menuItems`.
   - Displays a loading spinner and message (*"Loading menu items..."*).
   - If the database is empty, displays an empty state banner (*"No menu items available."*).
   - Clicking **"🔄 Refresh"** re-syncs the latest data from the server.

3. **Update (PUT)**:
   - Click **"Edit"** on any menu card.
   - *Business Rule Adherence*: Clicking "Edit" does **not** call `PUT` immediately.
   - The modal form opens pre-filled with the existing item's values.
   - The user modifies the fields and clicks **"Update Item"**.
   - Inputs are re-validated and a `PUT /menuItems/:id` request is dispatched, updating the UI.

4. **Delete (DELETE)**:
   - Click **"Delete"** on any menu item card.
   - A confirmation dialog appears (*"Are you sure you want to delete this menu item?"*).
   - If confirmed, sends `DELETE /menuItems/:id` and removes the item from the state. If cancelled, no action is taken.

---

## Validation Rules

Client-side validation is strictly enforced before submitting any data to the API:

| Field | Rule | Error Message |
|---|---|---|
| **Name** | Required (non-empty string) | *"Name cannot be empty"* |
| **Category** | Required (must select from dropdown) | *"Category cannot be empty"* |
| **Price** | Required | *"Price cannot be empty"* |
| **Price** | Positive number greater than 0 | *"Price must be a valid positive number"* |
| **Availability** | Required selection | *"Availability must be selected"* |

Inline error messages appear directly below each invalid field in red.

---

## Error Handling

The application gracefully handles API communication errors and informs the user:

- **GET failure**: *"Failed to load menu items."*
- **POST failure**: *"Failed to add menu item."*
- **PUT failure**: *"Failed to update menu item."*
- **DELETE failure**: *"Failed to delete menu item."*

---

## Screenshots Section

*(Add your screenshots here for project submission)*

### 1. Dashboard & Menu Cards View
```text
+--------------------------------------------------------------------------+
| 🍴 Restaurant Management System              [🔄 Refresh] [+ Add Menu]  |
+--------------------------------------------------------------------------+
|                                                                          |
|  +---------------------------+   +---------------------------+           |
|  | MAIN COURSE    [Available]|   | DESSERT       [Available] |           |
|  | Chicken Biryani           |   | Gulab Jamun               |           |
|  | ₹250                      |   | ₹80                       |           |
|  | [Edit]           [Delete] |   | [Edit]           [Delete] |           |
|  +---------------------------+   +---------------------------+           |
|                                                                          |
+--------------------------------------------------------------------------+
```

### 2. Add / Edit Modal Form
```text
+----------------------------------------------------+
| Edit Menu Item                                  [X]|
+----------------------------------------------------+
| Item Name *                                        |
| [ Chicken Biryani                                ] |
|                                                    |
| Category *                                         |
| [ Main Course                                  v ] |
|                                                    |
| Price (₹) *                                        |
| [ 250                                            ] |
|                                                    |
| Availability *                                     |
| (•) Available     ( ) Unavailable                  |
|                                                    |
|                     [ Cancel ]  [ Update Item ]    |
+----------------------------------------------------+
```
