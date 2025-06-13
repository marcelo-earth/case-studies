---
title: Marcebot
date: "2025-06-12"
description: "Creating a real-time connection between an LLM and a human"
tags:
  - mcp
  - bot
  - automation
  - assistant
---

<img src="/marcebot__cover.webp" alt="Marcebot interface preview" />

## Introduction

It’s amazing how much autonomy I can give to code agents so far. Still, I love being consulted on crucial decisions so I can guide the LLM to achieve the best results.

With the arrival of Codex and Model Context Protocol, I started thinking on a way I can quickly **command** new instructions on long term tasks. So I build a whole new personal system that allows me to easily communicate with my AI agents. And in the process, making a fun experiment where I am the tool. So call me maybe.

## Introducing **Marcebot**

### What is Marcebot?

**Marcebot** is a experiment build to study how beneficial is to have a human in the loop when running complex tasks. Which, from my experience, I have the hypothesis that indeed it might be.

So, in the very simple terms, it's a tool that allows the LLM to consult a human in order to get a better guidance in complex decisions. Altough iterations when the the agent already generated a response is good enough for the cases when the tasks can be performed in under a couple of minutes. What about building one system that can be run in the background and need to be controlled by a human?

## Manifesto

The concept of the Model Context Protocol becomes quite obvious when you think about it. I believe we can take advantage of it to guide LLMs to do what we want. Avoiding the wrong path when the model is thinking deeply about a problem, or when it's trying to solve a problem that isn't the one we actually want to address.

From my perspective, as developers (or creators), we are now more focused on the fundamentals of everything, unafraid to learn the details of implementation. Having granular control over the process, not just the result, can be great when dealing with complex problems.

This is an example of the set of tools I'm building to connect me more effectively to the tools I use every day, and eventually, gives me greater control over background agents. To keep creating new things that can be useful for everyone. 🌎

## Development

Marcebot is structured as a three-part system, all talking to each other in real time.

I started mapping how I would register all the data related to the **requests** (previously I call them **questions**, but I think that's a bit too narrow for what I'm doing).

Everytime an agent (or a human in the fun context), calls `askMarcelo`, a new request is created in my database. This request is then used to track the status of the request, and my response.

This is where the fun starts. I think. So, the LLM generates a couple of pre-defined options to choose from. Options that are very aligned with my values or way to solve problems (when it comes to complex problems), or very simple options that are good enough for the cases when the tasks just required a Yes or No, or Item 1, Item 2 and Item 3.

I also enable the possibility to write a custom response of course, when needed. So far, I can be limited to write it very fast. Because the assistant won't wait that long (again, so far, because this kind of system change very quickly).

So far I built a couple of API endpoints to handle the requests and responses. And when I say I want to respond to a request wherever I am, I mean it.

So I built first an iPhone app, and then an Apple Watch app. Both are built with SwiftUI and use the API to allow me to respond to the requests.

### Marcebot (Frontend)

The frontend is a **Progressive Web App** (PWA) built with [Next.js](https://nextjs.org/) and powered by [Vercel AI SDK](https://sdk.vercel.ai). It handles conversations, tool invocations, and real-time LLM feedback.

The chat UI includes:

- Markdown support
- Iconography with [lucide-react](https://lucide.dev)
- Tool invocation (for example, `askMarcelo`) and streaming responses

### Command (Backend & Dashboard)

The backend lives in a Flask API inside the `/command/api` folder of a Next.js monorepo. It handles:

- Request persistence in Firestore
- Storing and verifying responses
- Notification dispatch
- Answer status polling
- Integration with **Model Context Protocol (MCP)**

The dashboard (also built with Next.js) is private. It allows me to review all questions, reply from the web, and browse response history.

### Command App (iOS + watchOS)

Built with SwiftUI, the **Command App** is my personal interface for responding on the go.

It:

- Notifies me of new questions
- Lets me respond with a tap or custom text
- Syncs with the backend in real time
- Works on both iPhone and Apple Watch

The entire app is optimized for speed, minimalism, and black-and-white accessibility. It auto-switches to dark mode and follows native Apple Human Interface Guidelines.

## How it Works

1. An agent sends a question through the API (Ask-Person Interface)
2. A request is sent to my API and stored in a database.
3. I get a notification on my watch.
4. I select an option or reply manually if I'm alive
5. If I'm sleeping or R.I.P, it will figure out a way to reply acting like me (but telling that I'm not there)
6. The response is delivered back to the agent through the MCP server.

## Software Information

- **Frontend**: Next.js, Tailwind, Vercel AI SDK, `next-pwa`, `lucide-react`
- **Backend**: Flask API, Firestore, Model Context Protocol
- **Mobile App**: SwiftUI (iOS & watchOS)
- **Model**: OpenAI `gpt-4o` and Gemini `gemini-2.5-pro`
- **Industry**: AI, Productivity, Personal Tools
- **Work Duration**: ≈2 months
- **Accessibility WCAG**: AA (2.1)
- **Version**: 1.0-preview

## Features

- Fully personalized AI assistant
- Human-in-the-loop judgment
- Tool invocation and real-time response
- iPhone + Apple Watch app
- Markdown and Generative UI chat
- Serverless and real-time architecture
