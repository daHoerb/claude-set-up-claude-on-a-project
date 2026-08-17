# Claude course starter — Express API, in-memory store

## Commands

- Dev server (auto-restart): `npm run dev` — serves on `PORT` (default 3000)
- Start: `npm start`
- Run tests: `npm test` — Node's built-in runner (`node --test`), no Jest/Mocha
- Lint: `npm run lint` — ESLint

There is no watch mode for tests and no combined `check` script. CI
(`.github/workflows/ci.yml`) runs `npm install`, `npm run lint`, `npm test`
on Node 22.

## Conventions

- Plain JavaScript, CommonJS (`require` / `module.exports`) — no TypeScript,
  no ESM. `sourceType` is `script` in `.eslintrc.json`.
- Errors are returned as HTTP responses, not thrown: `res.status(404).json({ error: "..." })`.
  There is no central error handler or response wrapper.
- Validate request input in the route handler and return 400 before touching
  the store.
- Secrets go in `.env` (git-ignored); `.env.example` documents the shape.
  Never commit `.env`.

## Architecture

- `server.js` — builds the Express app and mounts the routers. `app.listen()`
  is guarded by `require.main === module` so tests can import the app without
  opening a port. Keep that guard.
- `routes/` — one file per resource, each exporting an `express.Router()`.
  Mounted in `server.js` (`/users`, `/health`).
- `db/store.js` — in-memory array standing in for a database. All data access
  goes through its exported functions; routes never touch the `users` array
  directly.
- `tests/` — `*.test.js`, driven with `supertest` against the imported app.

## Watch out

- `db/store.js` state is shared across tests in a run and resets only on
  restart. A test that creates a user changes what later tests see.
- The repo remote is public. Nothing sensitive belongs in a commit here.
