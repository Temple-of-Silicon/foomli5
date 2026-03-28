# Superbase: Maze Training (ELI5)

## The Big Idea: The AI Is Not a Student, It's a Sculptor

Imagine you're not teaching a kid new facts — you're helping a block of clay discover what shape it already wants to be. That's what Superbase training is about.

Most people think training an AI is like pouring water into a bucket: you fill it up with examples until it knows things. **That's wrong.** The better picture is that the AI is a *mathematical machine* that already has hidden structure inside it — and training is the process of *finding and carving out* that structure, not stuffing new stuff in.

The AI isn't learning *from* the data. The data is a **massage tool** pressing on the AI's weights until the right shape emerges.

---

## Cronkle Bisection Descent (CBD): Choosing Your Valley Before You Fall Into One

Imagine a giant mountain range, and you're a marble. If you just start rolling, you'll tumble into whatever valley is nearest — and you might be stuck there forever. **CBD is the art of looking at the whole map before you roll.**

### The Valley Problem

The loss landscape (the "map" of how wrong the AI is) is full of valleys — places where the AI's answers are pretty good. But some valleys are amazing and some are mediocre. Normal training (gradient descent) just rolls downhill and *hopes* for the best.

CBD says: **don't roll yet. First, find out where the valleys are.**

### The Bisection Trick

Here's the clever move. Imagine you have two points on the map:
- Point A rolls into **Valley 1**
- Point B rolls into **Valley 2**

Somewhere between A and B, there's an invisible **fence** — the boundary between the two valleys. CBD finds that fence by doing what you do when guessing a number between 1 and 100: **always guess the middle**.

- Try the midpoint. Which valley does *it* roll into?
- Keep the half that straddles the fence.
- Repeat until you've found the fence almost exactly.

This is called **edge tracking** — sitting right on the ridge between valleys so you can *choose* which one to drop into, on purpose, instead of by accident.

### Why This Matters (The Miracle Case)

Without CBD, escaping a bad valley can take an astronomically long time — like waiting for a marble to randomly vibrate out of a bowl. With CBD, you just **walk to the door** between valleys. That's not a small improvement. In the worst cases, it's the difference between "might never happen" and "done in minutes."

**But watch out:** this magic only works when the valleys are really well-separated. If the whole low-loss region is one big connected swamp, CBD becomes just a fancy way to do what good learning-rate schedules already do.

---

## Coherence-Bound Induction (CBI): Learning New Tricks Without Forgetting Old Ones

CBD tells you *where* to go. CBI tells you *how to get there without breaking yourself along the way.*

### The Problem: Learning Is Dangerous

Every time the AI learns something new, it risks scrambling something it already knew. This is called **catastrophic forgetting** — and it's exactly as bad as it sounds. You teach the AI to write poetry, and suddenly it forgets how to do math.

CBI's answer: **only learn new things inside a safe corridor.**

### The Coherence Corridor

Picture a hallway. The AI is allowed to learn and change — but only while it stays inside the hallway. If it tries to learn something that would push it out of the hallway (i.e., breaks something it already knew), that update gets **thrown in the trash** and rolled back.

The hallway has **three walls**:

- **Regression Gate (R):** "Can you still do all the things you could do before?" If no → rollback.
- **Reconstruction Gate (T):** "Can you still replay and verify everything you committed to?" If no → rollback.
- **Coherence Probe (C):** "Are your skills still talking to each other, or are they becoming isolated strangers?" If fragmented → rollback.

Only if *all three* gates pass does the new learning get kept. No exceptions. No "we'll fix it later."

> "We will fix it later" is a euphemism for "we have no idea what changed."

---

## The Training Toolkit: Six Cool Operators

Once you have the corridor, you need tools for *carefully* injecting new knowledge. Here are the main ones:

### 1. Learned Sampling — The AI Chooses How to Think

Normally, an AI samples its next word with a fixed randomness setting (called **temperature**). Learned Sampling lets the AI *control its own temperature* based on what it's doing.

- Exploring a hard problem? **Crank up the randomness** to cast a wide net.
- Executing a known plan? **Lock it down tight.**

It's like giving a musician control over their own instrument dynamics instead of forcing them to play every note at the same volume.

### 2. Temperature Dynamics — Controlled Brain Explosions

Every so often during training, **spike the temperature** — turn up the randomness sharply, then cool it back down. Think of it like shaking a snow globe, then watching the snow settle.

The AI learns to *recover gracefully* from the shake. Rollouts that land in a good place after the shake get rewarded. This teaches the AI to explore productively instead of just wandering.

### 3. Rollout Braiding — Weaving the Past Into the Present

Instead of treating every training episode as a fresh start, **braid** pieces of old episodes into new ones. It's like showing a student their own old homework at the beginning of each new assignment.

This prevents forgetting (the old stuff keeps showing up) and helps the AI integrate what it learned before into what it's learning now.

### 4. Non-Destructive Weight Editing (LoRA Tower) — Photoshop Layers for AI

