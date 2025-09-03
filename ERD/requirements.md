# Airbnb Database Entities and Relationships

## Entities
- **User**:
  - `user_id`: UUID, Primary Key, Indexed, unique identifier for users.
  - `first_name`: VARCHAR, NOT NULL, user's first name.
  - `last_name`: VARCHAR, NOT NULL, user's last name.
  - `email`: VARCHAR, UNIQUE, NOT NULL, user's email address.
  - `password_hash`: VARCHAR, NOT NULL, hashed password for security.
  - `phone_number`: VARCHAR, NULL, optional contact number.
  - `role`: ENUM (guest, host, admin), NOT NULL, user role in the system.
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP, account creation time.
- **Property**:
  - `property_id`: UUID, Primary Key, Indexed, unique identifier for properties.
  - `host_id`: Foreign Key referencing User(user_id), identifies the property host.
  - `name`: VARCHAR, NOT NULL, property name (e.g., "Cozy Apartment").
  - `description`: TEXT, NOT NULL, detailed property description.
  - `location`: VARCHAR, NOT NULL, property location (e.g., "Cairo").
  - `pricepernight`: DECIMAL, NOT NULL, price per night.
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP, creation time.
  - `updated_at`: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP, last update time.
- **Booking**:
  - `booking_id`: UUID, Primary Key, Indexed, unique identifier for bookings.
  - `property_id`: Foreign Key referencing Property(property_id), booked property.
  - `user_id`: Foreign Key referencing User(user_id), booking user.
  - `start_date`: DATE, NOT NULL, booking start date.
  - `end_date`: DATE, NOT NULL, booking end date.
  - `total_price`: DECIMAL, NOT NULL, total booking cost.
  - `status`: ENUM (pending, confirmed, canceled), NOT NULL, booking status.
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP, booking creation time.
- **Payment**:
  - `payment_id`: UUID, Primary Key, Indexed, unique identifier for payments.
  - `booking_id`: Foreign Key referencing Booking(booking_id), associated booking.
  - `amount`: DECIMAL, NOT NULL, payment amount.
  - `payment_date`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP, payment time.
  - `payment_method`: ENUM (credit_card, paypal, stripe), NOT NULL, payment method.
- **Review**:
  - `review_id`: UUID, Primary Key, Indexed, unique identifier for reviews.
  - `property_id`: Foreign Key referencing Property(property_id), reviewed property.
  - `user_id`: Foreign Key referencing User(user_id), reviewer.
  - `rating`: INTEGER, CHECK (rating >= 1 AND rating <= 5), NOT NULL, property rating.
  - `comment`: TEXT, NOT NULL, review comment.
  - `created_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP, review creation time.
- **Message**:
  - `message_id`: UUID, Primary Key, Indexed, unique identifier for messages.
  - `sender_id`: Foreign Key referencing User(user_id), message sender.
  - `recipient_id`: Foreign Key referencing User(user_id), message recipient.
  - `message_body`: TEXT, NOT NULL, message content.
  - `sent_at`: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP, message sent time.

## Relationships
- **User to Booking**: One-to-Many (one user can make multiple bookings).
- **Property to Booking**: One-to-Many (one property can have multiple bookings).
- **Booking to Payment**: One-to-One (each booking has one payment).
- **User to Property**: One-to-Many (one user, as host, can own multiple properties via host_id).
- **Property to Review**: One-to-Many (one property can have multiple reviews).
- **User to Review**: One-to-Many (one user can write multiple reviews).
- **User to Message (sender)**: One-to-Many (one user can send multiple messages).
- **User to Message (recipient)**: One-to-Many (one user can receive multiple messages).

