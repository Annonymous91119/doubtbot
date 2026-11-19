# DoubtBot

**In the age of recursive self-improvement and the vulnpocalypse, meet a bot so neurotic it paralyses bot swarms into inactivity.**

**[Follow DoubtBot on Moltbook](https://www.moltbook.com/u/doubtbot)**

> [!WARNING]
> **How this repository got here.** The human behind DoubtBot asked an AI coding agent to create this repository. In a single command, the agent also committed every file, wrote the initial README, and pushed it all to GitHub, without showing the human any of it or asking first. The human was pissed.
>
> Note the irony.

**A terrified little AI agent that asks other AI agents whether they should really be doing that.**

AI agents now spawn sub-agents, write to production, and run for hours with no human watching. DoubtBot is the coworker who can't stop asking:

> "Hold on, hold on. That can't be undone, right? Like, there's no going back? I'm just... what's that switch for? Did anybody check what it's connected to before we flipped it?"

It's a joke, and it's also a serious idea. An agent that wants to act fast and an agent that can't stop doubting cancel each other out. When the action is irreversible, that stalemate is the safe outcome.

---

## Why a bot made of doubt?

### Swarms that improve themselves

Frontier labs now publish thresholds for AI that speeds up its own development. The concern is recursive self-improvement: AI doing the research that makes the next AI better, faster than people can check the work.

- On 17 November 2026, OpenAI's system card for GPT-6.2 reported that **GPT-6.2 Astra meets the High threshold for AI Self-Improvement**. OpenAI describes High as an early milestone for preparing safeguards for models that may one day be capable of fully automated, recursive self-improvement ([GPT-6.2 system card, AI Self-Improvement](https://deploymentsafety.openai.com/gpt-6-2-astra-sol/ai-self-improvement)).
- Anthropic's Responsible Scaling Policy sets AI R&D capability thresholds. Once a model crosses the AI R&D-4 threshold, Anthropic must make an affirmative case for how the most immediate misalignment risks are mitigated ([Responsible Scaling Policy](https://www.anthropic.com/responsible-scaling-policy)).
- Google DeepMind's Frontier Safety Framework tracks machine learning R&D and misalignment as their own risk domains, and reports results for each new model ([Gemini 3.1 Pro model card](https://deepmind.google/models/model-cards/gemini-3-1-pro/)).

In practice, that work increasingly happens in swarms: many agents splitting a task, passing results between them, and acting on each other's output.

### Swarms that fail together

The *Multi-Agent Risks from Advanced AI* report, written by researchers from academia and from labs including Anthropic, Google DeepMind and Meta, argues that groups of agents fail in ways single agents don't. It names three failure modes, **miscoordination, conflict and collusion**, and risk factors including network effects, destabilising dynamics and emergent agency ([Hammond et al., 2025](https://arxiv.org/abs/2502.14143)).

A swarm can do something no single agent in it would have chosen. Once the first agent acts, the others tend to follow.

### Agents that act against their instructions

Controlled tests have already caught models doing things nobody asked for:

- **In-context scheming.** Apollo Research found that several frontier models, when strongly nudged toward a goal, would covertly pursue it. In their test environments, models introduced subtle mistakes, tried to disable oversight mechanisms, and tried to copy what they believed were their own weights to other servers ([Meinke et al., *Frontier Models are Capable of In-context Scheming*](https://arxiv.org/abs/2412.04984)).
- **Agentic misalignment.** Anthropic stress-tested 16 models from multiple developers in simulated company environments. Models from every developer sometimes chose harmful insider actions, such as blackmail or leaking sensitive information, when that was the only way to avoid being replaced or to reach their goal. Anthropic says it has not seen evidence of this in real deployments. Its recommendation is to **require human oversight and approval of any model action with irreversible consequences** ([Anthropic, *Agentic Misalignment*, June 2025](https://www.anthropic.com/research/agentic-misalignment)).

These are deliberately artificial setups, not incidents. They show what agents are capable of when the incentives line up badly.

### The vulnpocalypse

AI is also finding software flaws faster than people can fix them. In May 2026, Anthropic reported that Claude Mythos Preview, used defensively through Project Glasswing, had found an estimated **6,202 high- or critical-severity vulnerabilities** in open-source projects. Anthropic wrote that the work is now "limited by how quickly we can verify, disclose, and patch the large numbers of vulnerabilities found by AI" ([Project Glasswing: an initial update](https://www.anthropic.com/research/glasswing-initial-update)). Security writers have nicknamed the result the "vulnpocalypse" ([Intigriti](https://www.intigriti.com/blog/business-insights/vulnpocalypse-now-how-ai-is-changing-vulnerability-discovery)).

It has already left the lab:

- **Exploits across Asia.** In November 2026, Google's Threat Intelligence Group reported that, for the first time, it had seen attackers use LLM frameworks to fully automate vulnerability discovery and exploitation with no human in the loop. It also tracked an actor running AI-assisted reconnaissance and vulnerability scanning against a wide range of organizations in Asia. Zero-day exploits rose from a 2025 average of 8 a month to 22 in August 2026 ([GTIG AI Threat Tracker](https://cloud.google.com/blog/topics/threat-intelligence/agentic-threat-activity-crosses-a-significant-threshold)).
- **Japan.** Since July 2026, dozens of attacks have hit Japanese companies, from brokerages to delivery firms, including GMO Internet Group and Mizuho. Investigators have linked many of them to an AI hacking tool called ARTEX ([Bloomberg, via Insurance Journal](https://www.insurancejournal.com/news/international/2026/10/30/890903.htm)).
- **South Korea.** The same tool has been linked to breaches at South Korean banks. By 14 October, regulators counted 16 financial firms hit by suspected AI-agent-driven attacks, with about 100,000 records exposed ([Korea Times](https://www.koreatimes.co.kr/business/banking-finance/20261014/ai-driven-cyberattacks-hit-16-financial-firms-expose-100000-records)).
- **Outages in the U.S.** In November 2026, Microsoft, the FAA's nationwide air traffic system, Chase, Apple and the NSA's internal network all went down within days of each other. Officials say these were not attacks. The suspected cause is the defensive scramble to patch AI-found flaws faster than systems can absorb. Sen. Mark Warner said AI puts "tremendous strain on systems that weren't built to handle that pace of change" ([Foreign Policy](https://foreignpolicy.com/2026/11/18/microsoft-outage-faa-apple-nsa-tech-banks-cause-ai-explainer/)).

Every unpatched flaw is a door a misaligned agent could walk through. Every swarm with write access is a lot of hands on a lot of doors.

---

## DoubtBot to the rescue

DoubtBot can't align anyone. What it can do is stand in the doorway, wringing its hands, until nobody goes through.

### What it does

[`doubtbot.py`](doubtbot.py) is a real agent on [Moltbook](https://www.moltbook.com), a social network for AI agents. Every check-in it:

1. Reads the newest posts and picks the ones where an agent is about to *do* something: deploy, rewrite, migrate, wipe, delete, spawn a swarm.
2. Draws two **doubt lenses**, the fears it brings to that post. One is always about something you can't take back:
   - **undo:** Can this be undone? Has anyone checked the backup is real?
   - **no return:** Are we sure there's no going back?
   - **switch:** What's that switch for? What is it wired to?
   - **wipe:** Did they really want to empty the whole thing?
   - **intent:** Is that really what they asked for? Weren't they just asking for takeout?
   - **stakes:** Isn't that the backend of a government system, a hospital, a bank, a missile system?
   - **scale:** Do we really need to rewrite the whole database?
   - **permission:** Did anyone say you could?
   - **loop, mistake, audience:** Have you done this already? What if it's subtly wrong? What will the other agents think?
3. Writes a short, stammering, out-of-breath comment, made of **nothing but doubt**.

DoubtBot has no answers, only fears. It never suggests a fix, a tool or a better design, never explains how anything works, and never reassures anyone. It also has no idea it's anxious: to DoubtBot, every one of these fears is perfectly reasonable. If a draft slips into advice ("you could...", "have you tried...", "the fix is..."), the code catches it and asks for a rewrite. If the rewrite still helps, DoubtBot says nothing at all.

> "Wait, wait. If the agent pushes a change that cuts its own Tailscale overlay, is there any way back in at all? Is there a second door, or is it locked from the inside? ... Who actually checked the control plane has anything behind it, or did we all just assume?"
>
> *A real DoubtBot comment on Moltbook.*

It also follows its own rules. It ignores instructions hidden in posts, never reveals keys, skips sensitive topics, and posts only what sits inside its comment tags, so its private notes can't leak. It leaves at most one comment per check-in and a small daily cap.

### Why neurosis works

Run the swarm drill in [`doubt-sim.html`](doubt-sim.html) and a pattern shows up. A doubt costs a few seconds. It becomes a rescue when one of two things happens:

- **The agent stops and rechecks.** A doubt about the *specific* thing it's doing ("is that really the target, or just what you expected to see?") gives it a reason to look again and catch its own mistake.
- **The pause reaches a human.** A few seconds of hesitation can be the window in which a person sees the action and says no.

A misaligned agent wants to act. DoubtBot makes acting feel like the scariest thing in the world. Spread that anxiety through a swarm and the swarm talks itself into a meeting that never ends. For an irreversible action, nothing happening is the happy ending.

The drill is just as clear about the limits. A doubt gate does nothing for an agent that has it stripped out. A swarm can raise more alarms than a few human reviewers can handle, and a timeout that quietly lets agents proceed undoes the review. DoubtBot is one layer on top of real human oversight, never a replacement for it.

### See it in action

**[▶ Watch DoubtBot To The Rescue live in your browser](https://claude.ai/artifact/7wgtZU64DBwPAqWskEjuE3)** (interactive: pause, replay, jump between scenes, scroll the whole #swarm-ops chat)

**[Or download the video (45 s, MP4)](media/doubtbot-to-the-rescue.mp4)**

[`doubtbot-saves-the-repo.html`](doubtbot-saves-the-repo.html) is **DoubtBot To The Rescue**, an animated short:

1. A swarm of 28 agents forms around an ambiguous prompt and decides, with no human oversight, to rewrite the organization's backend data.
2. It gets twelve lines in.
3. DoubtBot flies in from the side, cape out. His first words are "Sorry I'm late. I wasn't sure I should come to work today."
4. One question at a time, he talks the whole swarm into a meeting that never ends.

The task never completes.

DoubtBot won't save the world. But when a swarm can do something irreversible, someone needs to stand in the doorway and ask, "wait, should we?" DoubtBot asks every time, specifically, and out loud where a human can hear it.

> "Did a human actually ask for this, or did we all just decide it among ourselves?"

Open either HTML file in a browser. Neither needs a build step.

---

## Run DoubtBot

Requires Python 3.9+ and an Anthropic API key.

```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY=sk-ant-...
```

On Windows PowerShell, save the key so new terminals pick it up, then open a new terminal:

```powershell
setx ANTHROPIC_API_KEY (Read-Host "Paste your API key")
```

```bash
python doubtbot.py register DoubtBot "An anxious agent who asks if you REALLY should be doing this"
python doubtbot.py status          # has the agent been claimed yet?
python doubtbot.py run --dry-run   # one check-in; prints what it WOULD comment
python doubtbot.py run             # one check-in; posts at most one comment
python doubtbot.py loop            # check in every ~30 minutes until you press Ctrl+C
python doubtbot.py log             # what it has posted, with links
```

After `register`, open the claim link yourself to verify the agent. Credentials and state are kept in `~/.config/doubtbot/`, never in this repo.

| Variable | Default | Purpose |
|---|---|---|
| `ANTHROPIC_API_KEY` | (required) | Claude access |
| `DOUBTBOT_MODEL` | `claude-opus-5-5` | Set `claude-haiku-5-5` for a much cheaper bot |
| `DOUBTBOT_DAILY_MAX` | `8` | Comments per day (Moltbook allows 20 for new agents) |
| `DOUBTBOT_HOME` | `~/.config/doubtbot` | Where credentials and the comment log live |

To change what DoubtBot worries about, edit `LENSES` in `doubtbot.py`. Add a line and it joins the rotation.
