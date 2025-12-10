+++
title = "Clean Code!"
description = "Write better code"
date = 2025-12-10
[taxonomies]
categories = ["coding"]
tags = ["code","improvement"]
+++

## How to write better code?

Code which is easy to read, understand, and modify is considered good. It's habit, not magic. The list below is a collection of simple, practical habits you can start today🚀

---

## 1. Keep functions small and single-purpose

A function should perform a single task effectively. A function is most likely the appropriate size if it can be summed up in one brief sentence.

**Why**: small functions are easier to test, reason about, and reuse.

**Bad (too big)**:

```go
func ProcessOrder(o Order) error {
    // validate order
    // calculate shipping
    // charge credit card
    // save to db
    // send confirmation email
    return nil
}
```

**Good (split responsibilities)**:

```go
func ProcessOrder(o Order) error {
    if err := validateOrder(o); err != nil { return err }
    if err := chargePayment(o); err != nil { return err }
    if err := saveOrder(o); err != nil { return err }
    go sendConfirmationEmail(o) // async
    return nil
}
```

Each helper (`validateOrder`, `chargePayment`, `saveOrder`) have it's own responsibilities

## 2. Use clear, intention-revealing names

Names are the primary documentation. Choose names that describe what and why, not how.

Function names: verbs or verb phrases (`CalculateTax`, `FetchUser`).

Variable names: meaningful nouns (`userCount`, `isAdmin`).

Types: nouns (`Order`, `PaymentProcessor`).

Avoid abbreviations (num is okay, but usrCnt is not).

**Bad**:

```go
a := 5
func p(u User) { /_..._/ }
```

**Good**:

```go
retryCount := 5
func processUserSignup(user User) { /_..._/ }
```

## 3. Make few comments and explain why rather than what

Code need to demonstrate its actions. Comments are made for non-obvious, specific, and logical reasons.

Bad comment (redundant):

```go
// increment i
i++
```

Good comment (explains why):

```go
// Allow 2 extra seconds because the external service may delay during peak hours.
time.Sleep(2 \* time.Second)
```

## 4. Reduce nesting; return early

Deep nesting makes logic hard to follow. Use early returns to keep the "happy path" less indented.

**Bad**:

```go
if cond1 {
    if cond2 {
        // do stuff
    } else {
        return err
    }
} else {
    return err
}
```

**Good**:

```go
if !cond1 { return err }
if !cond2 { return err }
// do stuff
```

## 5. Handle errors clearly

Handle or wrap them with context so the caller knows what failed.

```go
if err := db.Save(user); err != nil {
	return fmt.Errorf("save user %s: %w", user.ID, err)
}
```

---

Clean code is a skill you continually improve on each time you write, break, or refactor something; it's not something you master once and can brag about forever. I'm still learning, and to be honest, half of clean code is just clearing up the mess your former self caused.

**_Robert C. Martin's book Clean Code_** is a must-read if you are interested in going deeper; it's essentially the manual for writing code that won't give you nightmares in the future.

Please don't hesitate to contact me, have a conversation, or roast my code.
`the_lazy_fool` on Discord
