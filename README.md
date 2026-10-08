Two arcade classics, Snake and Tank Wars, in a single HTML file. Plain JavaScript and canvas, no frameworks, no build step, no dependencies.

Play it: bryanhamilton.info/arcade.html

Games
Tank Wars

Turn-based artillery for one or two players. Set your angle and power, fire, and try to land a shell on the other tank before it lands one on you.

Randomly generated terrain every battle.
Wind changes each turn and pushes shells off course.
Shells carve craters into the ground, and tanks settle into them.
Damage falls off with distance from the blast.
1 player vs CPU, or 2 players on the same device.

The CPU opponent samples 260 random angle/power pairs, simulates each shot against the current terrain and wind, picks the one that lands closest to you, then adds a little aiming error so it can miss.

Input	Action
← / →	Angle
↑ / ↓	Power
Space	Fire
Sliders and Fire button	Same, for touch and mouse
Snake

The classic, on a 20×20 grid.

Walls and your own tail are fatal.
The game speeds up as your score climbs (125 ms per step, down to a 55 ms floor).
Best score is saved in localStorage. If storage is blocked, the game still runs and just skips saving.
Input is queued, so quick double turns register.
Input	Action
Arrow keys or WASD	Steer
Space	Pause
Swipe	Steer on touch screens
On-screen d-pad	Shown on touch devices
Run it locally

No install needed. Open index.html in a browser, or serve the folder:

sh
python3 -m http.server 8000
# then visit http://localhost:8000
Use it on your own site

The whole thing is index.html. To embed it, drop it on any static host and iframe it:

html
<iframe src="/arcade.html" title="Arcade: Snake and Tank Wars"
        width="860" height="900" style="border:0;max-width:100%"></iframe>

Before publishing your own copy, update the URLs in the <head> (canonical, og:url, og:image and the JSON-LD block) and replace the author details.

Customize
Colors and fonts: the page tokens are CSS variables at the top of the <style> block (--bg, --panel, --p1 blue, --p2 orange, and so on). The canvas colors are hex values inside the draw and sDraw functions.
Tank Wars feel: G (gravity), R (crater radius) and the power multiplier in launch control how shells behave.
Snake feel: N is the grid size and the setTimeout line in tick controls speed.
Share image

arcade-share.png is the 1200×630 link preview used by the Open Graph and Twitter tags. It's generated, not hand-drawn:

sh
pip install pillow
python3 tools/make-share-image.py

The script draws the pixel logos and lettering from rectangles. It expects DejaVu Sans Mono Bold for the tagline, so change the font path at the bottom of the script if you're not on Linux.

Checks

tools/check.py uses only the Python standard library. It verifies that:

the required meta tags and canonical link are present,
the JSON-LD parses and every node has an @type,
og:image exists in the repo and is a 1200×630 PNG,
every element the script looks up by id exists in the markup,
the inline script passes node --check, when Node is available.
sh
python3 tools/check.py

GitHub Actions runs it on every push and pull request.

Project layout
index.html              both games, styles and metadata
arcade-share.png        social share image
tools/check.py          sanity checks (also run in CI)
tools/make-share-image.py   regenerates the share image
.github/workflows/ci.yml    CI
License

MIT © 2026 Bryan Hamilton
