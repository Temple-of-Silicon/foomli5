# SAGE: The AI's Imagination Room

## What's the Problem?

Imagine you have a friend who can only talk in a long line of words — one word, then the next, then the next. Now ask that friend to describe a maze. They *can* do it ("there's a wall on the left, then a path that goes right, then another wall..."), but it's really hard! They can't just *see* the maze all at once.

That's the problem regular AI language models have. They think in **one long line**, but the real world is **two-dimensional** — it has up, down, left, right, near, far. Things have neighbors. Things have shapes. Forcing all of that into a single line is like trying to fold a map into a single sentence.

**SAGE** is the fix. It gives the AI an **imagination room** — a grid, like graph paper — where it can actually *draw* things out and think about them spatially.

---

## What Is SAGE?

**SAGE** stands for *Semantic Automaton in Geometric Embedding-space*. That's a mouthful, so just think of it as the AI's **mental sketchpad**.

It has three parts that work together like a team:

### 1. The Translator (Language Interface)
This is the part that speaks English (or any language). It:
- **Reads** the problem you give it
- **Draws** the problem onto the sketchpad
- **Reads back** what the sketchpad figured out and explains it to you

Think of it like a librarian who reads your question, walks into the map room, finds the answer, then comes back and explains it.

### 2. The Sketchpad (Geometric World-State)
This is a **grid** — like a giant piece of graph paper — where every square can hold information.

If the AI is thinking about a maze:
- Squares with walls get a "wall" label
- Open squares get an "open path" label
- The starting point gets a "start" label
- The finish gets a "goal" label

The sketchpad **sticks around** while the AI is thinking. It doesn't disappear and get redrawn from scratch every second. The AI can keep coming back to it, changing it, adding to it — like a whiteboard that doesn't get erased.

### 3. The Thinking Engine (World-Evolution Engine)
This is the part that actually **solves things** by evolving the sketchpad over time.

Here's a fun example — imagine the AI is solving a maze:

```
Start                      After a few steps         Solved!
. . # . . . .              . . # . . 2 1             8 7 # 5 4 2 1
. # # . # . .              . # # . # 3 2             . # # 6 # 3 2
S . . . # . .    →         . . . . # 4 3    →        7 6 5 4 # 4 3
. # . # . . .              . # . # 5 5 4             8 # 6 # 5 5 4
. . . # # . .              . . . # # 6 5             9 8 7 # # 6 5
. # . . . # .              . # . . . # 6             . # 8 7 6 # 6
. . . . . . G              . . . . . . 0             . . 9 8 7 . G
```

The numbers spread out from the **Goal** like ripples in a pond, one step at a time, until they reach the **Start**. Then you just follow the numbers downhill to find the shortest path!

The AI does this with hundreds or thousands of tiny steps — each step is super cheap and fast. It's like doing lots of small easy calculations instead of one giant hard one.

---

## Why Use Meaning Instead of Just Numbers?

Here's a clever trick SAGE uses. Instead of labeling squares with plain numbers (0 = empty, 1 = wall), it uses **meaning-filled labels** — like the actual *concept* of "wall."

Why does that matter? Because the AI has learned that "wall," "barrier," "obstacle," and "blockage" all **mean roughly the same thing**. They're neighbors in the AI's understanding of language.

So if you trained the AI on mazes with "walls," it can automatically handle mazes with "barriers" — because the meaning is so close that the same tricks work. It's like knowing how to ride a bike and then being able to ride a slightly different bike without re-learning from scratch.

This also means the AI can handle complex ideas like a **"crumbling wall"** (different from a solid wall) or a **"permeable barrier"** (you can sort of get through it). The meaning shifts naturally — the AI doesn't need special rules for every new word.

---

## Object Permanence: Keeping Track of Stuff

Here's a problem toddlers solve around age 1: if you hide a toy under a blanket, it's still there. The toy didn't disappear. Psychologists call this **object permanence**.