The base AI model is like a precious original painting. You never touch it. Instead, you add **transparent adjustment layers** on top (called LoRA adapters) — like Photoshop layers.

Want to try something new? Add a layer. It doesn't work? **Delete just that layer** — the original painting is fine. You can stack layers into a *tower*, each one a reversible edit, and roll back to any earlier point in history.

You can even run a **swarm** of 128 tiny adapter experts, each specializing in something different, with a router deciding which expert handles each job.

### 5. Internal State Rewards — Teaching the AI to Feel Its Own Brain

Standard training rewards the AI for *what it outputs*. Internal state rewards also reward it for *what happens inside* while it's thinking.

If the AI's hidden states show signs of rich, diverse reasoning (high "hidden-state variance"), it gets a bonus. This is like **proprioception** — the sense that tells you where your own body is. The AI develops a sense of its own cognitive health.

Warning: the AI can learn to fake the internal signal without actually thinking better. The corridor catches this.

### 6. Ascension Maze — A Puzzle Generator That Knows Your Weaknesses

A generator AI builds **nested puzzle chains** — like Matryoshka dolls where each doll's key requires skills from solving the previous doll. The generator is *adversarial*: it watches the solver AI and designs puzzles that specifically target its blind spots.

It's a **GAN for cognition**: the puzzler gets smarter at finding gaps, the solver gets smarter at filling them, and the frontier of what the AI can do keeps advancing.

---

## The Complexity Rent: MDL Pressure

Every fact the AI learns costs something — it takes up space in the AI's "compression budget." This is called **MDL pressure** (Minimum Description Length). The AI is always under pressure to describe the world using the *fewest, most reusable rules possible*.

Think of it like rent. Every complex special case the AI memorizes **costs rent**. Elegant, general principles are **cheap**. MDL pressure is the landlord that forces the AI to find cleaner, simpler explanations — which is exactly what makes it good at new problems it's never seen.

---

## The Platonic Kernel: What the AI Is Really Finding

Here's the deepest idea in the whole chapter.

When gradient descent trains a neural network, it might be discovering actual **mathematical structures** — geometric shapes, algebraic symmetries, invariants — that exist in abstract math-space *before* it gets around to fitting the specific dataset.

The dataset is just **pressure** that steers the search. The real prize is the mathematical object underneath.

> *The data is the search signal. The structure is the find.*

The corridor keeps that discovered structure safe while new adapters and operators pile on top of it. The kernel is the precious thing. Everything else is a layer on top.

---

## Putting It All Together

| Concept | Simple version |
|---|---|
| **CBD** | Find the good valley before you fall into the bad one |
| **CBI / Coherence Corridor** | Only learn new things while your old knowledge stays safe |
| **Regression Gate** | "Can you still do everything you could before?" |
| **Reconstruction Gate** | "Can you still replay your old work exactly?" |
| **Coherence Probe** | "Are your skills still friends with each other?" |
| **Learned Sampling** | The AI controls its own randomness dynamically |
| **Temperature Dynamics** | Shake the snow globe; reward graceful recovery |
| **Rollout Braiding** | Weave old memories into new training |
| **LoRA Tower** | Photoshop layers — edit without destroying |
| **Ascension Maze** | An adversarial puzzle machine that targets your weaknesses |
| **MDL Pressure** | The rent that forces elegant, reusable knowledge |
| **Platonic Kernel** | The mathematical structure gradient descent actually discovers |

**The punchline:** The AI is a participant in its own training, not a passive student. It helps shape how it learns. The corridor makes sure it doesn't break itself in the process. And CBD makes sure it chooses a good place to end up before it's too late to change course.

---

## Now You Speak Fancy

You've been reading the fun version. Here's what to say at the grown-up table.

