# LLD Drill Problem Bank

Problems are ordered from simpler to more complex. Use in order during a session unless the candidate specifies otherwise.

---

## 1. Parking Lot
- A parking lot has multiple floors, each with multiple spots
- Spots can be: small, medium, large
- Vehicles can be: motorcycle, car, truck
- A vehicle can only park in a spot that fits its size
- Support: park a vehicle, unpark a vehicle, check availability

## 2. Food Ordering System
- Customers can browse restaurants and their menus
- A customer places an order with one or more items from a single restaurant
- Orders go through states: placed → preparing → out for delivery → delivered
- Support: place order, cancel order, track order status

## 3. Library Management System
- A library has books, and each book can have multiple copies
- Members can borrow and return books
- A member can borrow at most 3 books at a time
- If a book is unavailable, a member can reserve it
- Support: borrow book, return book, reserve book, search book by title/author

## 4. Hotel Booking System
- A hotel has rooms of different types: single, double, suite
- Guests can book a room for a date range
- A room cannot be double-booked
- Bookings can be cancelled with a reference number
- Support: search available rooms, book a room, cancel a booking

## 5. ATM Machine
- A user inserts a card and enters a PIN
- The ATM verifies the card and PIN against an account
- Supported transactions: check balance, withdraw, deposit
- Withdrawal fails if balance is insufficient
- Each transaction is logged

## 6. Ride Sharing (Uber simplified)
- Riders can request a trip from a pickup to a destination
- Drivers can accept or decline a trip request
- A trip goes through states: requested → accepted → in progress → completed
- Support: request trip, accept trip, complete trip, calculate fare

## 7. Elevator System
- A building has multiple elevators and multiple floors
- Users press a button on a floor to request an elevator (up or down)
- Users press a button inside the elevator to select a destination floor
- An elevator can be: idle, moving up, moving down
- Support: request elevator, select floor, dispatch elevator

## 8. Movie Ticket Booking
- A theater has multiple screens, each showing a movie at specific showtimes
- Each showtime has numbered seats
- A user can book one or more seats for a showtime
- A booked seat cannot be booked by another user
- Support: search showtimes, book seats, cancel booking

## 9. Tic-Tac-Toe
- Two players take turns marking a 3x3 grid
- A player wins by getting 3 in a row (horizontal, vertical, diagonal)
- The game ends in a draw if all cells are filled with no winner
- Support: make a move, check winner, check draw, reset game

## 10. Online Shopping Cart
- Users can browse products and add them to a cart
- A cart belongs to one user and contains one or more items with quantities
- Inventory decreases when an order is placed
- Orders go through states: pending → confirmed → shipped → delivered
- Support: add to cart, remove from cart, place order, track order

## 11. Chess Game
- Two players play on an 8x8 board
- Each piece type (king, queen, rook, bishop, knight, pawn) has different movement rules
- A move is invalid if it puts the moving player's king in check
- Support: make a move, validate move, check for check/checkmate

## 12. Vending Machine
- A vending machine holds items with quantities and prices
- A user inserts coins, selects an item, and receives it plus change
- The machine rejects a selection if balance is insufficient or item is out of stock
- Support: insert coin, select item, dispense item, return change

## 13. Social Media Feed (simplified)
- Users can post content and follow other users
- A user's feed shows posts from users they follow, newest first
- Users can like and comment on posts
- Support: create post, follow user, get feed, like post, comment on post

## 14. Rate Limiter
- A service needs to limit API calls per user to N requests per time window
- If a user exceeds the limit, requests are rejected until the window resets
- Support: allow request (returns true/false), get remaining quota
- Consider: fixed window vs sliding window as a discussion point

## 15. Cache (LRU)
- A cache stores key-value pairs up to a fixed capacity
- When full, the least recently used item is evicted
- Support: get(key), put(key, value)
- Constraint: both operations must be O(1)
