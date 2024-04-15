# Mutex Practice

## Building

Command line:

* `make` to build. An executable called `reservations` will be produced.

## Using the executable:

To run the program:
- `seat_count`: Total number of seats available.
- `broker_count`: Number of brokers (threads) simulating the reservations.
- `transaction_count`: Number of transactions each broker will attempt.

Example: 
./reservations 100 10 5000

## Files

* `reservations.c`: All of the code to run the program
* `Makefile`: File which builds an executable

## Data

This program uses a dynamic array (`seat_taken`) to track the status of each seat:
- `1` if the seat is taken.
- `0` if the seat is free.

`seat_taken_count` is a global counter tracking the number of seats currently reserved.

## Functions

Overview of functions and their hierarchy:

- `main()`
  - Initializes program data from command line arguments.
  - Creates and starts broker threads.
  - Waits for all threads to complete.
- `reserve_seat(int n)`
  - Attempts to reserve a seat. Returns `0` on success, `-1` if the seat is already taken.
- `free_seat(int n)`
  - Attempts to free a reserved seat. Returns `0` on success, `-1` if the seat is already free.
- `is_free(int n)`
  - Checks if a seat is free. Returns `1` (true) if free, `0` (false) if taken.
- `verify_seat_count()`
  - Verifies the count of taken seats matches the recorded count.
- `seat_broker(void *arg)`
  - Thread function for brokers handling seat transactions.

## Synchronization

The system uses a single mutex (`pthread_mutex_t lock`) to ensure mutual exclusion when brokers access or modify the shared seat data (`seat_taken` and `seat_taken_count`).

## Notes

- The system simulates a simple model of concurrent transactions analogous to real-world systems like ticket booking.
