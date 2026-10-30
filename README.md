<div align="center">

# 🚀 Lekzo — Advanced WhatsApp Web API

<!-- TYPING ANIMATION -->
<p>
  <img src="https://readme-typing-svg.demolab.com/?font=Fira+Code&weight=600&size=28&duration=3000&pause=1000&color=58A6FF&center=true&vCenter=true&width=800&lines=Advanced+WhatsApp+Web+API;Native+AI+Rich+Response+%26+Interactive+Buttons;Built+with+TypeScript+%26+Baileys;Lightweight+%7C+Efficient+%7C+Stable" alt="Typing Animation" />
</p>

<!-- BADGES -->
<p>
  <img src="https://img.shields.io/npm/dw/%40lekzox%2Fbaileys?label=NPM&color=%23CB3837" alt="NPM Downloads"/>
</p>

<!-- VISUAL SHOWCASE -->
### 📸 Project Showcase

<img src="https://b.top4top.io/p_3816tx02l1.jpg" alt="WhatsApp Interface" width="800" />
<br/>
<small><i>Native WhatsApp Experience integrated into your project</i></small>

<br/>

**Lekzo** (`lekzsync/Baileys`) is a powerful, lightweight, and efficient library for interacting with the **WhatsApp Web multi-device API** — no Selenium, no Chromium, no headless browser. It connects over a raw WebSocket, speaks WhatsApp's native binary + protobuf protocol, and exposes a fully typed, event-driven JavaScript/TypeScript API.

</div>

---

## ⚠️ Disclaimer & Liability

This library is a community-driven project and is **in no way affiliated with, endorsed by, or sponsored by WhatsApp Inc. or Meta**. It is an unofficial, reverse-engineered API. Use at your own discretion.

**Important Guidelines:**

- Do **not** use this library for spamming, bulk messaging, stalkerware, or any activity that violates WhatsApp's [Terms of Service](https://www.whatsapp.com/legal/terms-of-service).
- The developers are **not liable** for any misuse of this software, including account bans. Please refer to the [MIT License](LICENSE) for details.
- Users are fully responsible for ensuring their usage complies with applicable laws and WhatsApp's policies.

