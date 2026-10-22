# 04 Flow chart

**Key:** `[ box ]` = an action  ·  `< diamond >` = a question  ·  every question has a number (Q1–Q5) and a **yes** and a **no** path. Every path ends by going back to **START**.

```
                    ┌──────────────────────────────────┐
     ┌────────────► │  START: Waiting screen           │
     │              │  "Please hold your ticket's QR   │
     │              │   code under the scanner."       │
     │              └────────────────┬─────────────────┘
     │                               │
     │              [ Guest holds ticket under scanner ]
     │                               │
     │                 < Q1: Could the sensor read     >
     │                 <     the QR code?              > ──no──► [ Show "We couldn't read your ticket…" ]
     │                               │ yes                            │ wait 5 s
     │                               │                                ▼
     │                               │                           back to START
     │                               │
     │                [ Show "Checking your ticket…" ]
     │                [ Send ticket code to server   ]
     │                               │
     │                 < Q2: Did the server answer     >
     │                 <     within 5 seconds?         > ──no──► [ Show Offline panel ]
     │                               │ yes                            │ ask again every 10 s
     │                               │                                ▼
     │                               │                     server answers → back to START
     │                               │
     │                 < Q3: Is the ticket in the      >
     │                 <     database?                 > ──no──► [ Show "This ticket is not valid…" ]
     │                               │ yes                            │ wait 5 s → back to START
     │                               │
     │                 < Q4: Has the ticket already    >
     │                 <     been scanned?             > ──no──► [ Mark ticket as scanned ]
     │                               │ yes                       [ Show ✓ Welcome, Name, Row, Seat ]
     │                               │                                │ wait 5 s → back to START
     │                [ Add 1 to the refused count ]
     │                               │
     │                 < Q5: Is the refused count      >
     │                 <     exactly 1?                > ──yes─► [ Show ✗ "Entry refused." ]
     │                               │ no                             │ wait 5 s → back to START
     │                               │
     │                [ Show ✗ "Entry refused. This ticket has already been scanned. ]
     │                [       Please wait for a staff member to assist you."         ]
     │                               │ wait 5 s
     └───────────────────────────────┘
```

## The same chart in words

1. **START:** the Waiting screen.
2. A guest holds a ticket under the scanner.
3. **Q1 — Could the sensor read the QR code?**
   - No → show the Unreadable panel, wait 5 s, back to START.
   - Yes → go to step 4.
4. Show "Checking your ticket…" and send the code to the server.
5. **Q2 — Did the server answer within 5 seconds?**
   - No → show the Offline panel, ask again every 10 s, and when the server answers go back to START.
   - Yes → go to Q3.
6. **Q3 — Is the ticket in the database?**
   - No → show the Not valid panel, wait 5 s, back to START.
   - Yes → go to Q4.
7. **Q4 — Has the ticket already been scanned?**
   - No → mark it scanned, show ✓ Welcome with name, row and seat, wait 5 s, back to START.
   - Yes → add 1 to the refused count and go to Q5.
8. **Q5 — Is the refused count exactly 1?**
   - Yes → show ✗ "Entry refused.", wait 5 s, back to START.
   - No → show ✗ with the reason "This ticket has already been scanned. Please wait for a staff member to assist you.", wait 5 s, back to START.
