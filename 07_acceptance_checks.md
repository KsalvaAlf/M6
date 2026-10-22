# 07 Acceptance checks

Each sentence is either true or false when the system is tested.

1. When an unused ticket is scanned, the screen shows a green ✓ with the guest's name, row and seat within 5 seconds.
2. After any result, the screen goes back to the Waiting screen after 5 seconds.
3. When a ticket that has already been scanned is scanned again for the 1st refused time, the screen shows ✗ "Entry refused." and nobody is let in.
4. When the same used ticket is refused for the 2nd time, the screen shows ✗ "Entry refused. This ticket has already been scanned. Please wait for a staff member to assist you."
5. **(Something going wrong)** When the server does not answer within 5 seconds, the screen shows "The scanner cannot reach the ticket system. Please wait for a staff member." and no guest is let in until the server answers.
6. **(Edge case)** When two machines scan the same QR code at the same moment, exactly 1 guest gets ✓ and the other gets ✗.
7. **(Edge case)** When a guest holds the same ticket under the scanner without moving it, it counts as only 1 scan in any 3 seconds.
8. When a ticket code that is not in the database is scanned, the screen shows "This ticket is not valid for this event. Please see a staff member."
