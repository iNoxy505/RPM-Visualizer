# Real-Time Wheel Kinematics Visualizer (2D & 3D Perspective)

A zero-scroll browser simulator converting motor RPM and tyre diameter into time-accurate physics animation, 3D perspective rolling, and live bicycle speed benchmarks.

---

## 🎯 What's New in this Update

1. **3D Perspective View Mode (`[3D View 🌐]`)**:
   - Seamlessly switch between **2D Side Elevation** and **3D Perspective View** (press `V` or click the toggle in the header).
   - In 3D:
     - 3D perspective ground grid with road vanishing lines and moving transverse ticks.
     - 3D cylindrical tyre with depth, tread block lighting, rim bevels, 3D spokes, and protruding axle hub.
     - 3D cycloid trajectory curves arching above the road plane.
     - **Interactive Orbit**: Click and drag on the canvas to orbit the 3D camera angle (yaw & pitch).

2. **Bicycle & Real-World Speed Benchmark (`[🚲 vs Bike]`)**:
   - **Live HUD Badge**: Real-time ratio comparing current ground speed against a standard cruising bicycle ($20\text{ km/h}$ / $5.56\text{ m/s}$), e.g., `0.06× (-18.9 km/h)`.
   - **Visual Ghost Cyclist**: An animated bicycle paces along the ground track at $20\text{ km/h}$, letting you visually see whether your wheel outpaces or trails a cyclist.
   - **Real-World Speed Ladder**: Compare against Mars Curiosity ($0.14\text{ km/h}$), Walking ($5\text{ km/h}$), Running ($12\text{ km/h}$), City Bike ($20\text{ km/h}$), Racing Road Bike ($35\text{ km/h}$), and City Cars ($50\text{ km/h}$).
   - **One-Click Actions**:
     - `Match 20 km/h`: Automatically calculates and sets the exact RPM needed for your current wheel diameter to hit $20\text{ km/h}$.
     - `Load 26" Bike Wheel`: Sets tyre diameter to $660\text{ mm}$ ($26"$) and $160\text{ RPM}$ ($20\text{ km/h}$).

3. **200% Zoom & Rescaling Resilience**:
   - Responsive flexbox wrapping on the bottom control dock and header so **no buttons or telemetry are ever clipped or missing**, even at $200\%$ browser zoom.
   - Fixed-width tabular digits on timing readouts (`dt` and `FPS`) completely eliminate layout jiggle.

---

## 🛠️ Usage & Keyboard Shortcuts

Open [`index.html`](file:///x:/projects/programming/antigravity/RPM%20Visualizer/index.html) in any browser.

- `Space`: Play / Pause animation
- `V`: Toggle between 2D Side View and 3D Perspective View
- `R`: Reverse direction (Forward / Reverse)
- `O`: Reset odometer (distance, turns, and ghost bike)
- `Esc`: Close any open popovers or modals
- `Click & Drag Canvas`:
  - In 2D: Spin the wheel with rotational momentum.
  - In 3D: Orbit camera yaw and pitch.
