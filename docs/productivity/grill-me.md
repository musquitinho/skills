## What it does

`grill-me` takes a **loose idea** and interviews you until you can commit to it. You do not need a worked-out plan to start, because the [session](https://www.aihero.dev/ai-coding-dictionary/session) exists to produce one. It asks in **rounds**. Each round is the whole **frontier**, which is every question whose prerequisites you have already settled. So it never asks you something that depends on an answer it hasn't heard yet.

It is **[stateless](https://www.aihero.dev/ai-coding-dictionary/stateless)**. It writes no files and leaves no workspace behind. The only result is a clearer version of the idea, in your own head.

## When to reach for it

You invoke this by typing `/grill-me`; the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) won't reach for it on its own. Start it in a **fresh conversation**, not on top of a plan you already had an agent write.

Reach for it as soon as you have an idea worth taking seriously (a feature, a product direction, a business call, a piece of writing), and long before you have worked out what it involves. Vagueness is not a reason to wait, because the session exists to remove it. If you can already specify the thing precisely, you don't need to grill it.

Which of the three [grilling](https://www.aihero.dev/ai-coding-dictionary/grilling) [skills](https://www.aihero.dev/ai-coding-dictionary/skill) you want depends on what is in front of you:

- **Anything, anywhere.** Use `grill-me`. It needs no repo and writes no files, and the subject doesn't have to be code.
- **A codebase to align against.** Use [grill-with-docs](https://aihero.dev/skills-grill-with-docs). It is the same interview, but [stateful](https://www.aihero.dev/ai-coding-dictionary/stateful): it reads your code and keeps what it learns in `GLOSSARY.md` and ADRs.
- **Too big for one session.** Use [wayfinder](https://aihero.dev/skills-wayfinder). It charts the effort as a map and runs grilling sessions inside it.

Leave [plan mode](https://www.aihero.dev/ai-coding-dictionary/agent-mode) off. Plan mode makes the agent hurry to produce a plan, when you want it to keep asking questions.

## It's a conversation, not an interview

The skill asks the questions, but **you** own the scope. People often miss this. It is the difference between a session that turns an idea into decisions and one that produces confident nonsense.

The failure mode is **passivity**: answering "agreed, agreed, agreed" for forty questions and coming out with a plan the agent wrote and you nodded at. It feels productive because it was long. But you decided nothing, and the result looks more certain than it is.

Being active means steering. Push back on a question that is less detailed than you need. Say when the scope is drifting. Answer "I don't know" and mean it. This skill helps an engineer and does not replace one. The quality of the result depends on the quality of your answers, not on the number of questions.

The opposite error is real but rarer: staying in the interview so long you never reach code.

## Grillable and ungrillable

Some questions can be answered by talking. Others can't, and no amount of grilling will get you there.

"One long form or three pages?" and "how should this interaction feel?" are **ungrillable**. You need something to react to before you can answer them. When you hit one, stop grilling. Build the throwaway version with [prototype](https://aihero.dev/skills-prototype), look at it, then come back and answer in one line.

Sessions grow too long when you try to talk through an ungrillable question. The agent keeps rephrasing, you keep guessing, and the scope grows with the uncertainty.

## Common questions

**How many questions should I expect, and how do I know when it ends?**
Count rounds, not questions. Forty-six questions across four rounds is an ordinary session. It ends when the frontier is empty: it has visited every branch, and nothing is left as an unstated assumption.

**It asked me two hundred questions. What went wrong?**
Usually the scope was too large. Ask the agent to break the work into smaller pieces first, then grill each one. Very long sessions also drift into the **[dumb zone](https://www.aihero.dev/ai-coding-dictionary/smart-zone)**, where the [context window](https://www.aihero.dev/ai-coding-dictionary/context-window) is full enough that the questions get worse.

**Can I go back to one question at a time?**
Yes. Add this to your global `CLAUDE.md`:

```
When grilling, ask one question at a time.
```

**I installed `grill-me` on its own, and it says `grilling` doesn't exist.**
That is expected, and it is one of the most-filed problems with this skill ([#685](https://github.com/mattpocock/skills/issues/685), [#1319](https://github.com/mattpocock/skills/issues/1319)). The whole body of `grill-me` is one instruction to load [grilling](https://aihero.dev/skills-grilling), so it does nothing without it, and the installer does not pull it in for you. Install `grilling` as well, or the whole set. Some agents carry on anyway and improvise an interview. You can tell it isn't this one, because the questions arrive without rounds or recommended answers.

**It says `grill-me` "cannot be used with Skill tool due to disable-model-invocation".**
This is a [harness](https://www.aihero.dev/ai-coding-dictionary/harness) interaction, reported in Claude Code and still open ([#1052](https://github.com/mattpocock/skills/issues/1052), [#1056](https://github.com/mattpocock/skills/issues/1056)). The setting that stops the agent from firing `grill-me` on its own also stops the agent from calling it after you have typed it. The skill only needs `grilling`, which the agent is allowed to call, so tell it to call the Skill tool with `grilling` directly.

**It ran out of questions and started building.**
It should stop and wait for you to confirm that you share an understanding, but weaker or faster [models](https://www.aihero.dev/ai-coding-dictionary/model) skip that step, and some collapse the interview into a question or two and an outline ([#240](https://github.com/mattpocock/skills/issues/240), [#729](https://github.com/mattpocock/skills/issues/729)). The reliable fix is a line in your own `AGENTS.md` or `CLAUDE.md` telling the agent not to implement without your permission.

**What if I genuinely don't know the answer?**
Say so. "I don't know" is a real answer, and a question you can't answer is usually a sign to prototype rather than to guess.

**Do I start a fresh session before writing the [spec](https://www.aihero.dev/ai-coding-dictionary/spec)?**
No. The value of the session is the [context](https://www.aihero.dev/ai-coding-dictionary/context) you just built. Hand the same conversation straight to [to-spec](https://aihero.dev/skills-to-spec).

**Does the model matter?**
More than for most skills. Grilling depends on the model's own knowledge of how systems break, so use your best one. Implementation mostly follows context, so a cheaper model is fine there.

## It's working if

- You disagree with something. A session with no pushback from you is a session you didn't need.
- Questions arrive in a few rounds, not one at a time for a long time, and later rounds clearly build on what you said earlier.
- You end up somewhere you didn't expect, because a question showed you a decision you had been making without noticing.
- At the end you could defend each choice to someone who wasn't there.

## Where it fits

`grill-me` is a **standalone you can run anywhere, on anything**. Because it is stateless, it is portable. It needs no repo, workspace, or setup, and does not assume the idea is about software. People use it for business decisions, for writing, and for what to do next: anything they cannot think through clearly on their own.

Portability is the only difference from [grill-with-docs](https://aihero.dev/skills-grill-with-docs). That skill runs the same interview, but reads a codebase to align against and records what it learns as `GLOSSARY.md` and ADRs. Both use the [grilling](https://aihero.dev/skills-grilling) skill underneath. `grill-me` is the user-invoked entry point that keeps no state.

If what you grilled does turn out to be software, you can hand the same conversation to [to-spec](https://aihero.dev/skills-to-spec) and carry on into the build flow (an option, not the point of the skill). When you're unsure which flow fits, [ask-matt](https://aihero.dev/skills-ask-matt) routes you.
