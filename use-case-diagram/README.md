# Use Case Diagram — Airbnb Clone Backend

## Purpose
This use case diagram specifies the context of the Airbnb Clone Backend, captures the system requirements, and validates major interactions between external actors and the backend. It is used to drive implementation and generate test cases.

## Actors
- Guest
- Host
- Admin
- Payment Gateway (external)

## Major Use Cases (overview)
- Authentication: Register User, Login, Logout, Two-Factor Authentication
- Property: Search Properties, View Property Details, Manage Property (Add/Update/Delete), Manage Availability
- Booking: Book Property, Check Availability, View Booking History, Cancel Booking, Request Host Approval
- Payment: Make Payment, Process Payment, Initiate Payout, Apply Coupon, Refund Payment
- Reviews: Leave Review, Verify Booking Completed, Respond to Reviews
- Notifications & Media: Send Notification, Upload Media
- Admin: Manage Users, Manage Listings, Monitor Transactions, Handle Disputes

## Key relationships (UML)
- `<<include>>`:
  - Book Property <<include>> Check Availability
  - Book Property <<include>> Make Payment
  - Make Payment <<include>> Process Payment
  - Add/Update Property <<include>> Upload Media
  - Leave Review <<include>> Verify Booking Completed
  - Book/Cancel/Accept/Reject Booking <<include>> Send Notification
- `<<extend>>`:
  - Two-Factor Authentication <<extend>> Login
  - Apply Coupon <<extend>> Make Payment
  - Request Host Approval <<extend>> Book Property
  - Refund Payment <<extend>> Cancel Booking
- **Generalization**:
  - Register as Guest / Register as Host ──► Register User
  - Login with Email / Login with OAuth ──► Login
  - Add/Update/Delete Property ──► Manage Property

## File
- `alx-airbnb-usecase-diagram.png` — exported diagram (UML use case diagram)


