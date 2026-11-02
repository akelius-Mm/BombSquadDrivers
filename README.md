# Pocket Range

A 3D driving range for your phone. Hold the phone like a club grip and swing it.
The phone's gyroscope measures the swing, and the game turns it into a full ball flight
with carry, roll, spin, wind and a launch-monitor readout.

Everything is in one file, `index.html`. It uses three.js from cdnjs and has no build step.

## Play it on your phone

Phone browsers only give motion sensors to pages served over **https**. The easiest host is GitHub Pages:

1. On GitHub, open the repository's **Settings → Pages**.
2. Under **Build and deployment**, pick **Deploy from a branch**, choose the branch that holds `index.html`, folder `/ (root)`, and save.
3. After about a minute, open `https://<owner>.github.io/<repo>/` on your phone in Safari (iPhone) or Chrome (Android).
4. Tap **Swing with phone**. On iPhone, allow **Motion & Orientation** access when asked.
5. Optional: use **Add to Home Screen** so it opens full screen.

Any other https static host works too (Netlify, Cloudflare Pages, Vercel).
For local testing, `npx serve .` plus a tunnel such as `cloudflared tunnel --url http://localhost:3000` gives you an https link to open on the phone.

## How to swing

1. Turn on Portrait Orientation Lock. Hold the phone upright in both hands like a club grip, long edge along the shaft, screen facing you. Either end can point up. If you prefer the screen toward the target, set **Screen faces** to Target in settings.
2. Tap **Swing with phone**, set up at address and hold still. The game reads how you are holding the phone from gravity, squares a virtual driver to the target, and beeps.
3. Swing. From your point of view you see the driver and your hands follow the phone, and a yellow trail traces the clubhead's path.
4. After the ball lands, the trail stays on screen so you can check your path, and the next ball tees up on its own.

**Safety:** use a wrist strap or a firm two-handed grip, and clear the room. Swing smooth. **Power assist** in settings scales a gentle indoor swing up to full-shot club speeds.

## What the sensors measure

The gyroscope is integrated into the phone's orientation, starting from the calibrated address pose. That orientation drives a simple model of your arms and the club pivoting around your chest.

| Reading | How it is calculated |
| --- | --- |
| Club speed | Peak angular speed of the hands in the downswing × the club's swing radius × power assist |
| Face angle | Where the virtual clubface points at the moment the clubhead is closest to the ball |
| Club path | The direction the virtual clubhead is moving at that moment (in-to-out or out-to-in) |
| Start line and curve | Start line is about 78% face and 22% path. Curve comes from face minus path, as on a launch monitor |
| Tempo | Backswing time ÷ downswing time. Tour players average about 3:1, and tempo far from that costs strike quality |

The result card draws a top-down impact diagram: the dashed target line, your path (yellow arrow) and the face (red line), with angles doubled so they are easy to see.
The game reads which way up the phone is from the phone's orientation sensor. When the phone is upright, gravity can't show which way the screen faces, so the **Screen faces** setting fills that in. If the on-screen club still moves the opposite way to your hands, turn on **Reverse club motion** in settings.

Ball flight uses drag and Magnus lift with spin decay, then bounce and roll.
A tour-speed driver (167 mph ball speed, 11° launch, 2,700 rpm) carries about 270 yards.

## Graphics

The range is rendered with three.js r160: a physically based sky with drifting clouds, a sun that casts real shadows on the mat and club, sky reflections on the clubhead and ball, ACES filmic tone mapping, 150,000 swaying grass blades around the tee, mowed stripes, domed greens with bunkers and waving flags, layered tree lines and hills in the haze.
Everything is generated in code, so no image or model files are needed.
Add `?q=low` to the address for a lighter version on older phones.

## No motion sensors?

Tap **Swipe**: drag down on the screen for the backswing, then flick up through the ball. Flick speed sets power, and a sideways flick or a curved path shapes the shot.
Swipe mode also works on a computer with a mouse, and inside embedded previews that block motion sensors.

## Clubs

Driver, 3 wood, 5 iron, 7 iron, 9 iron and pitching wedge, each with its own loft, smash factor, launch and spin.
The **Session** panel shows average carry, total and dispersion per club, and keeps shots on the device between visits.
