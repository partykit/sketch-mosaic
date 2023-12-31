# sketch-mosaic

This is a multiplayer drawing challenge web toy, and can be found at [mosaic-party.vercel.app](https://mosaic-party.vercel.app).

Each turn, a user is asked whether a random tile should be black or white according to a given challenge. All users see the same mosaic, and all users play at the same time. It's fun to see how quickly the image converges... or doesn't.

![image](/assets/screenshot.png)

## Experimental!

This app was created during [Matt](https://interconnected.org)'s summer 2023 residency. The purpose is to experiment with multiplayer interactions, and simultaneously see what PartyKit can do. It's called a sketch because it's lightweight and quick, and because we learn something in making it.

## What you'll find here

This app is based on Next.js and PartyKit.

To share state, PartyKit keeps a `Mosaic` object in party-side storage. When a client connects, it receives the entire object in a websocket message called `sync`. When a client makes a turn, the new tile is added to the mosaic, and broadcast to all others in the room as an `update` message.

To see this code:

- server (party-side): `src/partykit/server.ts`
- client: `src/app/Room.ts`

## To run this locally

Clone the repo, then (assuming you have Node.js installed):

```bash
npm install
cp .env.example .env  # tells the app where to find the partyserver
npx partykit dev  # runs the partyserver
npm run dev       # runs the app
```

Then go to [localhost:3000](http://localhost:3000) to use the app (check out multiplayer by opening multiple browser windows).

The state of the game is kept in room storage. There's a debug endpoint so you can see the current state (you'll need to refresh the page to see changes). Go to [127.0.0.1:1999/party/announcer](http://127.0.0.1:1999/party/announcer) -- check out the the partyserver code for how this works.