---

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Import](#import)
- [Quick Start](#quick-start)
  - [With QR Code](#with-qr-code)
  - [With Pairing Code](#with-pairing-code)
- [Sending Message](#sending-message)
  - [Generic Send / Relay](#generic-send--relay)
  - [sPR](#spr)
  - [Simple Senders](#simple-senders)
  - [Ban Checker](#ban-checker)
  - [Send Message with Participant](#send-message-with-participant)
  - [Rich Menu](#rich-menu)
- [Message Builder](#message-builder)
- [Button](#button)
  - [Quick Reply + URL + Copy](#quick-reply--url--copy)
- [ButtonV2](#buttonv2)
- [Carousel](#carousel)
- [Toolkit](#toolkit)
- [Why Choose Lekzo?](#why-choose-lekzo)
- [Contributing](#contributing)
- [License](#license)

---

## Features

### 🧱 Core

| Feature | Description |
|---|---|
| ⚡ **Lightweight** | Direct WebSocket connection — no Selenium, no Chromium, no headless browser. |
| 🧠 **Efficient** | Drastically lower RAM usage compared to browser-based automation. |
| 📱 **Multi-Device** | Full support for WhatsApp Multi-Device (MD) protocols. |
| 🔒 **End-to-End Encrypted** | Complete Signal protocol implementation (1:1, groups, sender-key). |
| 🛡️ **Type-Safe** | Written in TypeScript with full IntelliSense / `index.d.ts` support. |
| 🔄 **Auto Reconnect** | Built-in reconnect and message retry logic. |

### 💬 Messaging

| Feature | Description |
|---|---|
| 🔁 **Generic Relay** | Send raw message objects with `relayMessage` or the standard `sendMessage`. |
| 📝 **Simple Senders** | One-line helpers for text, image, video, audio, location, poll, and quiz messages. |
| 📊 **Polls & Quizzes** | Create polls and quizzes with a single call. |
| 🔘 **Interactive UI** | Quick reply, URL, and copy buttons, classic button menus, and carousels. |
| 👥 **Participant Mode** | Send with `ptcp: true` for participant-aware delivery. |

### 🚀 Exclusive Enhancements

| Feature | Description |
|---|---|
| 📡 **sPR Helper** | Advanced send helper with include/exclude device targeting and configurable stanza options. |
| 🔎 **Ban Checker** | `checkBan` to query a phone number's status through an external API. |
| 🍽️ **Rich Menu** | `sendRich` for responses with a header image, action buttons, carousel cards, and a link footer. |
| 🤖 **Message Builder** | Integrated `MB` namespace (AIRich, Button, ButtonV2, Carousel, Toolkit) for rich, interactive responses. |
| 🧰 **Toolkit** | Helper utilities, including MP4 frame preview generation. |

---

## Requirements

- Node.js **>= 20**
- Optional peer dependencies, depending on the features you use:
  - `sharp` or `jimp` for image processing
  - `link-preview-js` for link previews
  - `audio-decode` for audio waveform handling
  - `fluent-ffmpeg` for frame preview video (Toolkit `getMp4Preview`)

---

## Installation

```bash
npm install @whiskeysockets/baileys@github:lekzsync/Baileys
```

Or add it to your `package.json`:

```json
{
  "dependencies": {
    "@whiskeysockets/baileys": "github:lekzsync/Baileys"
  }
}
```

---

## Import

```javascript
const {
  default: makeWASocket,
  // Other Options
} = require('@whiskeysockets/baileys');
```

---

## Quick Start

### With QR Code

```javascript
const {
  default: makeWASocket,
  Browsers
  // Other Options
} = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: Browsers.ubuntu('Chrome'),
  printQRInTerminal: true
});
```

### With Pairing Code

```javascript
const {
  default: makeWASocket,
  fetchLatestWAWebVersion,
  Browsers
} = require('@whiskeysockets/baileys');

const client = makeWASocket({
  browser: Browsers.ubuntu('Chrome'),
  printQRInTerminal: false,
  version: fetchLatestWAWebVersion(),
  auth: state
});

const number = "628XXXXX";
const code = await client.requestPairingCode(number.trim()); // Use (number, "XXXXXXXX") for custom pairing

console.log("Your pairing code : " + code);
```

---

## Sending Message

### Generic Send / Relay

```javascript
// relayMessage — sends a raw message object
(async () => {
	await client.relayMessage(m.chat, {
		conversation: 'Lekzo'
	});
})();

// sendMessage — the standard way to send a message
(async () => {
	await client.sendMessage(m.chat, {
		text: 'Lekzo'
	});
})();
```

### sPR

The `sPR` helper is included in this build. It is a named export and uses the library's internal utility modules.

#### Import

```javascript
const { sPR } = require('@whiskeysockets/baileys');
```

#### Basic usage

```javascript
const messageId = await sPR(
  sock,
  '6281234567890@s.whatsapp.net',
  { conversation: 'Hello from Lekzo' }
);

console.log('Message ID:', messageId);
```

#### Options

```javascript
await sPR(
    client,
    "120363000000000000@g.us",
    {
        conversation: "Hello, group!"
    },
    {
        mode: "include",
        target: [
            "6281234567890@s.whatsapp.net",
            "628000000000@s.whatsapp.net"
        ],
        deviceMode: 'all'
    }
);
```

Available options:

| Option | Type | Default | Description |
| --- | --- | --- | --- |
| `messageId` | `string` | Generated automatically | Custom message ID |
| `additionalAttributes` | `object` | `{}` | Extra message stanza attributes |
| `useUserDevicesCache` | `boolean` | `true` | Use the device cache during recipient resolution |
| `useCachedGroupMetadata` | `boolean` | `true` | Use cached group metadata when available |
| `statusJidList` | `string[]` | — | Additional status recipients |
| `additionalNodes` | `object[]` | — | Extra stanza nodes |
| `targetMe` | `boolean` | — | Override filtering for the sender's own devices |
| `mode` | `'include' \| 'exclude'` | `'exclude'` | Select matching or non-matching devices |
| `target` | `string[]` | `[]` | Recipient JIDs, optionally including a device ID |
| `hideDecryptFail` | `boolean` | `true` | Add the `decrypt-fail="hide"` attribute where applicable |
| `deviceMode` | `'all' \| 'primary' \| 'secondary'` | `'all'` | Filter by primary or secondary device ID |

#### Important compatibility notes

- `sPR` uses internal Baileys connection methods. Keep this helper aligned with the version of this build and retest it after updating the library.
- A returned message ID means the stanza was sent to the connection; it does not confirm that every intended recipient received or displayed it.
- Recipient and device filtering does not guarantee a particular visibility outcome. Test with accounts and devices you control, and use it transparently and responsibly.
- The helper supports text and message payloads that are compatible with the underlying Baileys encoders. Some message types or WhatsApp protocol changes may require further adaptation.

### Simple Senders

#### Send Text

```javascript
(async () => {
	await client.sendText(m.chat, 'Hi!', {
		contextInfo: {
			mentionedJid: [jid]
		}
	});
})();
```

#### Send Image

```javascript
(async () => {
	await client.sendImage(m.chat, { url: './photo.jpg' }, 'Lekzo');
})();
```

#### Send Video

```javascript
(async () => {
	await client.sendVideo(m.chat, { url: './clip.mp4' }, 'Lekzo');
})();
```

#### Send Audio

```javascript
(async () => {
	await client.sendAudio(m.chat, { url: './clip.mp3' });
})();
```

#### Send Location

```javascript
(async () => {
	await client.sendLocation(m.chat, 'Lekzo', -6.2, 106.8, 'https://maps.example', '1234567890');
})();
```

#### Send Poll

```javascript
(async () => {
	await client.sendPoll(m.chat, 'Pick one', ['Option 1', 'Option 2', 'Option 3'], true);
})();
```

#### Send Quiz

```javascript
(async () => {
	await client.sendQuiz(m.chat, 'Correct answer?', ['1', '2', '3'], '2');
})();
```

### Ban Checker

`checkBan` allows you to check the WhatsApp ban status of a phone number using an external API.

#### Example

```javascript
(async () => {
	try {
		const number = '6281234567890';
		const result = await checkBan(number);

		await client.sendMessage(m.chat, {
			text: JSON.stringify(result, null, 2)
		});
	} catch (error) {
		console.error('Ban Checker Error:', error.message);
	}
})();
```

#### Usage

- Replace `6281234567890` with the phone number you want to check.
- `checkBan` must already be defined in your bot's environment.

> [!NOTE]
> Ban Checker relies on an external API. Its availability and accuracy depend on the API provider. Results are not an official confirmation of a WhatsApp account's ban status.

### Send Message with Participant

`relayMessage`:

```javascript
(async () => {
	await client.relayMessage(m.chat, {
		extendedTextMessage: {
			text: 'Lekzo'
		}
	}, {
		ptcp: true
	});
})();
```

`sendMessage`:

```javascript
(async () => {
	await client.sendMessage(m.chat, {
		text: 'Lekzo'
	}, {
		ptcp: true
	});
})();
```

### Rich Menu

`sendRich` sends a rich response with an optional header image, action buttons, carousel cards, and an open-URL footer:

```javascript
await client.sendRich(m.chat, {
  header: {
    disclaimer: true,
    disclaimerText: "github.com/lekzsync/Baileys",
    title: "Lekzo"
  },
  body: {
    title: "Select Option",
    buttons: ["Menu 1", "Menu 2"]
  },
  footer: {
    text: "WhatsApp Community",
    url: "https://whatsapp.com/channel/0029Vb863rSLtOjDrDNHqq3o"
  }
});
```

---

## Message Builder

MessageBuilder v4.7 is included directly in `lekzsync/Baileys`.

### Import

```javascript
const {
  VERSION,
  Button,
  ButtonV2,
  Carousel,
  AIRich,
  Toolkit,
  bind,
  MB
} = require('@whiskeysockets/baileys');
```

> [!NOTE]
> MessageBuilder is integrated. You don't need to install `baileys-mbuilder` separately.

### Example

```javascript
const { MB } = require('@whiskeysockets/baileys')

const rich = new MB.AIRich(sock)
  .setTitle('Lekzo')
  .setFooter('Made with AIRich')
  .addText('Halo Lekzo!')
  .addCode('javascript', `console.log('Halo Lekzo')`)
  .addTable([
    ['Feature', 'Status'],
    ['Button', 'Available'],
    ['Carousel', 'Available'],
    ['AIRich', 'Experimental']
  ])
  .addSuggest(['List Menu', 'Help', 'About Lekzo'])

await rich.send(jid)
```

---

## Button

The `Button` builder is used for native-flow interactive messages.

### Quick Reply + URL + Copy

```js
const { MB } = require('@whiskeysockets/baileys')

const msg = new MB.Button(client)
  .setTitle('Select Menu')
  .setBody('Choose one of the options below.')
  .setFooter('github.com/lekzsync/Baileys')
  .addReply('Ping', 'ping')
  .addUrl('Open Website', 'https://example.com')
  .addCopy('Copy Code', 'LEKZO')

await msg.send(m.chat)
```

---

## ButtonV2

`ButtonV2` provides a simpler classic button builder.

```javascript
const { MB } = require('@whiskeysockets/baileys')

const message = new MB.ButtonV2(client)
  .setTitle('Lekzo')
  .setSubtitle('WhatsApp Bot')
  .setBody('Choose an action.')
  .setFooter('Lekzo Baileys')
  .setThumbnail('https://example.com/xxx.jpg')
  .addButton('Menu', 'menu')
  .addButton('Ping', 'ping')

await message.send(m.chat)
```

---

## Carousel

Carousel cards are created from `Button.toCard()` and then submitted to `Carousel`.

```javascript
const { MB } = require('@whiskeysockets/baileys')

const card1 = await new MB.Button(client)
  .setImage('https://example.com/card1.jpg')
  .setBody('First card')
  .addReply('Select', 'card_1')
  .toCard()

const card2 = await new MB.Button(client)
  .setImage('https://example.com/card2.jpg')
  .setBody('Second card')
  .addUrl('Open', 'https://example.com')
  .toCard()

const carousel = new MB.Carousel(client)
  .setBody('Choose one of the cards below.')
  .setFooter('Lekzo Carousel')
  .addCard([card1, card2])

await carousel.send(jid)
```

> [!IMPORTANT]
> Each carousel card must have an image or video media attachment in its header.

---

## Toolkit

The `Toolkit` helpers are exported from the MessageBuilder namespace:

```javascript
const { MB, Toolkit } = require('@whiskeysockets/baileys')
```

> [!NOTE]
> `Toolkit.getMp4Preview` (frame preview video) requires `fluent-ffmpeg` to be installed.

---

## Why Choose Lekzo?

Lekzo is built for developers who need a lightweight, stable WhatsApp Web API without the overhead of a browser. It connects directly over WebSocket, keeps memory usage low, and ships with typed declarations and a focused set of messaging helpers, including rich responses, carousels, and a participant-aware send mode. It is a practical base for building reliable WhatsApp automation and integrations.

---

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository & create your branch (`git checkout -b feature/amazing-feature`)
2. Commit your changes (`git commit -m 'feat: add amazing feature'`)
3. Push to the branch (`git push origin feature/amazing-feature`)
4. Open a Pull Request

## License

MIT — Copyright (c) 2026 Lekzo. See [LICENSE](LICENSE) for details.

---

<div align="center">

**Lekzo** — Advanced WhatsApp Web API

[![NPM](https://img.shields.io/badge/NPM-%40lekzox%2Fbaileys-CB3837?logo=npm&logoColor=white)](https://www.npmjs.com/package/lekzsync/Baileys)
[![GitHub](https://img.shields.io/badge/GitHub-lekzox%2FBaileys-181717?logo=github)](https://github.com/lekzsync/Baileys)
[![Channel](https://img.shields.io/badge/WhatsApp-Community-25D366?logo=whatsapp)](https://whatsapp.com/channel/0029Vb863rSLtOjDrDNHqq3o)

Made with by Lekzo

</div>