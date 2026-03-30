# ACM Plinko

A point-based Plinko game built for ACM Community events. Drop a ball, watch it bounce, and see where it lands. Each bin awards (or deducts) points from your running total.

<img width="1466" height="749" alt="Screenshot 2026-03-30 at 6 33 05 PM" src="https://github.com/user-attachments/assets/a29a480a-5762-467c-afb1-dc6dc1b3b049" />

## Features

- Custom point values per bin (no fake money, just points)
- Random officer face ball drops
- Sound effects on drop, win, and loss
- Running score total with reset
- Live stats panel
- ACM-styled dark UI with Community gradient

## Credits

This project is a fork of [AnsonH's plinko-game](https://github.com/AnsonH/plinko-game), originally built as a free-to-play web Plinko game inspired by Stake.com. Huge thanks to Anson for the physics engine setup and overall architecture. I just reskinned it for ACM.

## Development

> Requires Node.js 20+

```bash
npm install --legacy-peer-deps
npm run dev
```

### Building for Production

```bash
npm run build
npm run preview
```

## Built by ACM Development

Made with love by [ACM UTD](https://github.com/acmutd).
