# Wheel Kinematics Visualizer - Working Status & Roadmap

Last Updated: 2026-11-10

---

## 📋 Project Overview
A zero-dependency, self-contained single-page application for real-time wheel kinematics simulation, providing 2D and 3D CAD visual analysis, drivetrain calculations, and real-world speed benchmarks (including bicycle comparison).

---

## 🛠️ Work Items & Completion Status

| Task | Priority | Status | Details |
|---|---|---|---|
| **1. Fix Tyre Diameter Visual Scaling** | Critical | ✅ Completed | Fixed `getDrawnRadiusPx()` to dynamically scale visual pixel radius directly with `diameterMm` (20mm to 700mm+). |
| **2. Independent Ghost Bicycle (Zero Jiggle)** | Critical | ✅ Completed | Created dedicated `bikeEntity` moving smoothly without stroboscopic jitter or digit oscillation. |
| **3. XYZ / ZYX World Plane & Orientation Gizmo** | High | ✅ Completed | Added labeled 3D world axes (+X Red, +Y Green, +Z Blue) on the ground plane and 3D Triad Gizmo. |
| **4. Separate Camera Entity in 3D** | High | ✅ Completed | Dedicated `camera` object with yaw, pitch, distance/zoom, pan, damping, and presets (`iso`, `side`, `front`, `top`, `reset`). |
| **5. Separate 3D Wheel Entity & Geometry** | High | ✅ Completed | Solid 3D cylinder mesh with depth-shaded tyre treads, beveled metallic rim, 3D spokes, and axle along Z-axis. |
| **6. Rescaling & 200% Zoom Compatibility** | High | ✅ Completed | Fully responsive dock and header wrapping for high zoom levels with zero scrollbars and no clipped controls. |
| **7. Infinite Environment with Differentiating Pattern (2D & 3D)** | Critical | ✅ Completed | Infinite scrolling road with 60px dual-tone concrete slabs, FIA red/white race curbs, yellow dashed centerline, 0.25m/1.0m metric ticks in 2D, and 3D perspective slabs with dual-lane dividers and milestone pylons. |
| **8. Adjustable Bicycle Speed Controls** | Critical | ✅ Completed | Dedicated bicycle speed stepper & slider (0.1 - 60 km/h), quick presets (5, 12, 20, 32, 45 km/h), interactive speed ladder items, and mode toggle between Side-by-Side Pacing and Start-to-End Lap. |
| **9. Proper Wheel-to-Bicycle Physical & Kinematic Matching** | Critical | ✅ Completed | Eliminated runaway hypersonic speeds; implemented exact mathematical matching ($v = \pi D \cdot \text{RPM} / 60$) with zero slip drift. Positioned bike with dynamic clearance `-(drawnRadiusPx + 95)` to eliminate overlap in 2D, and true 3D wireframe mesh in adjacent lane ($Z = 130$). |
| **10. Fix 3D Infinite Merging & Z-Axle Pole Snapping** | Critical | ✅ Completed | Completely eliminated the modulo wrap-around glitch where poles snapped back to center at the Z-axis ($X = 0$). Replaced with persistent world coordinate indexing ($X = k \cdot S + \text{scrollX}$) so pylons and slabs glide seamlessly through the origin and past the camera. |
| **11. 3D Background Houses & Roadside Scenery** | High | ✅ Completed | Added procedural 3D architectural houses along the roadside verge ($Z = -350$), featuring pitched gable roofs, roof tiles, glowing amber windows, chimneys, and evergreen pine trees that move with natural perspective parallax. |
| **12. Continuous Verification & Documentation** | Ongoing | ✅ Completed | Validated 100% JavaScript syntax via Node.js VM engine, launched in browser, and updated roadmap. |
| **13. Optional Polish & Audio Drivetrain** | Future | 📋 Planned | Web Audio API synthetic motor RPM hum, G-force / centripetal acceleration vector ($a = \omega^2 r$). |

---

## 📝 Change Log

### Update 6 (Latest):
1. **Seamless 3D World Scrolling (Eliminated Pole Snap Bug)**:
   - **Root Cause Identified**: Previously, `offset = ((groundOffsetPx % slabLen) + slabLen) % slabLen` wrapped modulo 120, while pylons checked `k % 2 === 0` (every 240 units). When a pole reached the Z-axis ($X = 0$), the modulo wrap caused the pole to vanish and reset back to the center with a 40px phase jump.
   - **Fix Applied**: Implemented persistent integer world coordinate indexing ($k \in [k_{\min}, k_{\max}]$ where $k_{\min} = \lfloor (X_{\min} - \text{scrollX}) / S \rfloor$).
   - Every pylon, slab, curb tooth, and lane dash maintains its persistent identity $k$. Objects now glide seamlessly through the blue Z-axis ($X = 0$) and continue continuously down the negative X-axis into the distance behind the wheel without any snapping, jumping, or popping.

2. **3D Procedural Background Houses & Scenery**:
   - Built a dedicated 3D architectural rendering pipeline (`draw3DBackgroundHouses`) along the roadside verge ($Z = -350$ to $-420$):
     - **3D House Volumes**: Base walls, depth side walls, front wall facades, and triangular front gables.
     - **Pitched Roofs & Chimneys**: Beveled tile roofs in crimson terracotta, slate grey, and navy blue, with 3D brick chimneys.
     - **Glowing Interior Windows & Doors**: Warm amber glowing windows (`#ffb703`) with subtle bloom and dark frame trim.
     - **Evergreen Pine Trees**: Conifer trees with trunks and dual-layer evergreen foliage placed beside the homes.
     - **Parallax Motion**: Houses move at the exact ground speed, exhibiting natural 3D depth parallax relative to the foreground wheel and road.

3. **2D Seamless Pavement Alignment**:
   - Ported the persistent world coordinate indexing to 2D road slabs, FIA curbs, and metric distance ticks, ensuring identical zero-glitch visual fidelity in 2D mode as well.