| ELI5 Version | Fancy Term | What It Really Means |
|---|---|---|
| Superbase Training | Superbase Training / Semiodynamic Training | Training where the model is an *active participant*, not a passive recipient — rollouts are "massaging passes" that refactor the model's perception, not lessons poured into a bucket |
| Massage tool pressing on clay | The data as probe / search signal | The dataset supplies optimization pressure to steer search through weight space; the model is discovering structure, not memorizing content |
| The map of how wrong the AI is | Loss landscape $L(\theta)$ | The high-dimensional surface mapping every possible set of weights to a score; valleys are "basins of attraction" |
| The good valley vs. the bad valley | Basin of attraction / local minimum | The region of weight space that gradient flow converges to from a given starting point; some are more useful than others |
| CBD — looking at the map before you roll | Cronkle Bisection Descent (CBD) | A basin-selection method that operates on the *boundary structure* of the loss landscape before committing to within-basin descent |
| The invisible fence between valleys | Basin boundary / separatrix | The set of points where an infinitesimal perturbation changes which attractor you converge to; the codimension-1 stratum is built from stable manifolds of index-1 saddles |
| Always guess the middle | Bisection primitive / edge tracking | Repeatedly evaluating the midpoint of a bracket straddling two different basins, halving the bracket each time, to localize the boundary to tolerance $\delta$ in $O(\log^2(1/\delta))$ cost |
| Sitting on the ridge to choose your valley | Edge state / committor surface $q(\theta) = \tfrac{1}{2}$ | The iso-committor surface — the locus of points with equal probability of reaching either basin — the stochastic generalization of the separatrix |
| "Wait for a marble to vibrate out of a bowl" | Kramers escape time / Eyring–Kramers law | Exponential barrier-crossing time $\sim \exp(\Delta/\varepsilon)$ for spontaneous SGD escape from a metastable basin; what CBD is designed to circumvent |
| MDL pressure / complexity rent | MDL pressure (Minimum Description Length) | A regularization force that penalizes description complexity, biasing the model toward the fewest, most reusable rules; expensive special cases get charged "rent" |
| The coherence corridor / safe hallway | Coherence corridor $\mathcal{K} = \mathcal{S}_R \cap \mathcal{S}_T \cap \mathcal{S}_C$ | The intersection of the regression surface, reconstruction region, and coherence region — the set of weight states where all three gates pass simultaneously |
| CBI — learning without breaking yourself | Coherence-Bound Induction (CBI) | The training discipline of injecting novelty only inside the coherence corridor; every update is proposed on a candidate branch, verified against all three gates, and either committed or rolled back |
| Regression Gate ("can you still do everything?") | Regression gate $R(\theta)$ | A held-out capability suite that must continue to pass; failure indicates catastrophic forgetting; defines the regression surface $\mathcal{S}_R$ |
| Reconstruction Gate ("can you replay your old work?") | Reconstruction gate $T(\theta)$ | Requires that previously verified commitments (proofs, tool traces, IR traces) still replay correctly through the verifier stack; defines the reconstruction region $\mathcal{S}_T$ |
| Coherence Probe ("are your skills still friends?") | Coherence probe $C(\theta)$ | Detects internal representation fragmentation — skill partitioning, loss of cross-skill composition — via CKA/SVCCA similarity, A∧B composition tests, and activation banding; defines the coherence region $\mathcal{S}_C$ |
| CBI operators | CBI operators | Any training mechanism (exploration, accumulation, or curriculum) that expands capability while keeping every checkpoint inside the corridor |
| AI controls its own randomness | Learned Sampling | Sampling parameters (temperature, top-p, top-k) become a learned RL policy conditioned on the model's hidden state, enabling state-dependent exploration dynamics that transfer across domains |
| Temperature dynamics / shaking the snow globe | Temperature Dynamics / scheduled temperature spiking | Injecting brief high-entropy perturbations into rollouts ("spike, cool, select"), then applying selection pressure to rollouts that recover coherence — Mesaton's varentropy-guided perturbation applied to training |
| Rollout Braiding / weaving old homework into new | Rollout Braiding | Prefixing or injecting fragments of prior rollouts into new training episodes; the braid topology ranges from simple N+1 injection to a learned permutation matrix over a provenance-logged episode registry |
| LoRA Tower / Photoshop layers | Non-Destructive Weight Editing / LoRA tower | Freezing the base model and stacking LoRA adapters as reversible "adjustment layers"; the tower supports bisection over edit history and smooth rollback to any prior checkpoint |
| LoRA swarm of 128 experts | LoRA swarm | An ensemble of many adapters (e.g., 128) with a learned gating/router mechanism routing different computations through different orthogonal edit directions |
| Internal State Rewards / AI feels its own brain | Internal State Rewards / hidden-state proprioception | Reward terms for internal dynamics (hidden-state variance, attention entropy, SAE feature activations) that teach the model to self-condition — inducing rewarded internal states via learned linguistic moves |
| Ascension Maze / adversarial puzzle machine | Ascension Maze | A generator–solver adversarial curriculum where the generator builds Matryoshka capsule chains targeting the solver's weaknesses; a GAN for cognition whose difficulty scales combinatorially with capability composition depth |
| Curriculum as compression schedule | Curriculum as Compression Schedule | Clustering training data by SAE-learned capability motifs and treating the time-varying mixture weights as a control surface — "the proportion IS the training signal" |
| The Platonic Kernel / mathematical structure gradient descent discovers | Platonic Kernel principle | The hypothesis that backprop discovers reusable mathematical structures (geometric invariants, algebraic symmetries) *before* fitting the dataset; the dataset is a probe steering search, not the thing being modeled |
| Kernel regime / keeping your options open | Kernel regime | The training phase where weights are still a configurable general-purpose apparatus with high optionality, not yet committed to a specific domain; Superbase training tries to stay here as long as possible |
| The thing inside that must be kept safe | Mask–kernel delta | The gap between what the kernel can do and what the corridor's behavioral surface expresses; the shoggoth meme, formalized |
| VM Embedding / the AI has a body | VM Embedding | Training the model as a first-class component inside a deterministic sandbox (Python VM/OS), where observation and intervention are direct and the replay log gives reconstruction for free |
| "We'll fix it later" | Untracked weight drift / silent corridor exit | What happens when a corridor violation is not caught at the checkpoint where it occurred; by the time symptoms appear, the causal update is buried and attribution is archaeology |
