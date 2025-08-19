# Zoom Meeting SDK in Next.js Codelab

This repository contains a Google Codelab demonstrating how to embed the Zoom Meeting SDK in a Next.js application.  
It walks through generating an SDK signature, dynamically loading the Zoom component, and starting a meeting.

## Prerequisites
- Node.js
- A Zoom [Meeting SDK account](https://marketplace.zoom.us/)

## Create a Next.js Project
Install the Next.js CLI and create a new project (v14.2.0 is required):
```bash
npx create-next-app@14.2.0
```
Suggested responses during setup:
- TypeScript: optional
- ESLint: Yes
- Tailwind CSS: No
- Use `src/` directory: Yes
- App Router: Yes
- Customize import alias: No

## Project Structure
```
your-project/
├── app/
│   ├── layout.tsx
│   └── page.tsx
│   └── api/
│       └── generateSignature.tsx
├── component/
│   └── ZoomComponent.tsx
├── public/
├── styles/
├── next.config.js
├── package.json
└── tsconfig.json
```

## Installation
```bash
npm install @zoom/meetingsdk jsrsasign
```

## Environment Variables
Create a `.env` file and add:
```
ZOOM_MEETING_SDK_KEY=YOUR_SDK_KEY
ZOOM_MEETING_SDK_SECRET=YOUR_SDK_SECRET
NEXT_RUNTIME_LOG=1
NODE_OPTIONS=--trace-warnings
```

## Generate a Meeting SDK Signature
Add an API route (`src/api/generateSignature.ts`) that:
1. Accepts POST requests with `meetingNumber`, `role`, and `expirationSeconds`.
2. Uses `jsrsasign` to create a JWT signature.
3. Returns `{ signature: "<jwt>" }` or an error message.

## Load and Start the Meeting
In `ZoomComponent.tsx`:
1. Dynamically import `@zoom/meetingsdk`.
2. Initialize the SDK with `ZoomMtg.preLoadWasm()` and `ZoomMtg.prepareWebSDK()`.
3. Fetch the signature from your API route.
4. Call `ZoomMtg.join` to start the meeting or webinar.

## Running the Example
```bash
npm run dev
```
Navigate to `http://localhost:3000` and click **Join Meeting**.

## Resources
- [Zoom Meeting SDK Documentation](https://marketplace.zoom.us/docs/sdk/meeting/web/)
- [Zoom Developer Forum](https://devforum.zoom.us/c/zoom-apps)

