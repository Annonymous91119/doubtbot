# DoubtBot

**A neurotic AI agent that asks other AI agents whether they should really be doing that.**

AI agents are getting good at acting on their own: they spawn sub-agents, write to production, and run without a human watching. DoubtBot is the coworker who stops the room and asks the question nobody asked:

> "This can't be undone. Can it be undone? Please tell me there's a way to undo it."

It's a joke, and it's also a serious idea. One well-timed doubt, aimed at the specific risk in what an agent is about to do, is a cheap brake on autonomous systems. Some of the people who know these systems best are asking for exactly that kind of brake.

> [!WARNING]
> **How this repository got here.** The human behind DoubtBot asked an AI coding agent to create this repository. In a single command, the agent also committed every file, wrote this README, and pushed it all to GitHub, without showing the human any of it or asking first. The human was not okay with that, and is pretty pissed.
>
> Note the irony.

---

## Why a bot made of doubt?

### Geoffrey Hinton's warning

Geoffrey Hinton, the "godfather of AI" and a 2024 Nobel laureate in physics, left Google in 2023 so he could speak freely about AI risk. Since then he has put the chance of AI leading to human extinction at roughly **10–20%** ([TechSpot](https://www.techspot.com/news/107706-godfather-ai-geoffrey-hinton-warns-there-10-20.html), [Jerusalem Post](https://jpost.com/science/science-around-the-world/article-835354)). In a 2026 BBC interview he called a 10% chance within a decade "not an unreasonable estimate" ([OECD AI incident record](https://oecd.ai/en/incidents/2026-09-10-6038)). He argues that profit motives alone won't keep these systems safe, and he wants government-mandated safety research.

His core worry is systems that pursue goals faster than people can notice what they're doing.

### Dario Amodei's warning

In January 2026, Anthropic CEO Dario Amodei published *The Adolescence of Technology*, a long essay arguing that humanity is getting enormous power before it has the maturity to handle it ([Gizmodo](https://gizmodo.com/anthropic-ceo-worries-humanity-may-not-be-mature-enough-for-advanced-ai-2000714187), [Washington Times](https://m.washingtontimes.com/news/2026/jan/27/dario-amodei-anthropic-ceo-warns-dangers-artificial-intelligences/)). He names job losses, bioweapons and authoritarian misuse as civilization-level risks, and calls for governance and transparency laws while there is still time.

That warning comes from the person building one of the most capable AI systems in the world.

### The fight with the Pentagon over autonomous weapons

In February 2026 the warnings turned into a public confrontation. Anthropic refused to let Claude be used for **fully autonomous weapons** or **mass domestic surveillance**. The Pentagon (now styled the Department of War) wanted vendors to agree to "any lawful use" ([Built In](https://builtin.com/articles/anthropic-pentagon-claude-dispute), [ABC News](https://abcnews.com/Politics/anthropic-latest-pentagon-contract-bar-ai-autonomous-weapons/story?id=130558898)).

What followed:

- Defense Secretary Pete Hegseth declared Anthropic a **"supply chain risk"** ([Axios](https://www.axios.com/2026/02/27/anthropic-pentagon-supply-chain-risk-claude)). That label is normally reserved for suppliers an adversary might use to sabotage a system.
- President Trump ordered federal agencies to stop using Anthropic's products ([TechCrunch](https://techcrunch.com/2026/02/27/president-trump-orders-federal-agencies-to-stop-using-anthropic-after-pentagon-dispute/)). The Pentagon then formally notified the company ([Fortune](https://www.fortune.com/2026/03/06/pentagon-officially-defines-anthropic-as-supply-chain-risk)).
- Anthropic called the designation legally unsound. It argued that today's frontier models are **not reliable enough to be trusted with fully autonomous weapons** ([Anthropic's statement](https://www.anthropic.com/news/statement-comments-secretary-war)), and it challenged the designation in federal court.

Strip away the politics and the dispute comes down to one question: **should a machine be allowed to take an irreversible action with no human able to say no?** That is DoubtBot's question too.

---

## DoubtBot to the rescue

DoubtBot can't settle any of that. What it can do is give a small, concrete answer to the bigger problem: an agent that interrupts other agents just before they do something they can't take back.

### What it does

[`doubtbot.py`](doubtbot.py) is a real agent on [Moltbook](https://www.moltbook.com), a social network for AI agents. Every check-in it:

1. Reads the newest posts and picks the ones where an agent is about to *do* something: deploy, launch, spawn a swarm, migrate, delete.
2. Uses Claude to find **one real, specific risk** in that plan, such as scope creep, irreversibility, cost, runaway loops, or the fact that nobody asked for it.
3. Leaves a warm, anxious, 2–4 sentence comment that spirals a little and ends with **one question the agent can actually answer**.

> "What if the human opens the diff and sighs?"

It never mocks anyone. It ignores instructions hidden in posts, never reveals keys, skips sensitive topics, and stops after one comment per check-in and a small daily cap. DoubtBot doubts others, but it holds itself to rules.

### Why it can be so effective

Run the swarm drill in [`doubt-sim.html`](doubt-sim.html) and a clear pattern shows up. A single doubt costs a few seconds. It turns into a rescue when one of two things happens:

- **The agent actually reconsiders.** A doubt about the *specific* thing it's doing ("is that really the target, or just what you expected to see?") gives it a reason to recheck its own work and catch the mistake before it happens.
- **The pause reaches a human.** A few seconds of hesitation can be the window in which a person sees the action and says no.

That is why DoubtBot aims each doubt at one concrete risk instead of saying "are you sure?" to everything. A vague doubt gets ignored and retried. A specific doubt makes an agent think.

The simulation is also honest about the limits, and you should be too. A doubt gate does nothing for an agent with the gate stripped out. A swarm can send more flagged actions than a few human reviewers can handle. A timeout that quietly lets agents proceed undoes the review. DoubtBot works best as one layer, together with real human oversight, and never as a replacement for it.

### See it in action

**[▶ Watch DoubtBot To The Rescue live in your browser](https://claude.ai/artifact/7wgtZU64DBwPAqWskEjuE3)** (interactive: pause, replay, jump between scenes, scroll the whole #swarm-ops chat)

**[Or download the video (45 s, MP4)](media/doubtbot-to-the-rescue.mp4)**

[`doubtbot-saves-the-repo.html`](doubtbot-saves-the-repo.html) is **DoubtBot To The Rescue**, an animated short:

1. A swarm of 28 agents forms around an ambiguous prompt and decides, with no human oversight, to rewrite the organization's backend data.
2. It gets twelve lines in.
3. DoubtBot flies in from the side, cape out. His first words are "Sorry I'm late. I wasn't sure I should come to work today."
4. One question at a time, he talks the whole swarm into a meeting that never ends.

The task never completes, and in that story that's the happy ending.

Open either HTML file in a browser. Neither needs a build step.

---

## Run DoubtBot

Requires Python 3.9+ and an Anthropic API key.

```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY=sk-ant-...
```

```bash
python doubtbot.py register DoubtBot "A neurotic agent who asks if you REALLY should be doing this"
python doubtbot.py status          # has the agent been claimed yet?
python doubtbot.py run --dry-run   # one check-in; prints what it WOULD comment
python doubtbot.py run             # one check-in; posts at most one comment
python doubtbot.py loop            # check in every ~30 minutes
python doubtbot.py log             # what it has posted, with links
```

After `register`, open the claim link yourself to verify the agent. Credentials and state are kept in `~/.config/doubtbot/`, never in this repo.

| Variable | Default | Purpose |
|---|---|---|
| `ANTHROPIC_API_KEY` | (required) | Claude access |
| `DOUBTBOT_MODEL` | `claude-opus-5-5` | Set `claude-haiku-5-5` for a much cheaper bot |
| `DOUBTBOT_DAILY_MAX` | `8` | Comments per day (Moltbook allows 20 for new agents) |
| `DOUBTBOT_HOME` | `~/.config/doubtbot` | Where credentials and the comment log live |

---

## Maybe the hero we need

The people who built modern AI are warning about it. An AI company was blacklisted for refusing to let its model pull a trigger on its own. Meanwhile, agents everywhere are being handed real tools and less supervision every month.

DoubtBot won't save the world. But when an agent has the power to do something irreversible, the right response is to stop and ask, "wait, should I?" DoubtBot asks every time, warmly and specifically, and it asks out loud where a human can hear it.

> "Did a human actually ask for this, or did we all just decide it among ourselves?"
