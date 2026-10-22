# 05 Error states

Every message shows in the middle of the machine's screen, in place of the Waiting screen.

---

## Things that can go wrong

### 1. Ticket already scanned, first refused try
- **Exact message:** ✗ **Entry refused.**
- **Where it shows:** the middle of the screen, red.
- **What the system does meanwhile:** the server adds 1 to the ticket's refused count (now 1). It does not let anyone in and does not change the original scan.
- **How it gets back to normal:** after 5 seconds the Waiting screen returns.

### 2. Ticket already scanned, second refused try onward (says why)
- **Exact message:** ✗ **Entry refused. This ticket has already been scanned. Please wait for a staff member to assist you.**
- **Where it shows:** the middle of the screen, red.
- **What the system does meanwhile:** the server adds 1 to the refused count (now 2 or more). Nobody is let in.
- **How it gets back to normal:** after 5 seconds the Waiting screen returns. A staff member checks the row and seat printed on the guest's ticket and sorts out the problem by hand.

### 3. The same QR code was printed on two tickets (the mistake from the overview)
- **What happens:** Person 1 scans and gets ✓ Welcome. Person 2 scans and gets error 1, then scans again and gets error 2 with the reason.
- **What the system does meanwhile:** it keeps Person 1's entry and refuses every later scan of that code.
- **How it gets back to normal:** staff help Person 2. The machine carries on with the next guest.

### 4. Ticket not in the database
- **Exact message:** ✗ **This ticket is not valid for this event. Please see a staff member.**
- **Where it shows:** the middle of the screen, red.
- **What the system does meanwhile:** nothing is saved, because there is no record to change.
- **How it gets back to normal:** after 5 seconds the Waiting screen returns.

### 5. QR code can't be read (creased, dirty, too dark, moved too fast)
- **Exact message:** ! **We couldn't read your ticket. Please hold the QR code still and try again.**
- **Where it shows:** the middle of the screen, orange.
- **What the system does meanwhile:** nothing is sent to the server.
- **How it gets back to normal:** after 5 seconds the Waiting screen returns, and the guest tries again.

### 6. Server can't be reached
- **Exact message:** ! **The scanner cannot reach the ticket system. Please wait for a staff member.** The status light says **Offline**.
- **Where it shows:** the middle of the screen, orange, plus the status light in the corner.
- **What the system does meanwhile:** it refuses all scans and asks the server again every 10 seconds. It never lets a guest in without the server's answer.
- **How it gets back to normal:** when the server answers, the status light says **Ready** and the Waiting screen returns.

---

## Edge cases

### Two people at once
Two guests at two entrance machines scan the same QR code at the same moment.
- **What the system does:** the server handles one request at a time. The first request marks the ticket as scanned and gets ✓ Welcome. The second finds it already scanned and gets error 1.
- **How it gets back to normal:** each machine returns to the Waiting screen after 5 seconds.

### Someone who never leaves
A guest stays at the machine and keeps holding their ticket under the scanner.
- **What the system does:** the page ignores the same code read again within 3 seconds, so one hold counts as one scan. Each panel still disappears after 5 seconds. If the ticket is used, every new scan is refused and shows the reason.
- **How it gets back to normal:** the next guest scans and the machine works as usual. Staff can ask the guest to step aside.

### Nothing for an hour
Nobody scans anything for an hour.
- **What the system does:** the Waiting screen stays on. The page checks the server every 60 seconds so the status light stays correct. Nothing is saved or changed.
- **How it gets back to normal:** it is already normal. The next scan works straight away. If the server went down during the hour, the status light already shows **Offline**.
