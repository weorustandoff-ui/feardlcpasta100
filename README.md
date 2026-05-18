# SnakeArena — Multiplayer Snake Game

A real-time multiplayer Snake game (Slither.io style) built on top of a TanStack Start dashboard. Players eat food to grow, eliminate rivals by making them crash into your body, and compete for the top of the daily leaderboard.

## Tech Stack

| Layer | Technology |
|---|---|
| Client | Pure JavaScript, Canvas 2D API |
| Game Server | Node.js, Socket.io v4 |
| Frontend Framework | TanStack Start (React 19) |
| Styling | Tailwind CSS 4 |
| Deployment | Netlify (client + leaderboard API), Railway/Heroku (game server) |
| Database | Netlify Database (Postgres via Drizzle ORM) |

## Features

- Real-time multiplayer with up to 50 players per room
- Smooth movement with server-side authority and client-side interpolation
- Public matchmaking and private rooms with invite codes
- 30 tick/sec authoritative server with anti-cheat (speed and position validation)
- 12 snake skins including emoji patterns, country flags, and special effects
- Teams mode: Red vs Blue with shared score
- Kill feed and in-game chat
- Daily leaderboard stored in Netlify Database
- Reconnect support: disconnect tokens preserved for 30 seconds
- World minimap with viewport indicator

## Running Locally

### Game Server

```bash
cd server
npm install
cp .env.example .env
# Edit .env: set CLIENT_URL and optional LEADERBOARD_URL
npm run dev
```

Server starts on `http://localhost:3001`.

### Frontend (TanStack Start)

```bash
npm install
npm run dev
```

Open `http://localhost:3000`. Navigate to `http://localhost:3000/game/` for the game.

In the lobby, click **Configure** to set the server URL to `http://localhost:3001`.

## Deployment

### Netlify (client + leaderboard API)

1. Push this repository to GitHub
2. Import in Netlify — the `netlify.toml` handles the build
3. The `/api/leaderboard` endpoint (Netlify Function) is deployed automatically
4. Netlify Database is provisioned automatically on first deploy

### Game Server (Railway)

1. Create a new Railway project from the `server/` directory
2. Set environment variables:
   - `CLIENT_URL` — your Netlify site URL
   - `LEADERBOARD_URL` — your Netlify site URL
   - `INTERNAL_API_KEY` — a random secret
3. Deploy; Railway auto-detects `package.json` and runs `npm start`

### After deployment

In the game lobby, click **Configure** and enter your Railway server URL (e.g. `https://your-app.railway.app`).

## Environment Variables

See `server/.env.example` for the game server variables. No environment variables are required for the Netlify deployment.

## Game Controls

| Input | Action |
|---|---|
| Mouse movement | Steer snake |
| Left click / hold | Boost (drains length) |
| Space / hold | Boost |
| Touch drag | Steer on mobile |
| Two-finger touch | Boost on mobile |
| Enter | Submit chat message |
