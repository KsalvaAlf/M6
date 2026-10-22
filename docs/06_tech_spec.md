# 06 Tech spec

## How the process works

1. The guest holds their ticket under the scanner.
2. The **sensor** reads the QR code and turns it into a ticket code (plain text). It hands that text to the screen page the same way a keyboard would type it.
3. The **screen page** shows "Checking your ticket…" and sends the code to the **server**.
4. The **server** looks the ticket up, marks it as scanned if it is new, and sends back the answer.
5. The screen page shows the right panel (✓ or ✗) for 5 seconds, then goes back to waiting.

The screen page is made of three files that run on the machine's chip.

---

## The three files

| File | What it does |
|---|---|
| **index.html** | Holds every part the guest can see: the Waiting screen, Checking panel, Welcome panel, the two Refused panels, Not valid panel, Unreadable panel, Offline panel and the status light. Only one panel is shown at a time. |
| **style.css** | Makes the screen easy to read from a step away: very large text and symbols, green for ✓, red for ✗, orange for !, and a grey or orange status light. It also hides every panel except the one in use. |
| **script.js** | Listens for the ticket code from the sensor, ignores repeats within 3 seconds, sends the code to the server, picks which panel to show from the answer, starts the 5-second timer back to waiting, checks the server every 60 seconds, and handles the Offline panel. |

---

## Libraries and framework

| Kind | Name | Reason |
|---|---|---|
| Framework | **none** | The page is one screen that swaps between a few panels. Plain HTML, CSS and JavaScript are enough, and they start fast on a small chip. |
| QR reading library | **none** | The sensor reads the QR code itself and passes on plain text, so the page doesn't need to decode images. |
| Other libraries | **none** | Sending a message to the server and setting a timer are built into JavaScript. |

---

## What is saved and where

| What | Where | Kept after the page closes? |
|---|---|---|
| The ticket list: code, name, row, seat | Server | Yes |
| Whether each ticket has been scanned, and when | Server | Yes |
| How many times each used ticket was refused | Server | Yes |
| Which panel is showing, the last code read, whether the server is online | In the page's memory only | No |

Nothing is saved on the machine itself. The server is the single source of truth.

---

## Do

- Do let the server decide every result. The page only shows what the server says.
- Do mark a ticket as scanned and send the answer in one step on the server.
- Do show the name, row and seat on the Welcome panel.
- Do show the plain "Entry refused." on the first refused try, and the reason on every try after that.
- Do return to the Waiting screen 5 seconds after any result.
- Do ignore the same code read again within 3 seconds.
- Do refuse every scan while the server can't be reached.
- Do keep the words short and the text large.

## Do not

- Do not ask anyone to log in.
- Do not save which tickets were scanned on the machine or in the browser.
- Do not let a guest in when the server hasn't answered.
- Do not undo or reset a ticket's scan from the machine. Only staff can deal with problems.
- Do not show other guests' names or seats.
- Do not use a framework or library when plain HTML, CSS and JavaScript will do.
- Do not add re-entry or exit scanning. They are not part of this scenario.
