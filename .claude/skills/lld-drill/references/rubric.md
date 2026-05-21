# LLD Drill Evaluation Rubric

## Entities Identified

**✓ Pass** — All core entities present. No critical entity missing.
**Partial** — 1 minor entity missing (e.g., forgot `Ticket` but got everything else).
**✗ Not yet** — Missing a primary entity (e.g., no `Order` in a food ordering system).

## Attributes Present

**✓ Pass** — Each class has at least the key fields. Types implied or explicit.
**Partial** — Attributes listed for some classes but not all. Key fields present.
**✗ Not yet** — Only class names, no attributes at all.

## Method Signatures

**✓ Pass** — Methods have parameter types and return types. Placed on the correct class.
**Partial** — Methods listed but missing return types or one misplaced.
**✗ Not yet** — Methods named but no signatures, or majority misplaced.

## Ownership Correct

**✓ Pass** — Each method lives on the class that performs the action (actor owns the method).
**Partial** — One method misplaced but reasoning is understandable.
**✗ Not yet** — Fundamental misplacement (e.g., `place_order()` on `Restaurant`).

---

## Common Patterns (remind candidate when missed twice)

### Transaction Entity Rule
When two entities interact through a verb (borrow, park, order, reserve, book), a third entity tracks the transaction:
- Borrow book → `Loan`
- Park vehicle → `Ticket`
- Place order → `Order`
- Reserve seat → `Reservation`
- Book hotel room → `Booking`

### Actor Owns the Method
Ask "who does this?" The subject of that sentence owns the method.
- "Customer places an order" → `Customer.place_order()`
- "Member borrows a book" → `Member.borrow()`
- "Game checks for a winner" → `Game.check_winner()`

### Enum for States and Categories
Any time requirements list discrete states or size/type categories, use an enum:
- Order states → `OrderStatus(Enum)`
- Spot sizes → `SpotSize(Enum)`
- Vehicle types → `VehicleType(Enum)`

### Constraint Needs an Attribute
Any stated constraint implies an attribute to enforce it:
- "Max 3 books" → `Member.active_loans: List[Loan]`
- "Spot fits vehicle size" → `Spot.fits(vehicle) -> bool`
- "One booking per timeslot" → check against `reservations: List[Reservation]`

### Entity Archetypes (fast pattern matching)
| Problem type | Core entities |
|---|---|
| Board games | `Game`, `Player`, `Board`, `Piece`, `Die` |
| Booking systems | `User`, `Resource`, `Reservation`, `Schedule` |
| Payment / wallet | `Account`, `Transaction`, `Ledger` |
| Inventory / vending | `Item`, `Inventory`, `Order`, `Payment` |
| Library / rental | `Item`, `Member`, `Loan`, `Catalog` |
| Ride sharing | `Rider`, `Driver`, `Trip`, `Location` |
