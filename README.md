
# UE5 Web Monitor

**Real-time monitoring of Unreal Engine 5 Blueprint variables in a web dashboard.**

A reusable Unreal Engine plugin that streams variables from a running game to a live browser dashboard, so you can watch values change without attaching a debugger or staring at the Output Log.

> The source code is private because this is a commercial project. Happy to walk through the code and architecture in an interview or demo.

---

## Demo

<!-- Buraya GIF veya kısa video ekle: UE5'te Play'e bas, dashboard'da değerlerin canlı değiştiğini göster -->
![Live demo](docs/demo.gif)

<!-- Buraya dashboard ekran görüntüsü ekle -->
![Dashboard](docs/dashboard.png)

---

## What It Does

- Drop the plugin into any UE5 project and send variables straight from **Blueprints**, with no C++ required on the user's side.
- Watch values update live in the browser, with a history chart for each variable.
- Monitor several game instances at the same time, each one as its own session.

## Architecture

```
Unreal Engine 5          Node.js Server                 Browser
(C++ Plugin)     --->    REST API + WebSocket   --->    React Dashboard
                         + SQLite storage
```

1. **UE5 plugin (C++):** a subsystem collects variables and sends them to the server over HTTP.
2. **Node.js server:** validates the request, stores history in SQLite, and pushes updates to all connected dashboards over WebSocket.
3. **React dashboard:** shows live variable cards and a history chart per variable.

## Features

| Feature | Details |
|---|---|
| Blueprint integration | `Make ... Variable` nodes and a single `Send Variables` call |
| 11 supported types | float, int, bool, string, byte, int64, name, text, vector, rotator, transform |
| Live updates | WebSocket push, no page refresh needed |
| History | Persistent storage with SQLite, survives server restarts |
| Multi-session | Several UE5 instances can report at once, selectable in the dashboard |
| Security | API key authentication on incoming data |
| Easy setup | Server URL, API key and session name are set in **Project Settings → Plugins → Web Monitor** |
| Error handling | Connection problems are reported in the Output Log |

## Tech Stack

**Unreal Engine 5.4** · **C++** · **Blueprints** · **Node.js** · **Express** · **WebSocket** · **SQLite** · **React** · **Vite** · **Recharts**

## What I Learned

- Building and structuring a real Unreal Engine plugin (modules, subsystems, developer settings)
- Designing a small client-server system with REST and WebSocket
- Handling per-session data isolation and persistent storage
- Debugging Unreal's build system and tooling issues

## Roadmap

- Network deployment (access from other machines)
- Improved connection fault tolerance
- Packaging for distribution

---

## Contact

**Ebrar Çetinkaya**
GitHub: [@ebrarcetinkaya](https://github.com/ebrarcetinkaya)
<!-- E-posta veya LinkedIn linkini buraya ekle -->
