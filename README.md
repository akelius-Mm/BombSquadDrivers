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

1. Grip the phone in both hands like a club: long edge along the shaft, top edge toward your belt buckle, screen facing the target.
2. Tap **Swing with phone**, set up at address and hold still. A beep means the ball is teed up.
3. Take it back and swing through. After the ball lands, the next one tees up on its own, so you can keep the phone in your hands.

**Safety:** use a wrist strap or a firm two-handed grip, and clear the room. Swing smooth. **Power assist** in settings scales a gentle indoor swing up to full-shot club speeds.

## What the sensors measure

| Reading | How it is calculated |
| --- | --- |
| Club speed | Peak angular speed of the hands in the downswing × the club's swing radius × power assist |
| Face angle | How far your hands rotated around the shaft axis between address and impact, compared with your own baseline |
| Curve (draw/fade) | How fast the face is rotating through impact, compared with your baseline |
| Tempo | Backswing time ÷ downswing time. Tour players average about 3:1, and tempo far from that costs strike quality |

Your first swings set a personal baseline, so your normal swing flies straight and changes from it shape the ball.
If slices come out as hooks for your grip, turn on **Flip curve direction**. **Reset baseline** starts over.

Ball flight uses drag and Magnus lift with spin decay, then bounce and roll.
A tour-speed driver (167 mph ball speed, 11° launch, 2,700 rpm) carries about 270 yards.

## No motion sensors?

Tap **Swipe**: drag down on the screen for the backswing, then flick up through the ball. Flick speed sets power, and a sideways flick or a curved path shapes the shot.
Swipe mode also works on a computer with a mouse, and inside embedded previews that block motion sensors.

## Clubs

Driver, 3 wood, 5 iron, 7 iron, 9 iron and pitching wedge, each with its own loft, smash factor, launch and spin.
The **Session** panel shows average carry, total and dispersion per club, and keeps shots on the device between visits.
