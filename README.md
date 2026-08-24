# RideNow - Dual App Ecosystem (Rider App)

RideNow is a comprehensive Flutter-based platform that combines ride-hailing (Ride-style) and restaurant table reservations (Zomato-style) into a single, seamless user experience. This repository contains the **Rider Application**, which interacts with a centralized Firebase backend and a dedicated Partner App.

---

## 🏗 Project Architecture

RideNow follows a **Dual-App Architecture** connected through a real-time Firestore database:

1.  **Rider App (Current)**: Used by customers to book rides, search for nearby restaurants, manage their profile, and track spending.
2.  **Partner App**: Used by drivers and restaurant owners to accept incoming requests.
3.  **Real-time Handshake**: A custom state-machine logic where requests remain `pending` until a Partner explicitly clicks `accepted` in their app.

---

## 🚀 Key Features

### 1. Unified Home Interface
*   **Dual Service Gate**: Large, visual cards for "Book a Ride" and "Dining" with high-quality background images and dark gradient overlays.
*   **Personalized Experience**: Displays the user's name and quick access to the Profile dashboard.

### 2. High-Precision Riding System
*   **Live Location Streaming**: Uses a high-priority GPS stream (10-second settle time) to bypass default emulator coordinates and lock onto the user's real position.
*   **Google Maps Integration**: Full interactive map with custom markers, polylines (routes), and camera animations.
*   **Dynamic Pricing**: Calculates fares based on a `baseFare + (distanceKm * perKmRate)` formula.

### 3. Smart Dining Reservations
*   **Nearby Search**: Utilizes Google Places API to find restaurants within a 10km radius of the user's live GPS coordinates.
*   **Interactive List/Map**: Toggle between a detailed list view and a map view showing restaurant clusters.
*   **Booking System**: Select party size, date, and time slots with real-time Firestore synchronization.

### 4. Real-time Handshake Booking
*   **Firestore Sync**: Creates documents in `ride_requests` and `table_bookings` with a `pending` status.
*   **Wait Overlay**: A pulsing "Searching for Partner..." dialog that listens for status changes.
*   **Automatic Transition**: Instant navigation to Payment or Success screens once the status is updated to `accepted` by a Partner.

### 5. Profile & Activity Tracking
*   **Authentication**: Integrated Name and Phone Number login flow.
*   **Account Dashboard**: Shows wallet balance (mocked starting at ₹1500) and personal details.
*   **Activity History**: A unified history tab tracking every ride (route, type, fare) and every dining reservation (restaurant, guests, time).
*   **Total Spendings**: Automatically aggregates the cost of all completed services.

---

## 🛠 Technical Stack

*   **Frontend**: Flutter (latest Material 3 components)
*   **Backend**: Firebase Firestore (Real-time DB), Firebase Core
*   **Location Services**: `geolocator`, `geocoding`
*   **Maps**: `google_maps_flutter`
*   **HTTP/APIs**: Google Directions API, Google Places API
*   **State Management**: Singleton `AppState` with `ChangeNotifier` for synchronized UI updates.

---

## ⚙️ Setup & Configuration

### Firebase Integration
1.  Enable **Firestore** in your Firebase Console.
2.  Create two collections: `ride_requests` and `table_bookings`.
3.  Ensure your `google-services.json` (Android) and `GoogleService-Info.plist` (iOS) are correctly placed.

### API Keys
The project requires a Google Cloud API Key with the following enabled:
*   Maps SDK for Android/iOS
*   Places API
*   Directions API

---

## 🛡 Performance & Quality
*   **Clean Analysis**: The core `lib/` directory is verified as **100% error-free** via `flutter analyze`.
*   **Modernized**: All deprecated APIs (like `withOpacity`) have been updated to the latest Flutter 3.x standards (`.withValues`).
*   **Optimized**: Uses `const` constructors and distance filters on location streams to reduce CPU/Memory usage.
