<<<<<<< HEAD
# Frame-by-Frame Animation and Splash Screen with Twin Animation

## AIM

Create an Android application to demonstrate:

1. **Frame-by-Frame Animation**
2. **Twin Animation**
3. **Splash Screen**
4. **Immersive Mode**
5. **Edge-to-Edge Content Display**

The application demonstrates `AnimationDrawable` for frame-by-frame animation and Android animation resources for twin animation effects.

---

## What is Frame-by-Frame Animation?

Frame-by-frame animation, also called **drawable animation**, displays a sequence of images one after another at a specified interval. Each image represents one frame of the animation.

In Android, frame-by-frame animation can be implemented using:

* `AnimationDrawable`
* `<animation-list>`
* `oneShot` attribute

The images are stored in the `res/drawable` folder and are referenced from an animation-list XML file.

### Example

```xml
<animation-list
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:oneshot="false">

    <item
        android:drawable="@drawable/frame_1"
        android:duration="100" />

    <item
        android:drawable="@drawable/frame_2"
        android:duration="100" />

    <item
        android:drawable="@drawable/frame_3"
        android:duration="100" />

</animation-list>
```

The animation can then be controlled using `AnimationDrawable`:

```java
ImageView imageView = findViewById(R.id.imageView);

AnimationDrawable animationDrawable =
        (AnimationDrawable) imageView.getDrawable();

animationDrawable.start();
```

### `oneShot`

The `oneShot`/`oneshot` attribute determines whether the animation runs only once.

```xml
android:oneshot="true"
```

means that the animation stops after the last frame.

```xml
android:oneshot="false"
```

allows the animation to repeat.

---

# What is Twin Animation?

**Twin Animation** refers to Android's traditional **Tween Animation** system. Instead of changing the image frame-by-frame, it changes properties of a View over time.

Common tween animation types are:

* `<scale>` — changes the size
* `<translate>` — moves the View
* `<rotate>` — rotates the View
* `<alpha>` — changes transparency

Multiple animations can be combined using the `<set>` tag.

For example:

```xml
<set xmlns:android="http://schemas.android.com/apk/res/android">

    <scale
        android:fromXScale="0.5"
        android:toXScale="1.0"
        android:fromYScale="0.5"
        android:toYScale="1.0"
        android:duration="1000" />

    <alpha
        android:fromAlpha="0.0"
        android:toAlpha="1.0"
        android:duration="1000" />

</set>
```

---

# How to Achieve Edge-to-Edge Content Display?

Edge-to-edge display allows the application content to extend behind the system status bar and navigation bar.

In modern Android applications, this can be enabled using:

```java
WindowCompat.enableEdgeToEdge(getWindow());
```

Depending on the AndroidX version and project configuration, edge-to-edge can also be configured through the Android window APIs.

When content is displayed edge-to-edge, system-bar insets should be handled so that important UI elements are not hidden behind the status/navigation bars.

Example:

```java
ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main),
        (view, windowInsets) -> {

            Insets insets =
                    windowInsets.getInsets(
                            WindowInsetsCompat.Type.systemBars());

            view.setPadding(
                    insets.left,
                    insets.top,
                    insets.right,
                    insets.bottom);

            return windowInsets;
        });
```

---

# Application Screens

The application contains two main activities:

```text
SplashActivity
      ↓
MainActivity
```

## SplashActivity

The splash screen demonstrates tween/twin animation.

The background is a radial gradient rectangle:

* Shape: `rectangle`
* Gradient type: `radial`
* Center X: `0.9`
* Center Y: `0.9`
* Radius: `1500`
* Start color: Pink
* End color: Blue

The splash screen also contains animated elements using scale, translate, rotate and alpha animations.

After the animation completes, `SplashActivity` opens `MainActivity`.

## MainActivity

`MainActivity` demonstrates frame-by-frame animation using an `ImageView` and `AnimationDrawable`.

---

# Suggested Project Structure

