# Self Driving Car (Canvas demo)

Small browser demo showing a simple self-driving car simulation drawn on an HTML canvas.

## Project structure

- `index.html` — page and script includes
- `main.js` — entry point and animation loop
- `car.js` — Car class, movement and drawing
- `controls.js` — keyboard controls
- `road.js` — road and lanes drawing
- `sensor.js` — sensor rays and intersection detection
- `utils.js` — helper functions
- `style.css` — basic page styling


## How to run

You can open `index.html` directly in a browser, but using a small static server is recommended so relative requests behave consistently:

```bash
# from project root (macOS / zsh)
cd /Users/ssgmcollege/project1/self_driving_car
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

Or use any static server (VS Code Live Server, serve, etc.).


## Controls

- ArrowUp — accelerate
- ArrowDown — reverse
- ArrowLeft / ArrowRight — steer


## Known issues & troubleshooting

- "Car is not defined" error: ensure `car.js` is included in `index.html` before `main.js` (script load order matters).

- Yellow sensor rays not showing: a common cause is a bug in `sensor.js` where `this.readings` is populated incorrectly. The intended behavior is to push a single reading per ray (the intersection or `null`). If you see console errors like `Cannot read properties of undefined (reading 'x')`, check `sensor.update` — it should call `#getReading(this.rays[i], roadBorders)` and push that result into `this.readings`.

- If sensors still don't detect borders, ensure `road.borders` exists (some versions compute `borders` in `road.js`) and that `getIntersection` is implemented in `utils.js`.


## Development notes

- The animation loop may be frame-rate dependent in earlier versions. Use a delta-time based loop (pass `delta` seconds to `car.update(delta)`) to make physics time-based.
- Tweak `car.acceleration`, `car.maxSpeed`, and `sensor.rayLength` in `car.js` / `sensor.js` to change feel.


## Contributing

Small fixes and improvements welcome. Open a PR with a short description of changes.


## License

MIT
