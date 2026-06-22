# Avatar Tech Stack Research — React Native Compatible

## What Kind of Avatar Are We Actually Talking About?

Before the options, clarify this internally because the answer changes everything:

- **Option A:** A static/animated 2D character silhouette (Solo Leveling shadow aesthetic — think dark figure with glowing eyes, evolving with level)
- **Option B:** A fully customizable 3D avatar (Ready Player Me style — user picks face, hair, outfit)
- **Option C:** Animated 2D illustration that reacts to events (level up, check-in, streak) like a Duolingo owl but darker/cooler

**For pilot speed + Solo Leveling aesthetic: Option A or C wins.** Option B (full 3D customizable) is a 2-month build, not a 21-day one.

---

## Stack 1 — Rive

**What it is:** A design + animation tool that exports lightweight, interactive animations that run natively in React Native. Think of it as the evolution of Lottie — but the animations can respond to state (level, XP, streak) in real time.

**How it works for your avatar:** A designer/AI tool builds the avatar in Rive's editor (web-based, free), exports a `.riv` file, your RN app loads it and drives its state — `currentLevel = 3` makes the avatar look different than `currentLevel = 1`, without writing animation code manually.

**React Native compatible:** Yes, officially. Package: `rive-react-native`

**Free or paid:**
- Rive editor: Free for individuals and small teams
- Runtime (the RN package): Free, open source
- Paid plans exist for teams/commercial but you don't need them for pilot

**Why it's best for you:** Rive animations are vector-based, meaning infinitely sharp on any screen size, tiny file size, and can be state-driven — so your avatar literally transforms as the user levels up, without you writing a single line of animation code. This is how you get "Solo Leveling level-up moment" in React Native without a 3-month build.

**Limitation:** Someone needs to actually design/animate the avatar in Rive. If nobody on your team can do this, you use a pre-made Rive avatar from the Rive community library (rive.app/community — free, download and modify).

**Verdict for your team:** Best option if you use a community Rive avatar as a starting point and customize colors/style.

---

## Stack 2 — Lottie (lottie-react-native)

**What it is:** Plays animations exported from Adobe After Effects as JSON files. Massive community, thousands of free pre-made animations. Airbnb built it, now open source.

**How it works for your avatar:** Find/create a character animation as an After Effects file → export as `.json` via Bodymovin plugin → drop into your RN app. The avatar plays its animation loop automatically.

**React Native compatible:** Yes, mature package. `lottie-react-native` is one of the most-used RN animation packages.

**Free or paid:**
- Package: Free, open source
- LottieFiles.com (the community hub): Free tier has thousands of avatars/characters
- Premium LottieFiles subscription: Not needed for pilot

**Why it's good:** Easiest to get running fast — go to LottieFiles.com right now, search "character" or "warrior" or "fighter," download a free `.json` file, add it to your app in 20 minutes. Done. Your pilot has an animated avatar today.

**Limitation:** Not as interactive/state-driven as Rive. You can swap between different `.json` files for different levels (level 1 avatar JSON, level 3 avatar JSON) but it's less seamless than Rive's continuous state machine. Also can't easily customize Lottie files unless you have After Effects.

**Verdict for your team:** Best option if you want the fastest possible result today, non-zero creativity required. Use it for the pilot, replace with Rive post-pilot.

---

## Stack 3 — React Three Fiber + Expo GL (3D Avatar)

**What it is:** Three.js (the industry standard 3D library) wrapped in React syntax, running on Expo's OpenGL layer. Lets you load real 3D models (`.glb`/`.gltf` files) into your React Native app.

**How it works for your avatar:** You download a free 3D character model from Sketchfab or Ready Player Me → load it into your RN app via `@react-three/fiber` and `expo-gl` → apply animations.

**React Native compatible:** Yes but with asterisks. Expo GL (`expo-gl`) is required, and there are known limitations with React Three Fiber on RN vs web — not everything from the web Three.js ecosystem translates cleanly.

**Free or paid:**
- Three.js / React Three Fiber: Free, open source
- 3D models: Sketchfab has thousands of free `.glb` files
- Ready Player Me SDK: Free tier, lets users create their own avatar
- `expo-gl`: Free

**Why it's interesting:** You get a real 3D animated character — rotate, zoom, real lighting. Closest to actual game-quality avatars. This is the "legendary tier" visual that matches your ambition.

**Limitation:** This is the hardest to implement. Performance on mid-range Android devices needs optimization. The learning curve is steep even with AI tools. `react-three-fiber` on React Native is less mature than on web — you'll hit edge cases. For a 21-day pilot, this is a risk.

**Verdict for your team:** Build this post-pilot as the v2 "wow" upgrade. Not for right now.

---

## Comparison Table

| | Rive | Lottie | React Three Fiber |
|---|---|---|---|
| **RN Compatible** | Yes (official) | Yes (mature) | Yes (with caveats) |
| **Free** | Yes | Yes | Yes |
| **Difficulty** | Low-Medium | Low | High |
| **State-driven** | Yes (best-in-class) | Limited | Yes |
| **3D** | No (2D vector) | No (2D) | Yes |
| **Time to first avatar** | 1-2 hours | 20 minutes | 2-3 days |
| **Solo Leveling fit** | Excellent | Good | Best (but risky) |
| **Pilot-ready** | Yes | Yes | Risk |

---

## My Recommendation for Right Now

**Day 1 (today/tomorrow):** Use **Lottie** to get an animated character on screen in 20 minutes. Go to lottiefiles.com, search "warrior" or "fighter" or "shadow," download a free JSON, drop it in. This proves "avatar works in our app" by end of day.

**Week 2-3 (before pilot):** Migrate to **Rive** with a proper level-based state machine — avatar looks different at Recruit vs Warrior vs Champion. This is your real differentiator and it's still free.

**Post-pilot (v2):** Explore React Three Fiber for 3D if traction justifies the build time.