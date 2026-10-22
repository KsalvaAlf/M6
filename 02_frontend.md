# 02 Frontend

The visitor is a guest arriving at the event entrance. Everything they see is on the scanner machine: a screen with a scanner window below it. Nobody logs in.

---

## The screen before anyone does anything (Waiting screen)

| Part | What it shows (exact words) | What the visitor can do |
|---|---|---|
| Heading | **Welcome to the event** | Nothing, it is only read. |
| Instruction | **Please hold your ticket's QR code under the scanner.** | Hold their ticket under the scanner window. |
| Arrow | A large arrow pointing down at the scanner window | Nothing, it only shows where to hold the ticket. |
| Status light | A grey dot with the words **Ready** | Nothing. |

---

## The parts that appear after a scan

Only one of these shows at a time. Each one replaces the Waiting screen.

### 1. Checking panel
- **Shows:** a spinning circle and **Checking your ticket…**
- **When:** straight after the sensor reads a QR code, while the page waits for the server.
- **Visitor can do:** nothing. New scans are ignored until a result shows.

### 2. Welcome panel (ticket correct)
- **Shows:** a large green **✓**, then
  - **Welcome, [Name]!**
  - **Row [row] · Seat [seat]**
  - **Please go in.**
- **Visitor can do:** walk in.
- **After:** goes back to the Waiting screen after 5 seconds.

### 3. Refused panel, first refused try
- **Shows:** a large red **✗** and **Entry refused.**
- **Visitor can do:** scan the ticket again.
- **After:** goes back to the Waiting screen after 5 seconds.

### 4. Refused panel with the reason (second refused try onward)
- **Shows:** a large red **✗**, then
  - **Entry refused.**
  - **This ticket has already been scanned.**
  - **Please wait for a staff member to assist you.**
- **Visitor can do:** wait for staff.
- **After:** goes back to the Waiting screen after 5 seconds.

### 5. Not valid panel
- **Shows:** a red **✗** and **This ticket is not valid for this event. Please see a staff member.**
- **Visitor can do:** see a staff member.
- **After:** goes back to the Waiting screen after 5 seconds.

### 6. Unreadable panel
- **Shows:** an orange **!** and **We couldn't read your ticket. Please hold the QR code still and try again.**
- **Visitor can do:** hold the ticket under the scanner again.
- **After:** goes back to the Waiting screen after 5 seconds.

### 7. Offline panel
- **Shows:** an orange **!** and **The scanner cannot reach the ticket system. Please wait for a staff member.** The status light turns orange and says **Offline**.
- **Visitor can do:** wait. Scans are not accepted.
- **After:** goes back to the Waiting screen when the server answers again.

---

## What changes after each action

| Action | What changes on screen |
|---|---|
| Guest holds a ticket under the scanner | Waiting screen → Checking panel |
| Server says the ticket is correct and unused | Checking → Welcome panel (green), then back to Waiting after 5 s |
| Server says the ticket is used (first refused try) | Checking → Refused panel, then back to Waiting after 5 s |
| Same used ticket scanned again | Checking → Refused panel **with the reason**, then back to Waiting after 5 s |
| Server can't find the ticket | Checking → Not valid panel, then back to Waiting after 5 s |
| Sensor can't read the code | Waiting → Unreadable panel, then back to Waiting after 5 s |
| Server doesn't answer within 5 s | Checking → Offline panel until the server answers |