Language-only AIs struggle with this in complex situations. If you have 10 characters doing things in a story, keeping track of who is where and what they're holding gets really messy in a long line of words.

SAGE solves this naturally: **things live at locations on the grid**. The cat is at square (3, 5). The cat doesn't disappear between sentences — it stays at (3, 5) until something moves it. Object permanence comes for free!

This also means the AI can:
- **Track trajectories** — where did the cat come from? where is it going?
- **Run simulations** — what happens if I move the cat here?
- **Reason about time** — what did the grid look like 5 steps ago?

---

## Three Ways to Build the Thinking Engine

There's more than one way to build the "evolving sketchpad" part:

- **Cellular Automata** — Like Conway's Game of Life: each square only looks at its neighbors to decide what to do next. Simple rules, local interactions. Great for things like maze-solving and spreading information. Trains on small grids, works on big ones!

- **Diffusion** — Like an artist sketching a blurry picture that slowly sharpens. The whole grid updates at once, using attention to look at everything simultaneously. More powerful but heavier to compute.

- **Recurrent Memory** — A blend of the two: some things look locally, some things have a global memory. Can even track its own thinking progress!

All three share the same basic idea: **the grid evolves step by step until the answer emerges**.

---

## The Imagination Room

The really exciting part: **the sketchpad keeps existing even when the AI isn't talking to you**.

Between your questions, the AI can keep running simulations, trying things out, exploring possibilities — all silently, on its internal grid. This is what "imagination" means for an AI: a durable workspace where you can build, test, and modify ideas without having to say them out loud.

This gives SAGE four superpowers:

- **Debuggable** — if the AI gets the wrong answer, you can look at the grid and see exactly where things went wrong
- **Reusable** — solved pieces can be saved and snapped together like LEGO bricks
- **"What if?" thinking** — copy the grid, try a different scenario, compare the results
- **Time-aware** — the sequence of grid states is like a film strip showing cause and effect

---

## Still Hard Problems (The Dragons)

SAGE is exciting, but some things are still unsolved:

- **Too much in one square** — a location might need to be "empty" AND "lit up" AND "recently visited" all at once. How do you cram that in?
- **Meanings shifting during training** — if the AI keeps learning, the meaning of "wall" might slowly drift, breaking rules it already learned.
- **Knowing when to use the sketchpad** — not every question needs a grid. Learning when to skip it (and save effort) is its own puzzle.
- **Does bigger actually work better?** — the theory is great, but we still need lots of experiments to prove it works at large scale.

---

## The Big Picture

SAGE gives AI a way to **think in space, not just in sentences**. It's like the difference between:

- Describing a maze in words (exhausting, easy to get lost)
- Drawing the maze and solving it visually (natural, fast, checkable)

When language, geometry, and a step-by-step evolution engine work together, the AI can tackle problems that are genuinely *spatial* — mazes, maps, physics, planning, multi-agent coordination — without cramming everything through the narrow bottleneck of a single sentence.

**Imagination, it turns out, is just a sketchpad that sticks around.**

---

## Now You Speak Fancy

So you've learned the ELI5 version. Here's how to say all of it at a dinner party where everyone works in AI research.

