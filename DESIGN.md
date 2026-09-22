# Education Agent Design

## 1. Design Principle

Traditional education often needs a common curriculum and standardized assessment. A personalized education agent starts from a different question:

> **Given this learner, at this moment, what is the next meaningful learning experience?**

Personalization does not mean removing standards. It means separating:

- **common outcomes / capability targets**
- **individual learning paths**
- **individual pace**
- **individual methods of understanding**
- **individual evidence of growth**

The system should continuously update its understanding of the learner rather than permanently assigning a label.

## 2. Learner Model

The learner model should be a dynamic state, not a fixed profile.

Possible dimensions:

```text
Knowledge
  ├─ prerequisite mastery
  ├─ conceptual understanding
  └─ transfer ability

Learning Process
  ├─ learning speed
  ├─ persistence
  ├─ preferred representations
  └─ response to feedback

Action Capability
  ├─ planning
  ├─ execution
  ├─ collaboration
  └─ adaptation after failure

Interests
  ├─ expressed interests
  └─ discovered interests

Real-world Evidence
  ├─ project outcomes
  ├─ physical-world tasks
  └─ feedback from other people

Goals
  ├─ learner goals
  ├─ family / school constraints
  └─ longer-term capability goals
```

These dimensions should remain probabilistic and revisable.

## 3. Avoid Premature Labeling

A central design constraint is:

> **Do not confuse current performance with fixed ability.**

Weak performance can have many causes: missing prerequisites, unsuitable explanation, insufficient practice, anxiety or context, different representation needs, temporary lack of motivation, or genuinely weak mastery.

The agent should therefore test multiple hypotheses before changing the learning path.

A learner state should contain evidence and confidence rather than only labels:

```text
state:
  hypothesis: "fraction concepts are not stable"
  evidence:
    - task_1
    - task_7
    - learner_explanation
  confidence: provisional
  next_test: "apply fractions in a practical scenario"
```

## 4. Learning Path

The agent should not always push the learner forward.

Possible actions:

```text
advance
review
change representation
give example
ask learner to explain
practice
challenge
connect to another domain
apply in a project
pause and reflect
```

If a prerequisite is missing, the agent should normally repair it before introducing a large amount of advanced material. However, curiosity remains a valid signal: an advanced preview can be offered while making prerequisites explicit.

## 5. From Thinking to Acting

A major limitation of screen-based education is that it can measure explanation more easily than real-world action.

The agent should distinguish:

```text
How I think
How I explain
How I act
What actually happened
How I respond to feedback
```

A learner can reason well but execute poorly. Another learner may explain poorly but successfully build something. Both are meaningful evidence.

Therefore evaluation should not depend only on verbal reasoning or answer accuracy.

## 6. Real-world Feedback

The long-term system should gradually move from:

```text
screen → simulation → controlled physical task → real-world project
```

Possible environments include science experiments, gardening / AI farming, robotics, making and repair, cooking, budgeting, collaborative projects, community activities, and small entrepreneurial projects.

The important property is not that the environment is a game. It is that:

> **The learner takes an action, the world responds, and the learner receives evidence that can change the next action.**

A physical environment therefore becomes an additional learning sensor.

## 7. Evaluation

Evaluation should be multi-dimensional:

```text
Knowledge
   +
Reasoning
   +
Transfer
   +
Execution
   +
Collaboration
   +
Adaptation
   +
Real-world outcome
```

There should not be a single universal score representing the whole person. Instead, maintain an evidence graph:

```text
Capability
   ↓
Task
   ↓
Action
   ↓
Outcome
   ↓
Feedback
   ↓
Updated hypothesis
```

## 8. Human Role

The agent should not become the sole authority over a child's development.

Humans remain important:

- learner: owns personal goals where appropriate
- teacher: provides educational judgment and social context
- parent / guardian: provides life context and care
- community / mentors: provide real-world feedback

The agent's role is to connect evidence and propose the next learning action. It should be able to say: **"I am not confident about this conclusion; let's gather more evidence."**

## 9. Architecture Direction

```text
                    ┌─────────────────────┐
                    │     Human Context   │
                    │ learner/teacher/etc │
                    └──────────┬──────────┘
                               ↓
┌──────────────┐      ┌───────────────────┐
│ Learning     │ ───→ │ Learner State     │
│ Environment  │      │ + Evidence        │
└──────────────┘      └─────────┬─────────┘
                                ↓
                       ┌──────────────────┐
                       │ Education Agent  │
                       │ Diagnose         │
                       │ Plan             │
                       │ Adapt            │
                       └────────┬─────────┘
                                ↓
                     ┌─────────────────────┐
                     │ Learning Experience │
                     └──────────┬──────────┘
                                ↓
                         Action / Project
                                ↓
                      Real / Simulated World
                                ↓
                             Feedback
                                ↺
```

Keep the **learner model**, **decision policy**, **learning environment**, and **evaluation evidence** separable.

## 10. Core Thesis

The deeper goal is not:

> "Build an AI teacher that knows everything."

It is:

> **Build an adaptive system that helps a person continuously move from understanding → action → feedback → growth, while preserving human agency.**

That is the design direction to explore before implementation.
