# Collab Code

A real-time collaborative code editor. Join a shared room, edit the same file live with others, pick a language, and run the code in the browser.

**Live demo:** https://collab-code-2-vxsu.onrender.com/

## Features

- **Live collaboration:** code, language and the user list stay in sync for everyone in a room.
- **Room IDs:** generate a UUID room and share it to invite others.
- **Code execution:** run Java, Python, JavaScript or C++ with custom input, and see the output in the room.
- **Editor:** Monaco (the editor behind VS Code) with a dark theme, a typing indicator and one-click room ID copy.

## Tech Stack

| Layer | Technologies |
| --- | --- |
| Frontend | React 19, Vite, Monaco Editor, Socket.io client |
| Backend | Node.js, Express 5, Socket.io |
| Execution | [Piston](https://github.com/engineer-man/piston) public API (via Axios) |

## Getting Started

**Prerequisites:** Node.js 18 or later.

```bash
git clone <this-repo-url>
cd Collab-Code

# install dependencies
npm install
npm install --prefix frontend

# start the backend (http://localhost:5000)
npm run dev

# in a second terminal, start the frontend (http://localhost:5173)
npm run dev --prefix frontend
```

To run the production build served by the backend:

```bash
npm run build
npm start
```

If the backend runs on a different address during development, set `VITE_SOCKET_URL` in `frontend/.env`.

## Project Structure

```
Collab-Code/
├── backend/
│   └── index.js        # Express + Socket.io server, room state, code execution
├── frontend/
│   └── src/App.jsx     # React UI: join screen, editor, output console
├── package.json
└── README.md
```

## Known Limitations

- Room state is stored in memory and is lost when the server restarts.
- Rooms have no authentication; anyone with the room ID can join.
- Simultaneous edits use last-write-wins, so two people typing at once can overwrite each other.
- Usernames are used as keys, so two users with the same name appear as one.
- Code execution depends on the public Piston API being available.

## Roadmap

- [ ] Conflict-free syncing for simultaneous edits (e.g. Yjs)
- [ ] Persist rooms in a database
- [ ] Video chat with WebRTC
- [ ] Split the UI into components and add tests

