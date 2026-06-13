<div align="center">

<img src="https://camo.githubusercontent.com/c1f3b7dcf8145e1a0d91e90aae2b7080e761e88b7d770e0e8429c369d7311425/68747470733a2f2f66696c65732e636174626f782e6d6f652f6335733967302e6a7067" alt="WhatsApp Baileys" width="100%" />

<br/>
<br/>

# @ky-dev/baileys

<p>
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" />
  <img src="https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white" />
  <img src="https://img.shields.io/badge/WebSocket-010101?style=for-the-badge&logo=socketdotio&logoColor=white" />
  <img src="https://img.shields.io/badge/Open%20Source-FF4500?style=for-the-badge&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/license-MIT-blue?style=for-the-badge" />
</p>

**Open-source WhatsApp automation library 2014 no browser required.**  
Built on WebSocket for speed, stability, and full multi-device support.

<br/>

[Installation](#getting-started)
</div>

## What is @ky-dev/baileys?

**@skycodee/baileys** is a powerful, open-source library for developers who need reliable WhatsApp automation without the overhead of a browser. Powered by **WebSocket technology**, it supports message management, group administration, interactive messages, and action buttons all in a lightweight and modular package.

Actively maintained with continuous improvements to **pairing stability**, **session management**, and **WhatsApp multi-device compatibility**.

Perfect for:
- Business bots & chat automation
- Customer service systems
- Broadcast & notification tools
- E-commerce integrations

---

## Main Features

| Feature | Description |
|---|---|
| **Custom Pairing** | Stable pairing with your own codes no disconnection issues |
| **Interactive Messages** | Buttons, menus, native flows, and more |
| **Session Management** | Automatic, efficient, and long-term stable |
| **Multi-Device Support** | Fully compatible with WhatsApp's latest multi-device API |
| **Lightweight & Modular** | Easy to integrate into any Node.js project |
| **Rich Documentation** | Comprehensive guides and example code included |
| **Secure Auth** | Improved authentication flow with fixed prior vulnerabilities |

---

## Getting Started

Install via npm or yarn:

```bash
npm install @whiskeysockets/baileys
# or
yarn add @whiskeysockets/baileys
```

Then import and initialize:

```javascript
const { makeWASocket, useMultiFileAuthState } = require("@whiskeysockets/baileys");

const { state, saveCreds } = await useMultiFileAuthState("auth_info");
const sock = makeWASocket({ auth: state });

sock.ev.on("creds.update", saveCreds);
```

---

## Additional Functions

### Get Channel ID
```javascript
await sock.newsletterId(url);
```

### Check Banned Number
```javascript
await sock.checkWhatsApp(target);
```

---

## SendMessage Documentation

<details>
<summary><b>Group Status Message (V2)</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    groupStatusMessage: {
        text: "Hello World"
    }
});
```
</details>

<details>
<summary><b>Album Message (Multiple Images)</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    albumMessage: [
        { image: cihuy, caption: "First photo" },
        { image: { url: "IMAGE_URL" }, caption: "Second photo" }
    ]
}, { quoted: m });
```
</details>

<details>
<summary><b>Event Message</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    eventMessage: {
        isCanceled: false,
        name: "Event Name",
        description: "Event description here",
        location: {
            degreesLatitude: 0,
            degreesLongitude: 0,
            name: "Location Name"
        },
        joinLink: "https://call.whatsapp.com/video/example",
        startTime: "1763019000",
        endTime: "1763026200",
        extraGuestsAllowed: false
    }
}, { quoted: m });
```
</details>

<details>
<summary><b>Poll Result Message</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    pollResultMessage: {
        name: "Poll Title",
        pollVotes: [
            { optionName: "Option A", optionVoteCount: "112233" },
            { optionName: "Option B", optionVoteCount: "1" }
        ]
    }
}, { quoted: m });
```
</details>

<details>
<summary><b>Simple Interactive Message</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @Xskycode",
        buttons: [
            {
                name: "cta_copy",
                buttonParamsJson: JSON.stringify({
                    display_text: "Copy Code",
                    id: "123456789",
                    copy_code: "ABC123XYZ"
                })
            }
        ]
    }
}, { quoted: m });
```
</details>

<details>
<summary><b>Interactive Message with Native Flow</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @Xskycode",
        image: { url: "https://example.com/image.jpg" },
        nativeFlowMessage: {
            messageParamsJson: JSON.stringify({
                limited_time_offer: {
                    text: "Limited offer text",
                    url: "https://t.me/Xskycode",
                    copy_code: "PROMO2024",
                    expiration_time: Date.now() * 999
                },
                bottom_sheet: {
                    in_thread_buttons_limit: 2,
                    divider_indices: [1, 2, 3, 4, 5, 999],
                    list_title: "List Title",
                    button_title: "Button Title"
                },
                tap_target_configuration: {
                    title: "Title",
                    description: "Description text",
                    canonical_url: "https://t.me/Xskycode",
                    domain: "shop.example.com",
                    button_index: 0
                }
            }),
            buttons: [
                {
                    name: "single_select",
                    buttonParamsJson: JSON.stringify({ has_multiple_buttons: true })
                },
                {
                    name: "call_permission_request",
                    buttonParamsJson: JSON.stringify({ has_multiple_buttons: true })
                },
                {
                    name: "single_select",
                    buttonParamsJson: JSON.stringify({
                        title: "Select an Option",
                        sections: [
                            {
                                title: "Section Title",
                                highlight_label: "Label",
                                rows: [
                                    {
                                        title: "Row Title",
                                        description: "Row description",
                                        id: "row_1"
                                    }
                                ]
                            }
                        ],
                        has_multiple_buttons: true
                    })
                },
                {
                    name: "cta_copy",
                    buttonParamsJson: JSON.stringify({
                        display_text: "Copy Code",
                        id: "123456789",
                        copy_code: "ABC123XYZ"
                    })
                }
            ]
        }
    }
}, { quoted: m });
```
</details>

<details>
<summary><b>Interactive Message with Thumbnail</b></summary>
<br/>

```javascript
await sock.sendMessage(target, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @Xskycode",
        image: { url: "https://example.com/image.jpg" },
        buttons: [
            {
                name: "cta_copy",
                buttonParamsJson: JSON.stringify({
                    display_text: "Copy Code",
                    id: "123456789",
                    copy_code: "ABC123XYZ"
                })
            }
        ]
    }
}, { quoted: m });
```
</details>
