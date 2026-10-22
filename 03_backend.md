# 03 Backend

**Nobody logs in.** Guests never type a name or password. The QR code on the ticket is the only thing the system needs.

---

## What runs out of sight, in order

1. **The machine starts.** The chip powers on the sensor and opens the screen page. The page shows the Waiting screen.
2. **The page checks the server.** The page sends a "are you there?" message to the server. If the server answers, the status light says **Ready**. This check repeats every 60 seconds.
3. **The sensor reads a QR code.** When a guest holds a ticket under the scanner, the sensor turns the QR code into a ticket code, for example `EVT7-00123`, and passes it to the page.
4. **The page ignores repeats.** If the same code was read in the last 3 seconds, the page ignores it, so one hold of the ticket counts as one scan.
5. **The page asks the server about the ticket.** The page shows **Checking your ticket…** and sends the ticket code to the server.
6. **The server looks the ticket up.** It searches the ticket list for that code.
   - **Not found:** it answers "not valid".
   - **Found and not yet scanned:** it marks the ticket as scanned, saves the time, and answers "welcome" with the name, row and seat. Marking and answering happen in one step, so two scans can never both get in.
   - **Found and already scanned:** it adds 1 to the ticket's refused count and answers "already scanned" with that count.
7. **The page shows the result.**
   - "welcome" → the green ✓ with the name, row and seat.
   - "already scanned" with count 1 → the plain ✗ **Entry refused.**
   - "already scanned" with count 2 or more → the ✗ with the reason: **This ticket has already been scanned. Please wait for a staff member to assist you.**
   - "not valid" → the Not valid panel.
8. **The page waits 5 seconds**, then goes back to the Waiting screen and is ready for the next guest.
9. **If the server doesn't answer within 5 seconds**, the page shows the Offline panel and asks again every 10 seconds until the server answers.

---

## Each message

| # | Message | Sent by | Received by |
|---|---|---|---|
| 1 | Ticket code read from the QR code | Sensor | Screen page |
| 2 | "Are you there?" check | Screen page | Server |
| 3 | "Yes, I'm here" | Server | Screen page |
| 4 | "Check this ticket: [code]" | Screen page | Server |
| 5 | "Welcome" + name, row, seat | Server | Screen page |
| 6 | "Already scanned" + refused count | Server | Screen page |
| 7 | "Not valid" | Server | Screen page |

---

## Each thing it remembers

### On the server (one record per ticket)

| Thing | Kind of value | Starts as | Kept after the page closes? |
|---|---|---|---|
| Ticket code | Text | The code printed in the QR code | Yes |
| Owner's name | Text | The name it was booked under | Yes |
| Row | Text | The booked row, e.g. "F" | Yes |
| Seat | Whole number | The booked seat, e.g. 12 | Yes |
| Scanned | True / false | False | Yes |
| Time scanned | Date and time | Empty | Yes |
| Refused count | Whole number | 0 | Yes |

### On the screen page

| Thing | Kind of value | Starts as | Kept after the page closes? |
|---|---|---|---|
| Current panel | Text (e.g. "waiting", "checking") | "waiting" | No |
| Last code read | Text | Empty | No |
| Time of last read | Date and time | Empty | No |
| Server online | True / false | False until the first check | No |

The page keeps nothing after it closes. Everything that matters is on the server, so restarting the machine can never let a used ticket in again.
