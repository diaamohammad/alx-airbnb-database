# Normalization Process for Airbnb Database

## Introduction
The Airbnb database design (User, Property, Booking, Payment, Review, Message) was normalized to ensure data integrity, eliminate redundancy, and optimize performance. The following steps confirm compliance with 1NF, 2NF, and 3NF.

## 1NF (First Normal Form)
- **Requirement**: Each table has a Primary Key, no repeating groups, and atomic values.
- **Implementation**:
  - All tables (User, Property, Booking, Payment, Review, Message) have unique Primary Keys (e.g., `user_id`, `property_id`, `booking_id`).
  - Attributes are atomic (e.g., `first_name`, `email` in User are single values).
  - No repeating groups (e.g., no multiple values in a single column like `phone_number`).

## 2NF (Second Normal Form)
- **Requirement**: Must be in 1NF, and non-key attributes fully depend on the entire Primary Key.
- **Implementation**:
  - All tables use single-column Primary Keys (e.g., `user_id` in User, `booking_id` in Booking), so no partial dependencies exist.
  - Non-key attributes (e.g., `email`, `first_name` in User) depend fully on `user_id`.
  - Example: In Booking, `start_date`, `end_date`, `total_price` depend on `booking_id`, not partially on `user_id` or `property_id`.

## 3NF (Third Normal Form)
- **Requirement**: Must be in 2NF, with no transitive dependencies (non-key attributes depend only on the Primary Key, not other non-key attributes).
- **Implementation**:
  - No transitive dependencies exist. For example:
    - In User, `email` depends on `user_id`, not on `first_name` or `last_name`.
    - In Property, `pricepernight` depends on `property_id`, not on `location` or `description`.
  - Foreign Keys (e.g., `host_id` in Property, `booking_id` in Payment) link tables without introducing transitive dependencies.

## Conclusion
The Airbnb database design is in 3NF, ensuring no data redundancy, efficient storage, and maintainable relationships.


