

## Date Module

Handles all date-related functionality required by the system.

**Implemented capabilities:**
- Validates calendar dates with correct leap-year logic  
- Computes the number of days in any month  
- Converts dates to a continuous serial count  
- Calculates the number of days between two dates  

These functions support the donation-spacing rules and ensure data consistency.

---

## BloodDonation Module

Represents and validates a single blood donation.

**Includes:**
- ID validation (`exactly 6 digits`)
- Age validation
- Weight validation
- Date validation through the Date module
- Parsed `Date` object storage
- Deterministic `validate()` result codes (`OK`, `BAD_ID`, `BAD_AGE`, etc.)

This module guarantees that only structurally valid donations reach the account layer.

---

## VacationAccount Module

Stores accepted donations for a single donor and manages earned vacation credit.

**Core functionality:**
- Ensures donations belong to the correct donor
- Rejects same-day donations  
- Rejects donations less than 180 days apart  
- Awards 4 vacation hours per valid donation  
- Provides read-only accessors: donor ID, total hours, number of donations, indexed lookup  

**Memory-safety features:**
- Manual dynamic array of `BloodDonation*`  
- `ensureCapacity()` for controlled resizing  
- `clear()` to delete all owned items  
- `deepCopyFrom()` for cloning state  
- Fully implemented Rule of Three to prevent leaks and double-frees  

This module ensures correctness, fairness, and system robustness.

---

## Testing

The `main.cpp` file includes a comprehensive set of `assert()` tests verifying:

- All validation error codes  
- Boundary values (age, weight, ID formatting)  
- Leap-year and invalid-date scenarios  
- Exact 180-day spacing  
- Same-day rejection  
- Multiple successful donations  
- Correct accumulation of vacation hours  
- Proper deep copying and assignment of `VacationAccount` objects  

All tests pass.

---

## Build Instructions

g++ Date.cpp BloodDonation.cpp VacationAccount.cpp main.cpp -o proj1 -std=c++17
./proj1


