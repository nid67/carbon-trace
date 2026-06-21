# CarbonTrace

CarbonTrace is a production-quality, responsive single-page web application designed to help individuals monitor, understand, and reduce their daily carbon footprint. 

Built using **plain HTML, CSS, and vanilla JavaScript**, the entire application is contained within a single `index.html` file, designed to run directly in any modern browser without build steps or external dependencies.

---

## 🚀 Getting Started

### Prerequisites
* A modern web browser (Chrome, Firefox, Safari, Edge, etc.)
* Node.js (optional, only to run a local server) or Python.

### Running Locally
To launch the application using a local server, you can use either Node.js or Python:

**Using Node.js:**
```bash
# Serve the directory using http-server
npx http-server -p 8080
```
Then navigate to `http://localhost:8080`.

**Using Python:**
```bash
python -m http.server 8080
```
Then navigate to `http://localhost:8080`.

---

## 🏛️ Architecture & Code Structure

The JavaScript codebase follows the **Module Revealing Pattern** to ensure strict namespace separation, security, and maintainability.

*   **`AppState`**: Manages the application's central state, handles Supabase cloud synchronization (if configured), and performs fallback localStorage persistence for logging history.
*   **`EmissionsCalculator`**: Pure mathematical functions with robust JSDoc descriptions for calculating CO₂ emissions based on activity values and predefined factors.
*   **`ChartRenderer`**: Draws stacked bar charts and category doughnut charts dynamically using native HTML5 Canvas. Includes responsive support and high DPI scaling handles for razor-sharp visualization on Retina displays.
*   **`UIController`**: Manages DOM manipulation, handles view switches, debounces inputs (300ms), and coordinates pagination for log tables.
*   **`InsightsEngine`**: Analyzes state trends and yields actionable, ranked recommendations based on users' high-emission categories.
*   **`DataValidator`**: Sanitizes inputs (XSS protection) and enforces strict validation boundaries (e.g., negative boundary checks, maximum value limits).
*   **`TestRunner`**: Executes automated unit tests on page load and updates the UI with a system health status pill.

---

## 📊 Emission Factors

Calculations are driven by standard, real-world emission coefficients (in kg CO₂e per unit):

| Category | Item / Mode | Factor | Unit |
| :--- | :--- | :--- | :--- |
| **Transport** | Car | `0.21` | kg CO₂/km |
| | Bus | `0.089` | kg CO₂/km |
| | Train | `0.041` | kg CO₂/km |
| | Flight | `0.255` | kg CO₂/km |
| | Bike / Walk | `0` | kg CO₂/km |
| **Food** | Beef | `27.0` | kg CO₂/kg |
| | Chicken | `6.9` | kg CO₂/kg |
| | Fish | `5.1` | kg CO₂/kg |
| | Dairy | `3.2` | kg CO₂/kg |
| | Vegetables | `2.0` | kg CO₂/kg |
| **Energy** | Electricity | `0.233` | kg CO₂/kWh |
| | Gas | `0.184` | kg CO₂/kWh |
| | Heating | `0.25` | kg CO₂/kWh |
| **Shopping** | Electronics | `70.0` | kg CO₂/item |
| | Clothing | `15.0` | kg CO₂/item |
| | Furniture | `45.0` | kg CO₂/item |

---

## 🎨 Design System

Styled entirely with CSS custom properties to maintain visual harmony:
-   **Primary Color:** `#2D6A4F` (Forest green)
-   **Secondary Color:** `#52B788` (Eco green)
-   **Accent:** `#74C69D`
-   **Background:** `#F8FAF9`
-   **Surface:** `#FFFFFF`
-   **Danger/Alerts:** `#C1292E`
-   **Warning:** `#E9C46A`
-   **Fonts:** System UI (`-apple-system`, `sans-serif`)

---

## ♿ Accessibility (a11y) & Security

*   **Keyboard Navigation & Accessibility:** Implements descriptive `aria-label` elements, skip-to-content links, explicit `<label>` inputs, and robust tab indices meeting WCAG AA contrast/color standards.
*   **XSS Protection:** Encodes all user text variables through a DOM node extraction parser (`textContent`) before displaying them.
*   **No Eval:** Uses zero unsafe eval or document writes.
