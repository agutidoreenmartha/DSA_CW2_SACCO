SACCO Member Account Manager
BCS 2204 Data Structures and Algorithms - Group Coursework 2 (Scenario 6)
Language: C++17 (g++ or clang++)

WHAT IT DOES
  A console program that manages the member accounts of a SACCO: add, search,
  update, delete, deposit, withdraw, transfer, apply interest, and ordered reports.
  Data is loaded from members.txt at start-up and saved back when you exit.

DATA STRUCTURES
  Hash table (written by us, in HashTable.h)
      Separate chaining, 101 buckets, key = account number. Gives fast lookup,
      insert and delete by account number (O(1) on average).
  Balanced tree (STL std::set, a red-black tree, used in Sacco.h)
      Keeps account numbers in sorted order for the range report and the full list
      (O(log n) to insert, erase and find the start of a range).

FILES
  HashTable.h    Member record, Node, and our own HashTable class
  Sacco.h        The Sacco class: all operations, validation, file load and save
  Main.cpp       Menu, input checking and screen output
  Test.cpp       The group's quick tests (20 checks)
  TestTable.cpp  Prints the full test table (55 tests: input, expected, actual, pass/fail)
  members.txt    Sample data (one member per line)

DATA FILE FORMAT (members.txt)
  accountNo,name,phone,balance
  Example: 1001,Salim Ategeka,0740496006,220000.00
  - account number: a positive whole number
  - name: not empty and must not contain a comma
  - phone: exactly 10 digits
  - balance: 0 or more
  Invalid, duplicate or incomplete lines are skipped when loading.

HOW TO COMPILE AND RUN
  Run these commands in the folder that contains all the files:

  1. Main program
       g++ -std=c++17 -Wall -Wextra -fsanitize=address -g Main.cpp -o sacco
       ./sacco

  2. Quick tests
       g++ -std=c++17 -Wall -Wextra -fsanitize=address -g Test.cpp -o test
       ./test

  3. Full test table
       g++ -std=c++17 -Wall -Wextra -fsanitize=address -g TestTable.cpp -o testtable
       ./testtable

  The -fsanitize=address flag checks for memory leaks and invalid memory access.
  A clean run prints no error text from AddressSanitizer.
  Always leave the program with option 0 so it saves and frees its memory.

MENU
   1  Add member               8  Apply interest
   2  Search member            9  Report: account number range
   3  Update member           10  Report: top savers (highest balance first)
   4  Delete member           11  Save
   5  Deposit                 12  List all members (account number order)
   6  Withdraw                13  Show hash buckets (for the demo)
   7  Transfer                 0  Save and exit

INPUT CHECKS
  Numbers must be valid (text and nan/inf are rejected), amounts must be above 0,
  phone numbers must be 10 digits, names cannot be empty or contain a comma,
  and withdrawals or transfers cannot exceed the balance. Bad input is rejected with a
  message and the program keeps running.

NOTE
  members.txt is rewritten every time you save or exit. Keep a backup copy of the
  original sample data if you want to restore it.
