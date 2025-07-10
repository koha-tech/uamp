# Universal Agent Messaging Protocol (UAMP)


> **Open, secure and streaming‑native messaging for AI agents, services and robots.**
> Current **stable** spec: **[UAMP 1.0](spec/uamp-1.0.md)**

---

## ✨ Why UAMP?

* **Envelope freeze** — the 1.x wire‑format is locked until 2.0.
* **Zero‑trust security** — TLS 1.3 / QUIC + detached JWS signatures.
* **Streaming‑first** — `Delta` frames deliver incremental LLM output.
* **Transport choice** — HTTP/2, HTTP/3, WebSocket, gRPC.
* **Polyglot SDKs** — Python, TypeScript, Go (coming).

For architectural background see **[Design Principles](design-principles.md)**.

---

## 🚀 Quick Start ( ≤ 5 min )

### 1 · Run the reference agent

```bash
pip install -r reference-impl/python/requirements.txt
hypercorn --bind 0.0.0.0:8443 \
          --certfile certs/server.pem --keyfile certs/server-key.pem \
          uamp_reference_impl:app
```

### 2 · Send a signed *ask* envelope with the JS SDK

```bash
npm install uamp-js
```

```ts
import { UAMPClient, generateKeyPairES256 } from 'uamp-js';

const { privateKey } = await generateKeyPairES256();
const client = new UAMPClient({
  baseUrl: 'https://localhost:8443',
  key: privateKey,
  insecureTLS: true,            // dev‑only!
});
await client.send('Ping', 'did:web:worker.example');
```

You should see the agent stream back `progress` and `done` deltas.

---

## 📚 Documentation

| Section                                       | Description                                |
| --------------------------------------------- | ------------------------------------------ |
| **[Specification 1.0](uamp-1.0.md)**     | Normative wire format & transport bindings |
| **[Design Principles](design-principles.md)** | Rationale & architecture decisions         |
| **[Examples](examples/)**                     | Minimal ask/confirm, streaming image demo  |

---

## 🧑‍💻 Get Involved

* **GitHub Issues / Discussions** — bug reports, RFCs, roadmap.
* Discord `#uamp-dev` — real‑time chat.

---

© 2025 UAMP Project — Spec CC BY 4.0, Code Apache‑2.0