```text
app/
└── src/
    └── main/
        ├── java/
        │   └── com.example.animationapp/
        │       ├── MainActivity.java
        │       └── SplashActivity.java
        │
        ├── res/
        │   ├── anim/
        │   │   ├── splash_animation.xml
        │   │   ├── scale_animation.xml
        │   │   ├── translate_animation.xml
        │   │   ├── rotate_animation.xml
        │   │   └── alpha_animation.xml
        │   │
        │   ├── drawable/
        │   │   ├── splash_background.xml
        │   │   ├── frame_animation.xml
        │   │   ├── frame_1.xml
        │   │   ├── frame_2.xml
        │   │   └── ...
        │   │
        │   ├── layout/
        │   │   ├── activity_main.xml
        │   │   └── activity_splash.xml
        │   │
        │   └── mipmap/
        │
        └── AndroidManifest.xml
```

---

# Splash Background

Create the splash background in:

```text
res/drawable/splash_background.xml
```

Example:

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <gradient
        android:type="radial"
        android:centerX="0.9"
        android:centerY="0.9"
        android:gradientRadius="1500"
        android:startColor="#FF69B4"
        android:endColor="#0000FF" />

</shape>
```

This creates a rectangular background with a radial pink-to-blue gradient.

---

# Tween/Twin Animation XML

Create the animation resources inside:

```text
res/anim/
```

## Scale Animation

```xml
<?xml version="1.0" encoding="utf-8"?>
<scale xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXScale="0.5"
    android:toXScale="1.0"
    android:fromYScale="0.5"
    android:toYScale="1.0"
    android:pivotX="50%"
    android:pivotY="50%"
    android:duration="1000" />
```

## Translate Animation

```xml
<?xml version="1.0" encoding="utf-8"?>
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXDelta="0"
    android:toXDelta="200"
    android:fromYDelta="0"
    android:toYDelta="0"
    android:startOffset="100"
    android:duration="1000" />
```

## Rotate Animation

```xml
<?xml version="1.0" encoding="utf-8"?>
<rotate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromDegrees="0"
    android:toDegrees="360"
    android:pivotX="50%"
    android:pivotY="50%"
    android:duration="1000" />
```

## Alpha Animation

```xml
<?xml version="1.0" encoding="utf-8"?>
<alpha xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromAlpha="0.0"
    android:toAlpha="1.0"
    android:duration="1000" />
```

---

# Combining Animations Using `<set>`

The `<set>` tag allows multiple animations to be grouped together.

```xml
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">

    <scale
        android:fromXScale="0.5"
        android:toXScale="1.0"
        android:fromYScale="0.5"
        android:toYScale="1.0"
        android:pivotX="50%"
        android:pivotY="50%"
        android:duration="1000" />

    <translate
        android:fromXDelta="0"
        android:toXDelta="150"
        android:fromYDelta="0"
        android:toYDelta="0"
        android:startOffset="100"
        android:duration="1000" />

    <rotate
        android:fromDegrees="0"
        android:toDegrees="360"
        android:pivotX="50%"
        android:pivotY="50%"
        android:duration="1000" />

    <alpha
        android:fromAlpha="0.0"
        android:toAlpha="1.0"
        android:duration="1000" />

</set>
```

This satisfies the requirement to include:

* `<set>`
* `android:startOffset="100"`
* `android:duration="1000"`
* `<scale>`
* `<translate>`
* `<rotate>`
* `<alpha>`

---

# Loading Animation with `AnimationUtils`

Animations from the `res/anim` directory can be loaded using the `AnimationUtils` class and `loadAnimation()` method.

```java
Animation animation =
        AnimationUtils.loadAnimation(
                this,
                R.anim.splash_animation);
```

The animation can then be applied to a View:

```java
imageView.startAnimation(animation);
```

---

# Using `setAnimationListener()`

An animation listener can be used to perform an action after the splash animation finishes.

```java
animation.setAnimationListener(new Animation.AnimationListener() {

    @Override
    public void onAnimationStart(Animation animation) {
    }

    @Override
    public void onAnimationEnd(Animation animation) {
        Intent intent =
                new Intent(SplashActivity.this,
                        MainActivity.class);

        startActivity(intent);
        finish();
    }

    @Override
    public void onAnimationRepeat(Animation animation) {
    }
});
```

---

# `finish()` Method

The `finish()` method closes the current Activity.

In the splash screen, after opening `MainActivity`, `finish()` is used so that pressing the Back button does not return to the splash screen.

```java
startActivity(new Intent(
        SplashActivity.this,
        MainActivity.class));

