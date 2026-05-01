# Assignment 3 - Complete Documentation

Student Name: khaled-naif
Student ID: 446540016
Date Submitted: May 1, 2026

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

Video Link: [حط رابط Google Drive هنا]

Video filename: 446540016_Assignment3_Synchronization.mp4

Verification:
✔ Link is accessible
✔ Video is 3-5 minutes
✔ Shows code and commits
✔ Clear audio
✔ Uploaded to personal Gmail

---

## Part 1: Development Log

### Entry 1 - April 30, 2026 - 6:30 PM

What I implemented:
Started the assignment and honestly just tried to understand the code first and where the problems are.

Challenges encountered:
At first I didn’t fully get where the race condition happens.

How I solved it:
I re-read the code and focused on the shared variables.

Testing approach:
Ran the program before doing anything just to see how it behaves.

Time spent: around 40 minutes

---

### Entry 2 - April 30, 2026 - 8:00 PM

What I implemented:
Added ReentrantLock for the counters.

Challenges encountered:
Was a bit confused where exactly to put lock() and unlock().

How I solved it:
Checked examples and used try-finally to be safe.

Testing approach:
Ran the program and made sure nothing broke.

Time spent: about 1 hour

---

### Entry 3 - May 1, 2026 - 3:00 PM

What I implemented:
Protected the executionLog using a lock.

Challenges encountered:
Didn’t know before that ArrayList is not thread-safe.

How I solved it:
Wrapped add() inside lock.

Testing approach:
Ran it multiple times to see if any errors show.

Time spent: 45 minutes

---

### Entry 4 - May 1, 2026 - 5:00 PM

What I implemented:
Added Semaphore to control CPU access.

Challenges encountered:
Wasn’t sure where to put acquire and release.

How I solved it:
Put acquire at the start and release inside finally.

Testing approach:
Checked that only one process runs at a time.

Time spent: around 1 hour

---

### Entry 5 - May 1, 2026 - 7:00 PM

What I implemented:
Final testing and small fixes.

Challenges encountered:
Making sure everything works together without issues.

How I solved it:
Just kept testing and adjusting.

Testing approach:
Ran the program multiple times to check stability.

Time spent: 40 minutes

---

## Part 2: Technical Questions

### Question 1: Race Conditions

One race condition is in contextSwitchCount because multiple threads can update it at the same time, which may cause incorrect values. Another one is executionLog since it is an ArrayList and not thread-safe. If multiple threads try to add elements at the same time, it can lead to inconsistent data or even exceptions. Without synchronization, results can be wrong or unpredictable.

---

### Question 2: Locks vs Semaphores

ReentrantLock is used to make sure only one thread accesses a critical section at a time. Semaphore controls how many threads can access a resource. In my code, I used ReentrantLock to protect shared variables like counters and logs. I used a Semaphore with 1 permit to simulate CPU access, so only one process runs at a time.

---

### Question 3: Deadlock Prevention

Deadlock happens when threads wait for each other and nothing moves. One way to prevent it is using try-finally so locks are always released. Another way is to avoid complicated locking or nested locks. In my code, I made sure to always release locks and semaphore in finally.

---

### Question 4: Lock Granularity Design Decision

I used separate locks for each counter. I chose this because each variable is independent, so no need to block everything with one lock. This gives better performance because threads can work in parallel. The downside is that it makes the code a bit more complex. Using one lock is simpler but reduces concurrency. So in this case, separate locks are better.

---

## Part 3: Synchronization Analysis

### Critical Section #1: Counter Variables

Which variables:
contextSwitchCount, completedProcessCount, totalWaitingTime

Why they need protection:
Because multiple threads update them at the same time.

Synchronization mechanism used:
ReentrantLock

Code snippet:

```java
contextSwitchLock.lock();
try {
    contextSwitchCount++;
} finally {
    contextSwitchLock.unlock();
}
```

Justification:
Prevents incorrect updates due to concurrent access.

---

### Critical Section #2: Execution Log

What resource:
executionLog

Why it needs protection:
Because ArrayList is not thread-safe.

Synchronization mechanism used:
ReentrantLock

Code snippet:

```java
logLock.lock();
try {
    executionLog.add(message);
} finally {
    logLock.unlock();
}
```

Justification:
Ensures safe access and avoids errors.

---

### Critical Section #3: CPU Semaphore

Purpose of semaphore:
Control access to CPU

Number of permits and why:
1 (only one process at a time)

Where implemented:
Inside run() and runToCompletion()

Code snippet:

```java
SharedResources.cpuSemaphore.acquire();
try {
    // execution
} finally {
    SharedResources.cpuSemaphore.release();
}
```

Effect on program behavior:
Makes sure processes don’t run at the same time.

---

## Part 4: Testing and Verification

### Test 1: Consistency Check

Testing procedure:
Ran the program multiple times.

Results:
The program worked fine without errors and results looked consistent.

Why synchronization is necessary:
Without it, shared variables could get wrong values and logs might break.

Conclusion:
Synchronization keeps results correct.

---

### Test 2: Exception Testing

Testing procedure:
Checked if any ConcurrentModificationException appears.

Results:
No exceptions happened.

What this proves:
executionLog is properly protected.

---

### Test 3: Correctness Verification

Expected values:
All processes finish correctly.

Actual values:
Program output looks correct.

Analysis:
Everything works as expected.

---

### Test 4: Different Scenarios

Scenario tested:
Different number of processes

Purpose:
Check stability

Results:
Program still worked fine

What I learned:
Synchronization is reliable

---

## Part 5: Reflection and Learning

What I learned about synchronization:
At first it was confusing, but I understood that race conditions happen when multiple threads access the same data. Using locks and semaphores helps control that. I also learned that even simple variables can cause problems if not protected. After testing, I saw how important synchronization is to keep results correct.

Real-world applications:

Example 1:
Bank systems where multiple users access the same account.

Example 2:
Operating systems scheduling processes.

How I would explain synchronization:
It’s like letting one person use something at a time so no one messes things up.

---

## Part 6: GitHub Repository Information

Repository URL:
https://github.com/khaled-naif-446/OS-Assignment3-khaled-naif-4465/tree/main

Number of commits:
4

Commit messages:

1. Set student ID
2. Added locks
3. Added semaphore
4. Final testing

---

## Summary

Total time spent on assignment:
Around 4–5 hours

Key takeaways:

1. Learned about race conditions
2. Learned how locks work
3. Learned how semaphores control threads

Most challenging aspect:
Understanding synchronization at the beginning

What I'm most proud of:
Getting everything to work correctly without errors

---