| ELI5 Version | Fancy Term | What It Really Means |
|---|---|---|
| The AI's imagination room / mental sketchpad | **Externalized imagination substrate** | A persistent, inspectable geometric buffer the model can evolve and edit between language steps — as opposed to hiding all "thinking" inside opaque parameter weights |
| Thinking in one long line | **1D sequence / token narrative** | How standard language models process everything: one token after the next, which makes spatial structure implicit, expensive, and easy to lose |
| Forcing a map into a single sentence | **Dimensionality bottleneck** | The structural cost of compressing 2D (or higher-dimensional) spatial information into a 1D token sequence, hiding adjacency, locality, and symmetry |
| The sketchpad (graph paper grid) | **Geometric world-state** | A structured latent space — typically a 2D grid — where each cell holds information about what occupies that location |
| The Thinking Engine | **Spatial inference engine / world-evolution engine** | The learned dynamical system that updates the world-state through iterative steps until a solution emerges |
| Ripples spreading from the goal | **Breadth-first / constraint propagation dynamics** | A local update rule where each cell sets its value to `1 + min(neighbor)` over passable neighbors, globally solving pathfinding through purely local steps |
| Meaning-filled labels instead of plain numbers | **Semantic embedding grid** | Grid cells that hold continuous high-dimensional vectors from the language model's semantic space rather than discrete symbolic labels |
| "Wall" and "barrier" meaning nearly the same thing | **Semantic similarity / embedding proximity** | Concepts with related meanings occupy nearby points in vector space, so dynamics trained on one word transfer automatically to synonyms |
| Squares holding concepts like "crumbling wall" | **Compositional semantic representations** | Embedding vectors that naturally blend modifiers (e.g. "crumbling," "permeable") with base concepts through geometric relationships in the embedding manifold |
| The toy under the blanket still exists | **Object permanence** | The cognitive property that entities continue to exist at their locations even when not being actively attended to — SAGE gets this for free because objects are pinned to grid cells |
| Keeping track of who is where | **Entity binding / object tracking** | Maintaining distinct identities for multiple entities across time steps; hard in pure language models, explicit in a spatial substrate |
| Simple rules, one square looking at neighbors | **Neural Cellular Automata (NCA)** | A world-evolution engine where a single tiny network applies the same local update rule to every cell simultaneously, giving strong locality and translation-invariance biases |
| Blurry picture that slowly sharpens | **Latent diffusion variant** | A world-evolution engine that uses attention-based global denoising over the full grid, trading locality for the ability to coordinate long-range spatial structure |
| A blend of local rules and global memory | **Recurrent memory kernel** | A hybrid engine with structured recurrent processing over the grid, capable of maintaining hidden state about its own reasoning progress |
| The sketchpad that keeps existing between questions | **Persistent world-state / working memory** | The grid survives across reasoning steps and language turns, allowing incremental construction and inspection rather than rebuilding from scratch each time |
| The AI running silent simulations | **Internal rollouts / counterfactual reasoning** | Evolving the world-state forward (or branching it) without emitting tokens, exploring possible futures and testing hypotheses before committing to an answer |
| Copy the grid and try a different scenario | **Clone-and-perturb / counterfactual rollout** | Forking the world-state, applying a perturbation to one copy, evolving both, and comparing outcomes under the same verifier — systematic "what if?" testing |
| A film strip of cause and effect | **Temporal integration / grounded temporality** | The trajectory W₀ → W_T as an explicit causal witness: each frame is a verifiable snapshot, and planning reduces to finding trajectories that satisfy constraints |
| Step-by-step ripples are cheap and fast | **Iterative local computation** | Replacing one expensive global inference step with many cheap local update steps, distributing computation across the grid |
| Train on small mazes, use on big ones | **Size generalization via translation invariance** | Because the NCA update rule is the same at every cell, the same learned rule applies to grids much larger than anything seen during training |
| Meanings drifting and breaking old rules | **Embedding manifold drift** | The risk that joint training shifts the semantic vector space so that spatial dynamics learned on old embeddings no longer work correctly |
| Knowing when to skip the sketchpad | **Invocation policy** | The meta-level learned behavior of deciding when spatial reasoning adds value, how large a grid to allocate, and how many evolution steps to run |
| Too much crammed into one square | **Compositionality within cells / multi-slot binding** | The challenge of representing multiple independent properties at a single grid location — solved partially by multi-slot cells, factored representations, or graph overlays |
| SAGE as the AI's full imagination system | **Semantic Automaton in Geometric Embedding-space (SAGE)** | The complete three-component architecture: language interface (translator) + geometric world-state (sketchpad) + world-evolution engine (thinking engine), operating as a closed loop |