finish();
```

---

# `overridePendingTransition()`

`overridePendingTransition()` can be used to specify the transition animation when moving between Activities.

Example:

```java
startActivity(new Intent(
        SplashActivity.this,
        MainActivity.class));

overridePendingTransition(
        android.R.anim.fade_in,
        android.R.anim.fade_out);

finish();
```

> Note: `overridePendingTransition()` is part of the traditional Activity transition API. For newer Android versions, AndroidX transition APIs may be preferred depending on the project requirements.

---

# `onWindowFocusChanged()`

`onWindowFocusChanged()` is called when the Activity's window gains or loses focus.

It can be used for immersive-mode related behavior.

Example:

```java
@Override
public void onWindowFocusChanged(boolean hasFocus) {
    super.onWindowFocusChanged(hasFocus);

    if (hasFocus) {
        getWindow().getDecorView().setSystemUiVisibility(
                View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY
                        | View.SYSTEM_UI_FLAG_FULLSCREEN
                        | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
                        | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
                        | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                        | View.SYSTEM_UI_FLAG_LAYOUT_STABLE
        );
    }
}
```

This is the traditional immersive-mode approach and is useful for demonstrating the concept in an educational application.

---

# AnimationDrawable

`AnimationDrawable` is used for frame-by-frame animation.

First, create an animation-list:

```xml
<?xml version="1.0" encoding="utf-8"?>
<animation-list
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:oneshot="false">

    <item
        android:drawable="@drawable/frame_1"
        android:duration="100" />

    <item
        android:drawable="@drawable/frame_2"
        android:duration="100" />

    <item
        android:drawable="@drawable/frame_3"
        android:duration="100" />

</animation-list>
```

Set this drawable on an `ImageView`:

```xml
<ImageView
    android:id="@+id/imageView"
    android:layout_width="250dp"
    android:layout_height="250dp"
    android:src="@drawable/frame_animation" />
```

Then start the animation:

```java
ImageView imageView = findViewById(R.id.imageView);

AnimationDrawable animationDrawable =
        (AnimationDrawable) imageView.getDrawable();

animationDrawable.start();
```

---

# Converting SVG Files to XML

Android Studio can use vector graphics in XML format.

An SVG file can be converted to an Android Vector Drawable.

### Steps

1. Right-click the `res/drawable` folder.
2. Select **New → Vector Asset**.
3. Select **Local file (SVG, PSD)**.
4. Browse and select the SVG file.
5. Configure the asset.
6. Click **Next**.
7. Click **Finish**.

Android Studio generates an XML vector drawable such as:

```text
res/drawable/ic_animation.xml
```

The vector drawable can then be referenced using:

```xml
android:src="@drawable/ic_animation"
```

---

# MainActivity Responsibilities

`MainActivity` should:

1. Load the main layout.
2. Find the `ImageView`.
3. Load the frame animation drawable.
4. Start `AnimationDrawable`.
5. Demonstrate the frame-by-frame animation.
6. Support the required edge-to-edge/immersive behavior.

Basic structure:

```java
public class MainActivity extends AppCompatActivity {

    private ImageView imageView;
    private AnimationDrawable animationDrawable;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        imageView = findViewById(R.id.imageView);

        animationDrawable =
                (AnimationDrawable) imageView.getDrawable();

