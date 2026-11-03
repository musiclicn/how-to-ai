Think of the AI as a **strong senior engineer on their first day**. They're smart and fast, but they know nothing about your codebase, your business, or why things are the way they are. You're writing a design ticket for them, not a script.

As a backend engineer, you already know the mental model: **specify the contract, not the implementation.** Give the preconditions, postconditions and invariants, and leave the method body to them. That's the right altitude.

**How to tell if your altitude is right:** the agent should be able to check on its own whether it's done.
- **Too high:** "Make the API faster." There's no clear finish line, so the agent guesses what "faster" means, picks something easy, and declares success.
- **Too low:** "Add a cache in UserService line 40 using a HashMap…" You've done the thinking yourself. When reality doesn't match your assumptions, the agent follows your steps anyway instead of adapting.
- **Right:** "p99 of `GET /users/{id}` is 800ms and needs to be under 200ms. Stale data up to 30s is acceptable. Don't add new infra dependencies." The goal is concrete enough to measure and open enough to solve.

**A structure that works well:**
1. **Goal and why.** What it's for, not just what to do. The reason lets the agent make sensible calls in cases you didn't think of.
2. **Definition of done.** Acceptance criteria it can check: tests pass, a metric is hit, a behavior is shown to work.
3. **Constraints and the reasons behind them.** "Don't change the public schema, because mobile clients pin to it" generalizes much better than a bare "don't."
4. **Context.** Point to the relevant files, past decisions, and things you already tried that failed. This is where you have the biggest edge over the agent.
5. **Latitude.** Say what it can decide on its own and when it must stop and ask, for example before migrations or anything irreversible.

**Practical tips:**
- **Split the task** if it needs two or more separate "done" checks. One ticket should have one finish line.
- **Write out the edge cases you care about.** The model is good at the obvious path and weak at unstated assumptions.
- **Ask for a plan first on big tasks.** Reviewing a plan is the cheapest way to catch it working at the wrong altitude before it writes code.
- **The "new hire" test:** could a competent engineer who's new to the repo start without asking you anything, and know when to stop? If so, the prompt is good.

In short, describe the problem and how success will be judged, and let the agent work out the solution.
