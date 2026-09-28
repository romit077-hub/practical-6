# Mobile Application Development - Practical 6

**Enrollment No:** 24012011189  
**Subject:** Mobile Application Development  
**Technology:** Kotlin, Android SDK, Gradle  

---

## Overview

This project demonstrates the implementation of **Android Animations** including **Frame-by-Frame (Drawable) Animations** and **Tween (View) Animations** in an Android application using Kotlin and XML resource configurations.

---

## Features

- **Animated Splash Screen (`SplashActivity`)**:
  - Frame-by-frame logo animation using `uvpce_animation_list.xml`.
  - Concurrent Tween Animation (`twin_animation.xml`) featuring scaling, translation, rotation, and alpha fading.
  - Automatic navigation to `MainActivity` with smooth fade transitions upon animation completion.

- **Main Dashboard (`MainActivity`)**:
  - Continuous frame-by-frame clock animation (`alarm_animation_list.xml`).
  - Animated heart icon sequence (`heart_animation_list.xml`).
  - Real-time live digital clock (`TextClock`).
  - Action buttons for alarm creation and cancellation UI.

- **Lifecycle-Aware Animation Control**:
  - Overrides `onWindowFocusChanged` to dynamically start and stop frame animations when focus changes, optimizing resource usage.
  - Implements `Animation.AnimationListener` to handle animation lifecycle events (`onAnimationStart`, `onAnimationEnd`, `onAnimationRepeat`).

---

## Project Structure

```
24012011189_Mad_pr6/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/a24012011189_mad_pr6/
│   │       │   ├── MainActivity.kt        # Main screen with clock & heart animations
│   │       │   └── SplashActivity.kt      # Splash screen with frame & tween animations
│   │       └── res/
│   │           ├── anim/
│   │           │   └── twin_animation.xml # Tween animation (Scale, Translate, Rotate, Alpha)
│   │           ├── drawable/
│   │           │   ├── alarm_animation_list.xml  # Alarm sequence animation
│   │           │   ├── heart_animation_list.xml  # Heart sequence animation
│   │           │   ├── uvpce_animation_list.xml  # Logo sequence animation
│   │           │   └── rectangle_gradient.xml    # Gradient background
│   │           └── layout/
│   │               ├── activity_main.xml    # Main activity layout
│   │               └── activity_splash.xml  # Splash activity layout
└── build.gradle.kts
```

---

## Tech Stack & Requirements

- **Language:** Kotlin
- **IDE:** Android Studio
- **Build System:** Gradle (Kotlin DSL)
- **Min SDK:** 24 (Android 7.0)
- **Target SDK:** 37
- **UI Components:** AppCompat, ConstraintLayout, Material Components

---

## How to Build & Run

1. Clone or download this repository.
2. Open the project in **Android Studio**.
3. Sync the Gradle project dependencies (`Sync Project with Gradle Files`).
4. Select an Android Virtual Device (AVD) or connect a physical device via USB debugging.
5. Click **Run** (`Shift + F10`) to build and launch the application.
