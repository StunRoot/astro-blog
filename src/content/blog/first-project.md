---
title: "Building a Real-Time Chat App with WebSockets"
description: "How I built and deployed a small real-time chat app, and what I'd do differently."
pubDate: 2026-08-01
tags: ["project", "node", "websockets"]
---

## What it is

A small chat app that uses raw WebSockets (no framework) to demonstrate
real-time message passing between clients, with a Node.js backend.

## Why I built it

I wanted to understand what libraries like Socket.IO are abstracting away
before relying on them. This project documents that process for future me
(and for anyone else curious).

## Stack

- Node.js `ws` library for the WebSocket server
- Vanilla JS on the frontend
- Deployed on Render

## What I learned

- Handling reconnect logic is the hard part, not sending messages
- Broadcasting to all connected clients needs a simple pub/sub pattern
- Heartbeats/pings matter for detecting dead connections

## Repo

[github.com/yourusername/realtime-chat](https://github.com/yourusername/realtime-chat)
