# Naira Run

A 3D endless runner built with Three.js for [start.ng](https://start.ng). Dodge the crates, collect naira coins, and run as far as you can.

## How to play

| Action | Keyboard | Touch |
| --- | --- | --- |
| Change lane | Arrow keys or A / D | Tap the left or right half |
| Jump | Space, Up arrow or W | Swipe up |

3 lives. Each coin is worth ₦10. The game speeds up the longer you run.

## start.ng integration

- **Players:** the game asks start.ng's connect page who is playing (`startng:whoami`) and shows their character's name and face. Guests get start.ng's guest look and a sign-in link.
- **Character:** the 3D runner is dressed from the player's start.ng style (body colours, skin, hair, hat, accessory). Colours are applied through CSS tokens on `:root` (`--char-top`, `--char-bottom`, `--char-skin`, `--char-hair`, `--char-accent`), so central styling changes the character.
- **Leaderboard:** columns are defined in `startng.json` (`distance`, `coins`). Runs are saved with `startng:score` for signed-in players.

## Files

```
index.html    the game
startng.json  leaderboard columns
cover.png     card picture (16:10)
```

Runs locally too, as a guest. Sign-in, scores and the leaderboard only work once the game is live on start.ng.
