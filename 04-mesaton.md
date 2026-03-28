# Mesaton: Context Physics (ELI5)

## Two Ways to Write a Story

Imagine two kids writing a story.

**Kid #1 (Autoregressive)** writes on a really long piece of paper, left to right, never erasing. If they make a mistake, they have to write "oops, I meant to say..." and keep going. The paper just gets longer and longer. That's how most AI works today.

**Kid #2 (Diffusion / Mesaton)** has a magic whiteboard. They can erase and rewrite *any part* at any time. They can write the ending first, then go back and fix the beginning. The whiteboard always shows the *current best version* — no crossed-out words, no "oops" notes.

**Mesaton is Kid #2's magic whiteboard.** It's not just a faster way to do what Kid #1 does — it's a totally different game.

---

## The Magic Whiteboard Has Rules: Freeze, Mutate, Verify

When Kid #2 works on the whiteboard, they follow three rules:

- **Freeze** — Some parts are perfect. Cover them with a magic shield. Don't touch them.
- **Mutate** — The uncertain parts get erased and rewritten until they're good.
- **Verify** — Before declaring "done!", check that everything still makes sense together.

This is the heartbeat of Mesaton. **Freeze what's right. Fix what's uncertain. Check before committing.**

---

## Finding the Wobbly Spots (Varentropy)

How does Kid #2 know *which* parts to fix?

Imagine the whiteboard is covered in a magic glow. Words the AI is very sure about glow **dim and steady**. Words the AI is wobbly about glow **bright and flickery**.

The flickery, wobbly spots are called **high varentropy** positions. They're not just uncertain — they're *unstably* uncertain, meaning a small change there could shake up the whole story.

```
"The  cat  sat  on  the  [???]  near  the  old  [???]  by  the"
                              ↑ FLICKERY           ↑ FLICKERY
```

Mesaton targets the flickery spots first. Fix those, and the rest of the story gets more stable too. It's like fixing a wobbly table leg instead of stacking books under it.

---

## Files Are Just Whiteboard Regions

Here's a wild idea: what if the AI's whiteboard **was** the actual file on your computer?

Today, coding AIs work like this:
1. Read a file into memory
2. Think about changes
3. Write out a "diff" (instructions for changes)
4. Apply the diff to the file

With Mesaton, the file *is* the whiteboard. Edit the whiteboard, you've edited the file. No middleman. No translation. No "apply" step. The AI's working copy is always the real thing.

It's like the difference between telling someone what groceries to buy versus just reaching into the fridge yourself.

---

## Writing Backwards (Future Information Backflow)

Normal AI writing is like reading left to right — sentence 1 comes before sentence 10, and sentence 1 can't "know" what sentence 10 will say.

But humans don't actually write that way. We write a rough ending, then go back and fix the beginning so it earns the ending. We revise. We rearrange.

Mesaton can do this too:

1. Write a full draft
2. **Freeze** sentence 10 (the conclusion you love)
3. **Unfreeze** sentence 1
4. Rewrite sentence 1, now that it *knows* sentence 10 exists

The future teaches the past. This is called **future information backflow**, and it's one of Mesaton's superpowers.

---

## Induction vs. Deduction: The Two Brain Halves

- **Deduction** (autoregressive AI): "I know the cat sat down, so probably it sat on a mat." Follow the logic forward, step by step.
- **Induction** (diffusion / Mesaton): "What if the cat AND the dog AND the mat AND the tree all belong in the same scene?" Hold many possibilities at once and *fuse* them into something coherent.

The best system uses **both halves**:

| Left Brain (AR) | Right Brain (Diffusion) |
|---|---|
| Logical step-by-step | Creative exploration |
| Check consistency | Find new connections |
| Write the outline | Fill in the details |
| "Does this make sense?" | "What could this become?" |

Neither half is complete alone. Together they're much smarter.

---

## Second-Order Attention: Aiming the Eraser

Regular attention is "which words look at which other words." That's the AI's basic reading skill.

**Second-order attention** is "where should I aim the eraser right now?" It's deciding *which region* of the whiteboard to work on next.

The eraser can move in interesting patterns:
- Left to right (simple sweep)
- Back and forth like a pendulum
- Jumping to the flickery/wobbly spots
- Splitting into two erasers working in parallel

The AI can even *learn* where to aim its eraser — and eventually write down instructions like "sweep back and forth across the introduction" to guide itself.

---

## Three Real Examples

All three of these follow the same recipe: **Freeze the goal → Mutate the path → Verify → Repeat.**

### Writing a Math Proof
- **Freeze**: The problem statement, then the theorem you want to prove
- **Mutate**: The actual proof steps (the hard part)
- **Verify**: A proof-checker program says yes or no
- Wobbly spots in the proof get extra attention; once a step is verified, it gets frozen

### Refactoring Code
- **Freeze**: The tests (they describe what the code *must* do)
- **Mutate**: The implementation (rewrite it however you like)
- **Verify**: Run the tests — pass means commit, fail means try again
- The tests are the "future conclusion" that the new code must earn

### Writing a Scientific Paper
- **Freeze**: The conclusion first (what did you discover?)
- **Mutate**: The introduction (now set it up properly!)
- **Verify**: Every claim has evidence; intro and conclusion match
- The paper is written *conclusion-first*, then filled in backward — because that's how real science works

---

## The Big Idea

> **Mesaton treats text like a living world with physics, not a river flowing one direction.**

- The whiteboard (context) is the world
- The diffusion model is the laws of physics — the rules that govern how words can change
- Generation is *simulation*, not dictation

Freeze what must stay true. Let everything else evolve. Check that reality held. That's Mesaton.
