---
layout: post
title: "The Smart Solver Behind Bulls and Cows: A Minimax Approach"
date: 2025-05-05
categories: algorithm game-theory
---

## Introduction: From Game to Algorithm

After becoming fascinated with the classic Bulls and Cows number guessing game (also known as Mastermind with numbers), I set out to develop an algorithmic solver that could crack any 4-digit code as efficiently as possible. The game's simple rules - where you get bulls (correct digit in correct position) and cows (correct digit but wrong position) as feedback - hide surprisingly complex strategic depth.

## Core Algorithm Philosophy

My solver implements the Minimax strategy from game theory, adapted for this deduction game. The fundamental principle is to always make the guess that minimizes the maximum number of remaining possible solutions in the worst-case scenario.
# The Smart Solver Behind Bulls and Cows: A Minimax Approach

## Introduction: From Game to Algorithm

After becoming fascinated with the classic Bulls and Cows number guessing game (also known as Mastermind with numbers), I set out to develop an algorithmic solver that could crack any 4-digit code as efficiently as possible. The game's simple rules - where you get bulls (correct digit in correct position) and cows (correct digit but wrong position) as feedback - hide surprisingly complex strategic depth.

## Core Algorithm Philosophy

My solver implements the **Minimax strategy** from game theory, adapted for this deduction game. The fundamental principle is to always make the guess that minimizes the maximum number of remaining possible solutions in the worst-case scenario.

### Algorithm Workflow

1. **Maintain potential solutions**: Start with all valid 4-digit numbers (1023-9876, 4536 possibilities)
2. **Filter using feedback**: After receiving bulls and cows feedback for a guessed number:
- Compare each remaining number in the potential solutions against the guessed number
- Keep only numbers that would produce the exact same bulls and cows count
- Eliminate all numbers that would produce different feedback
3. **Select Optimal Next Guess Using Minimax**: 
   From the filtered numbers:
- Consider each remaining number as a potential next guess

- For each potential guess, calculate how it would partition the remaining numbers based on possible feedback

- For each possible feedback pattern, count how many numbers would produce that pattern

- Find the maximum group size (worst-case remaining possibilities) for each potential guess

- Select the guess with the smallest maximum group size

## Example Scenario
## Step 1: initial guess
- **Game Rules**: Guess a 4-digit number with no repeating digits
- **Initial possible answers**: 1023-9876 (4,536 possibilities)
- **First guess**: "1234"
- **Feedback received**: 1 bull, 2 cows
## Step 2: Filtering with Feedback (Visualization)
### Process Flow
[All possible answers] --(Guess "1234" gets 1B2C)--> [Filtered answers]
4,536 numbers Only numbers producing 1B2C vs "1234"

### Filtering Logic
```java
// Pseudocode
for each candidateNum in potentialNumbers:
    if calculateBullsAndCows(candidateNum, "1234") != (1,2):
        remove candidateNum
```
Example Filtering:

| Number | Comparison with "1234" | Result | Action |
|--------|------------------------|--------|--------|
| 1423   | 1 bull (1), 2 cows (4,2) | 1B2C   | Keep   |
| 1245   | 2 bulls (1,2), 1 cow (4) | 2B1C   | Remove |
| 5678   | No matches             | 0B0C   | Remove |

## Step 3:Optimal Next Guess Selection (Minimax)
Decision Matrix
Remaining candidates: ["1423", "1342", "3214", "4213", "2413"]

Evaluate guess "1423":
- vs 1423: 4B0C → 1 remains
- vs 1342: 1B2C → 3 remain
- vs 3214: 0B3C → 2 remain
- Worst-case: 3 remain

Evaluate guess "2413":
- vs all → Worst-case: 2 remain
### Selection:
Choose guess with smallest worst-case remainder → "2413"

## Key Properties
1. **Information Gain**: Each guess maximizes entropy reduction

2. **Worst-Case Optimization**: Minimizes maximum remaining possibilities

3. **Efficiency**: Typically solves in 5-7 guesses
