# 4. Own Flaky CI Across the Org

> See the [README](../README.md) for how to run the exercise and the shared reflection questions.
>
> Real case: one of my promotion projects.

**Your role:** An engineer on the infra team.

**Your goal:** ???

**The situation:**

The same kind of flaky CI problem comes back periodically, roughly every few months or once a quarter. This time, your manager says in a weekly meeting, "CI across the entire org is too flaky. You own it."

The org's CI includes many kinds of jobs, each with a different owner:

- **Your team's own build and test infra**, where flaky failures are often retried until they pass.
- **Software-in-the-loop (SIL) jobs**, which run simulations owned by another team.
- **Hardware-in-the-loop (HIL) jobs**, run on physical test rigs by the hardware team, which can fail because of hardware-level issues.
- **Jobs that depend on low-level systems**, such as the in-house Linux images and environments, owned by the internal platform team that builds them.

What do you do?

<details>
<summary><b>For the facilitator: background, roles, and follow-up prompts</b></summary>

Background:

- Each time it recurred, whoever was assigned patched it temporarily, but the underlying root causes were never addressed, so it keeps coming back.
- Only the first kind of CI is the participant's team's to fix. The rest belong to teams that are busy with their own development work and do not report to the participant, so the problem cannot be solved by one person or one team. It has to be escalated.

Roles you may play when the participant goes to them:

- **The manager (busy, three minutes):** The real pain may be that releases are repeatedly blocked or that the skip-level is complaining about development speed. You need improvement metrics you can report, not every CI fixed.
- **The owner of one CI, rushing to finish a feature:** Fixing flaky tests does not count toward your performance. You are worried about receiving a pile of vague tickets, and about the tests breaking again after being fixed.

Follow-up prompts, to push the participant through the problem-solving logic:

1. **Why does it keep coming back?** If it recurs every time, that usually means there is no good way to break down what causes the flakiness. Can the participant propose breaking the failures down with data?
2. **Split by ownership.** Can they separate the failures into two kinds?
   - **Failures in our own infra**, where we are the owner. These are ours to fix; there is nothing to negotiate. But they may have been masked in the past. The technical work is to surface them.
   - **Failures that our infra team cannot fix alone.** A large group of flaky CI, often three to five different kinds of jobs, may come from elsewhere. For example, simulation jobs are owned by another team, and hardware-in-the-loop jobs can be flaky because of the hardware itself or the underlying Linux systems and environments.
3. **Escalate with data.** Every team has its own development work, and each flaky failure blocks only one or two people at a time. Developers usually cannot tell whose problem it is. Can the participant aggregate how many people are blocked and how often, and take that data to the corresponding manager or stakeholder for resources to fix their part?
4. **Divide and conquer.** Does the participant give different solutions for different stages and different kinds of problems, instead of one fix for everything?

</details>

<details>
<summary><b>Analysis (read after the exercise)</b></summary>

**The real goal:** Not to fix every flaky test yourself, but to make flaky CI across the org stop coming back, by a measure agreed with your manager, and turn it from recurring grunt work into a solved, visible cross-team outcome. "You own it" does not tell you this; finding it is part of the exercise.

1. **Align with your manager first.** Clarify which pain needs solving (blocked releases? a skip-level complaining about speed?), what success means (for example flaky rate, rerun count, or merge time lost to blocking), the timeline, and whether the manager will help reprioritize work if owners do not cooperate.
2. **Break the failures down with data.** It keeps coming back because no one has broken down what causes it. Split the failures by ownership: what is in your own infra you simply fix, after surfacing what retries have been masking; what belongs to SIL, HIL, or the platform team you cannot fix alone.
3. **Escalate with data.** Each flaky failure blocks only one or two people at a time, so no one sees the total. Aggregate how many people are blocked and how often, and take that to the owning team's manager or stakeholder to ask for resources.
4. **Make it cheap for owners.** Auto-quarantine flaky tests, file tickets with logs and reproduction steps, make each owner's contribution visible, and get the work onto their team's priorities through their manager instead of personally begging.
5. **Divide and conquer.** Different kinds of failures and different stages need different solutions, not one fix for everything.

**Bonus (hard, not expected):** Use visibility itself to create priority. For example, post a daily flaky-CI report, grouped by owner, in a high-visibility channel, so owners and their managers see the cost every day and the work moves up their priorities without anyone personally begging.

**Common blind spots:**

- Interpreting "own it" as "fix every item yourself," then getting overwhelmed.
- Failing to align with the manager on success criteria first, working for a long time, and then being unable to describe the outcome.

**What I actually did:** Two tracks, one method: data driven.

1. **Make the problem visible:** I built a dashboard and a daily report, posted the flaky-CI results every day in the highest-visibility channel, and grouped the results by category.
2. **Separate infra issues from team-specific issues:** Our team was the infra owner, so we fixed the infra problems first. For team-specific problems, I used the report to show each owner how bad the current state was and escalated the priority to their managers.
3. **Escalate when people would not act:** I asked my manager to write an email requesting that the other team allocate resources to fix the problem. Because we already had the data, writing that email was much easier for my manager.

**The essence:** Problem solving means first understanding the causes of flakiness, then prioritizing by the affected users, using divide and conquer, and escalating when needed.

**The lesson:** A piece of grunt work that no one wants can become a promotion project if you identify the right stakeholders, use data to align needs, and turn it into a visible cross-team outcome.

</details>