        imageView.post(() -> animationDrawable.start());
    }
}
```

---

# SplashActivity Responsibilities

`SplashActivity` should:

1. Display the gradient splash background.
2. Display the splash image/logo.
3. Load the tween animation using `AnimationUtils`.
4. Demonstrate scale, translate, rotate and alpha animations.
5. Use `setAnimationListener()`.
6. Open `MainActivity` after the animation.
7. Use `overridePendingTransition()`.
8. Call `finish()`.

Basic structure:

```java
public class SplashActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_splash);

        ImageView logo = findViewById(R.id.logo);

        Animation animation =
                AnimationUtils.loadAnimation(
                        this,
                        R.anim.splash_animation);

        animation.setAnimationListener(
                new Animation.AnimationListener() {

                    @Override
                    public void onAnimationStart(
                            Animation animation) {
                    }

                    @Override
                    public void onAnimationEnd(
                            Animation animation) {

                        startActivity(
                                new Intent(
                                        SplashActivity.this,
                                        MainActivity.class));

                        overridePendingTransition(
                                android.R.anim.fade_in,
                                android.R.anim.fade_out);

                        finish();
                    }

                    @Override
                    public void onAnimationRepeat(
                            Animation animation) {
                    }
                });

        logo.startAnimation(animation);
    }
}
```

---

# AndroidManifest.xml

Set `SplashActivity` as the launcher Activity.

```xml
<application
    android:theme="@style/Theme.AnimationApp"
    android:label="Animation Demo">

    <activity
        android:name=".MainActivity" />

    <activity
        android:name=".SplashActivity"
        android:exported="true">

        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>

    </activity>

</application>
```

---

# Required Android Concepts

| Concept                       | Purpose                                       |
| ----------------------------- | --------------------------------------------- |
| `ImageView`                   | Displays images and animation frames          |
| Frame-by-Frame Animation      | Displays multiple images sequentially         |
| `AnimationDrawable`           | Controls drawable/frame animation             |
| `<animation-list>`            | Defines animation frames                      |
| `oneShot`                     | Controls whether frame animation repeats      |
| Tween/Twin Animation          | Animates View properties                      |
| `<set>`                       | Combines multiple animations                  |
| `<scale>`                     | Scales a View                                 |
| `<translate>`                 | Moves a View                                  |
| `<rotate>`                    | Rotates a View                                |
| `<alpha>`                     | Changes View transparency                     |
| `AnimationUtils`              | Loads animation resources                     |
| `loadAnimation()`             | Loads an animation XML file                   |
| `setAnimationListener()`      | Detects animation lifecycle events            |
| `startOffset`                 | Delays an animation                           |
| `duration`                    | Defines animation duration                    |
| `overridePendingTransition()` | Controls Activity transition animation        |
| `finish()`                    | Closes the current Activity                   |
| `onWindowFocusChanged()`      | Responds to window focus changes              |
| Immersive Mode                | Provides a fullscreen immersive experience    |
| Edge-to-Edge                  | Allows content to extend to system-bar edges  |
| SplashScreen                  | Provides an introductory screen               |
| `res/anim`                    | Stores traditional animation XML resources    |
| Vector Drawable XML           | Android XML representation of vector graphics |

---

# Expected Flow

```text
Application Starts
       │
       ▼
 SplashActivity
       │
       ├── Radial Gradient Background
       │
       ├── Scale Animation
       ├── Translate Animation
       ├── Rotate Animation
       └── Alpha Animation
       │
       ▼
 Animation Ends
       │
       ▼
 MainActivity
       │
       ▼
 ImageView
       │
       ▼
 AnimationDrawable
       │
       ├── Frame 1
       ├── Frame 2
       ├── Frame 3
       ├── Frame 4
       └── ...
       │
       ▼
 Frame-by-Frame Animation
```

---

# Conclusion

This Android application demonstrates two important types of traditional Android animation.

**Frame-by-frame animation** displays a sequence of drawable images using `AnimationDrawable` and `<animation-list>`.

**Tween/Twin animation** modifies properties such as position, size, rotation and transparency using `<translate>`, `<scale>`, `<rotate>` and `<alpha>`. These animations can be combined using `<set>`.

The project also demonstrates a splash screen, immersive mode, edge-to-edge content, animation listeners, Activity transitions, `finish()`, and conversion of SVG graphics into Android Vector Drawable XML.
=======
# practical-6
>>>>>>> 1b6b4732ab3771edf9e86f8d70138c71f667ed9d
