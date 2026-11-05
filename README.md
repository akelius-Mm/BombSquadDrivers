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

## Left-handed?

Tap **Righty ⇄** at the top (next to Range / Putt / Course) to switch to Lefty. The golfer, club, putter, ball basket and stroke meter all mirror, and shot names follow your hand (a ball curving right is a draw for a left-hander). The setting is remembered and also lives in settings as **Handed**.

## Camera

Tap the **eye** button at the top to switch between **Facing me** (a golfer faces you and copies your hands) and **First person** (your own eyes: head down on the ball through the swing, then you look up and watch the ball fly; on the green you watch the putt roll). The **⇄** button flips the facing view left to right.

## How to swing

1. Turn on Portrait Orientation Lock. Hold the phone upright in both hands like a club grip, long edge along the shaft, screen facing you. Either end can point up. If you prefer the screen toward the target, set **Screen faces** to Target in settings.
2. Tap **Swing with phone**, set up at address and hold still. The game reads how you are holding the phone from gravity, squares a virtual driver to the target, and beeps.
3. Swing while watching the golfer on screen facing you (the ⇄ button at the top flips the view left to right): their club follows your hands, and a yellow line traces the clubhead's path. Each shot is called out loud (carry, left or right, shot shape), so you don't need to read the screen mid-swing. **View** in settings switches to **My eyes**, looking down at the ball; **Call out results** turns the voice off.
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
Your first backswing teaches the game how you hold the phone: it checks which way the phone actually turned and lines the on-screen swing up with it, so the club follows you whichever way the screen faces or whichever end is up. **Re-learn my grip** in settings starts that over. The game reads which way up the phone is from the phone's orientation sensor. When the phone is upright, gravity can't show which way the screen faces, so the **Screen faces** setting fills that in. If the on-screen club still moves the opposite way to your hands, turn on **Reverse club motion** in settings.

Ball flight uses drag and Magnus lift with spin decay, then bounce and roll.
A tour-speed driver (167 mph ball speed, 11° launch, 2,700 rpm) carries about 270 yards.

## Course

Tap **Course** at the top left to play **Pocket Pines**, an original 9-hole, par-36 course: doglegs, fairway and greenside bunkers, ponds, a creek across a par 5, and tree lines that mark out of bounds.

- Every shot is played from where the last one stopped. The club is picked for you from the distance to the pin; tap another club to change it. **Chip** is a short-game club for shots around the green.
- The **‹ ›** arrows aim 2° left or right, for doglegs or to play away from trouble. The hole map on the right shows the fairway, hazards, green, pin, your ball and the aim line.
- Lies matter: shots from the rough lose about 12% and from sand about 28%, rough grabs the roll, and a ball rolling into a bunker stays there.
- Water: one penalty stroke and a drop short of the hazard. Out of bounds: stroke and distance.
- On the green it switches to putting automatically. Hole out for the score ("Birdie!", "Par", "Bogey"), then the next tee.
- The scorecard is in the chart panel, with **New round**. Your round is saved if you close the page. Holes are picked up at par + 5.

## Putting

Tap **Putting** at the top left to move to a sloped practice green with four cups.

1. Hold the phone the same way as on the range, tap **Swing with phone**, and stay still until the beep and **PUTT** prompt.
2. Rock the phone back and through like a putter. Any stroke after the beep counts, so settle before you start.
   The view is face-on and close, like the range, and a **stroke meter** shows your putter moving back and through. Take the red marker back to the **yellow zone** for the right pace on this putt (it accounts for distance, slope, green speed and putt power). The meter also shows the face live and turns green when it's square.
3. The ball rolls with real slope and green speed, drops if it reaches the cup at a catchable pace, and lips out if it's too firm. The result is called out loud.

| Control | What it does |
| --- | --- |
| Distance chips | 3, 6, 10, 20 or 30 ft from a random spot around a cup |
| 3–12 ladder | 3, 6, 9 and 12 ft in a loop |
| Mix | A random cup and distance (4–34 ft) every putt |
| ‹ › arrows | Aim 1 inch left or right of the cup to play the break |
| Read line | Distance, uphill or downhill %, and which way it breaks, measured halfway to the hole |
| Putt power (settings) | Scales your stroke speed if putts come up short or run long |
| Green speed (settings) | Slow, medium or fast greens (stimp 8, 10 or 12) |

The putt card shows the miss (short, long, left, right), start line, putter and ball speed, tempo (about 2:1 is typical) and your makes from that distance. **Session** keeps make percentage and average miss by distance.
Swipe works for putting too: drag down and flick up gently.

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
