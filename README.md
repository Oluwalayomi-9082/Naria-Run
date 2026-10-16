# Naria-Run
A 3D endless runner built with Three.js. It shows the logged-in start.ng user, and the character’s look follows the platform’s CSS style tokens.

A 3D endless runner built with Three.js. Dodge the crates, collect naira coins, and see how far you can get. The game shows the logged-in start.ng user, and the character's colors come from the platform's CSS style tokens.

**Play it:** https://<your-username>.github.io/naira-run/

## How to play

| Action | Keyboard | Touch |
| --- | --- | --- |
| Move left or right | Arrow keys or A / D | Tap the left or right half of the screen |
| Jump | Space, Up arrow or W | Swipe up |

- You have 3 lives. Hitting a crate costs one life.
- Each coin is worth ₦10, and your score is distance in metres plus coin value.
- The game speeds up the longer you run.
- The top 5 scores are saved on the device you play on.

## Run it locally

The game is a single `index.html` file that loads Three.js (r128) from cdnjs.

```bash
git clone https://github.com/<your-username>/naira-run.git
cd naira-run
npx serve .
```

Open the address that `serve` prints. Opening the file by double-clicking usually works too, but a local server is safer.

## start.ng integration

### Logged-in user

The game picks up the user in this order:

1. `window.START_NG_USER`, set by the host page as `{ id, name, avatar }`.
2. A message from the host page:
```js
   iframe.contentWindow.postMessage(
     { type: 'startng:user', user: { id: '42', name: 'Ada', avatar: 'https://...' } },
     '*'
   );
```
3. URL parameters: `?user=Ada&avatar=https://...`
4. Otherwise the player is shown as Guest.

The name and avatar appear in the top bar and next to saved scores.

### Central styling

The 3D character is built from boxes and its colors are read from CSS variables on `:root`:

| Variable | Part of the character |
| --- | --- |
| `--char-skin` | Head and arms |
| `--char-top` | Shirt |
| `--char-bottom` | Trousers |
| `--char-accent` | Cap |

Changing any of these updates the character immediately, with no reload. The platform can change them in its stylesheet, or send them to the game:

```js
iframe.contentWindow.postMessage(
  { type: 'startng:style', vars: { '--char-top': '#c0392b', '--char-accent': '#ffffff' } },
  '*'
);
```

The start screen also has color pickers for shirt, trousers and cap that set the same variables.

## Project structure

```
index.html   the whole game: styles, start.ng adapter, Three.js scene and game loop
```

## Known limits

- Scores are stored in the browser's `localStorage`, so they are per device and not shared between players.
- To share scores across users, replace `saveScore` and `renderBoard` in `index.html` with calls to a backend.
- On a standalone page there is no platform login, so the game shows Guest unless a user is passed in as above.
- The `postMessage` handlers accept messages from any origin. Before shipping on start.ng, check `event.origin` against the platform's domain.
