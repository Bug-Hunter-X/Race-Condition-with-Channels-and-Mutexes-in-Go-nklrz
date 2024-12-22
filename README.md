# Go Concurrency Bug: Race Condition with Channels and Mutexes
This repository demonstrates a common concurrency bug in Go involving race conditions with channels and mutexes. The bug occurs due to improper handling of the `WaitGroup` and channel closure, potentially leading to a deadlock.

## Bug Description
The `bug.go` file contains a program that uses goroutines to send integers to a channel. A mutex is used to protect the channel access.  However, there's a race condition because the `close(ch)` operation is not guaranteed to happen before the loop reading from the channel terminates. This can lead to the loop waiting indefinitely on a channel that will never close.

## Solution
The `bugSolution.go` file presents a corrected version that ensures proper synchronization using the WaitGroup.  The `close(ch)` operation is now performed after the WaitGroup signals that all goroutines have finished writing to the channel.

## How to reproduce the bug
1. Clone this repository.
2. Navigate to the repository's directory.
3. Run `go run bug.go` and observe the potential deadlock or unexpected behavior.
4. Run `go run bugSolution.go` to observe the corrected output.

## Note
This example highlights the importance of careful synchronization when dealing with goroutines and channels in Go. Always ensure proper usage of synchronization primitives such as mutexes and wait groups to prevent race conditions and deadlocks.