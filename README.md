# Encrypted Chat Demo

This repository demonstrates integrating `encrypted-chat-sdk` with `chat-room` using Git submodules and includes a `PostMessageCommAPI` in-page/iframe communication example.

## Structure
- `encrypted-chat-sdk` (submodule): SDK repository
- `chat-room` (submodule): Forked chat room backend
- `examples/postmessage-demo`: In-page and cross-iframe communication demo

## Setup

Initialize submodules:
```bash
git clone https://github.com/jinyang756/encrypted-chat-demo.git
cd encrypted-chat-demo
# Initialize submodules
git submodule add https://github.com/jinyang756/encrypted-chat-sdk.git encrypted-chat-sdk
git submodule add https://github.com/jinyang756/chat-room.git chat-room
# Pull submodule content
git submodule update --init --recursive
```

Start backend:
```bash
cd chat-room
npm install
npm start
```

Run SDK build (if needed):
```bash
cd ../encrypted-chat-sdk
npm install
npm run build
```

## SDK Integration (Socket.IO)
Use `EncryptedChatSDK` to connect to `chat-room`:
```typescript
import { EncryptedChatSDK } from 'encrypted-chat-sdk';

const sdk = new EncryptedChatSDK({
  serverUrl: 'http://localhost:3000',
  transport: 'socketio',
  roomId: '/demo',
  userId: 'user-123',
  autoKeyExchange: true
});
await sdk.connect();
```

## PostMessageCommAPI Demo
See `examples/postmessage-demo` for in-page and iframe messaging.

## Notes
- Submodules reference latest default branches; pin to specific versions as needed.
- For production, configure HTTPS and secure WS, rotate keys regularly.
