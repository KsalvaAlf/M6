# 01 Overview

**7. Event entry: a ticket scans once, a second scan is refused and says why.**

**Alfred**

---

## Overview

*(Written word for word from the paper.)*

To create a machine that scans a guest or people ticket to give them entry to the event, I need to write a code and put it into an external chip with built in sensor to detect the input and show an output whether if the ticket is in the database or not. It's basically a if, else, else if loop where if the ticket is correct, it will show a checkmark which indicate welcome and x if there's an error. The way the machine work is the chip inside and sensor conneted, it will fetch the information in the server and look for the ticket's owner information and their rows and seats numbered they booked. However their information is in a qr code ticket that help reflect what they booked and paid for. Furthermore, if more than one people got the same qr code, and the second person scan it first time, error would show, second time it would show the ticket has already been scanned and pls wait for a staff to assit you with the problem.

### Earlier draft (crossed out on the paper)

1. A machine programmed to scan a ticket of people to allow them entry to the event.
2. People use it by pressing their ticket and the machine scans it and look for their info then if its in the database it gives
3. It notice the people ticket being pressed
4. It scans the ticket

---

## Answers to the questions about this overview

- **What this is:** A written design of the scenario: how the system is made and how people use it. It is not a finished build.
- **How the machine is made:** The sensor reads the QR code and passes the ticket code to the machine's screen. The screen is a web page (HTML, CSS and JavaScript) that runs on the machine. The page asks the server for the ticket's owner, row and seat, and the server remembers which tickets have already been scanned.
- **Nobody logs in.** Guests just hold their ticket under the scanner.
- **The same-QR-code mistake:** The ticket system made a mistake and printed the same QR code on two tickets. Each ticket shows a different row and seat above the QR code.
  1. Person 1 scans first and gets ✓ Welcome.
  2. Person 2 scans for the first time and gets ✗, an error with no reason.
  3. Person 2 scans a second time and gets ✗ with the reason: the ticket has already been scanned, please wait for a staff member.
- **Leaving the event:** Leaving does not use the machine, so no error shows. Re-entry is not part of this scenario.
- **The feedback below:** Recorded only. It is not part of the design.
- **Defaults chosen by Claude (not answered on paper):** the exact screen wording, a result that stays on screen for 5 seconds, a 5-second wait for the server, and the edge cases in 05.

---

## Feedback (written in blue ink by a classmate)

*(Written word for word from the paper.)*

> **Feedback (Not sure.. Sorry)** – Mark the number under the QR Code when printing the tickets so do'nt have to call staff, if Someone has 2 tickets and tickets has the same code.
>
> ```
> ┌──────┬──────────┐      ┌──────┬──────────┐
> │ [QR] │  info    │      │ [QR] │  info    │
> │  ①   │  ─────   │      │  ②   │  ─────   │
> └──────┴──────────┘      └──────┴──────────┘
> ```
>
> *(Crossed out by the reviewer: "I think … Extra system" and "if there's any option screen or button to scan the tickets")*

---

## Edited Overview

To create a machine that scans a guest's or people's ticket to give them entry to the event, I need to write a code and put it into an external chip with a built-in sensor to detect the input and show an output whether the ticket is in the database or not.

It's basically an if, else, else-if loop where if the ticket is correct, it will show a checkmark which indicates welcome, and an X if there is an error.

The way the machine works is the chip inside and the sensor connected; it will fetch the information in the server and look for the ticket's owner information and their rows and seat numbers they booked. Their information is in a QR code ticket that helps reflect what they booked and paid for.

Furthermore, if more than one person got the same QR code, and the second person scans it the first time, an error would show; the second time it would show the ticket has already been scanned and please wait for a staff member to assist you with the problem.

### Earlier draft (edited)

1. A machine programmed to scan a ticket of people to allow them entry to the event.
2. People use it by pressing their ticket and the machine scans it and looks for their info, then if it's in the database it gives…
3. It notices the people's ticket being pressed.
4. It scans the ticket.
