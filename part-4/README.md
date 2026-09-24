# Part 4 — Disagreement & Team Leadership

A note on terms: this answer explains each technical term the first time it is used. The wording is kept simple on purpose. The reasoning is not simplified — only the words are.

A note on what is real: sections 2 and 3 are things that happened. Sections 1 and 4 are how I would act, and I say so rather than dress them up as memories. My role was different in each story, and that changes what my options were. In section 2 I was a senior individual contributor with no authority over the release. In section 3 I had been a team lead for about one month, with three engineers.

---

## Framing

The hard part of this question is not "am I right about the architecture".

The hard part is that three things are true at the same time:

- the flaw is real, and it lands in 6 to 12 months
- the team has already agreed
- the delivery pressure is now

Put those together and the shape of the problem appears. **The cost of being right is paid today, by other people. The benefit arrives much later, and it arrives as something that did not happen.** Nobody gets thanked for an outage that never occurred.

That is why the answer cannot just be "I would speak up". Speaking up is the easy part. Everything that decides whether it works happens around it: what I ask for, when, in front of whom, and what I do when the answer is no.

One more thing worth saying before the steps. A decision that is already made is a different object from a decision still being made. Re-opening one costs the team time and costs me some credit, and that credit is a limited account. I can do this a few times a year, not a few times a month. So part of the job is knowing which concerns are worth spending it on — which is why section 1 ends with the line about what I escalate and what I let go.

---

## 1. How I would raise the concern

### Step 0 — check myself first

Believing a design is flawed is not the same as it being flawed. The missing knowledge may be mine. So before I speak to anyone, I do a short piece of research and try to write down three things: what breaks, roughly when, and what evidence would prove me wrong.

I time-box this. A few hours, not a week. There is delivery pressure, and a concern that arrives even later is worth even less.

If I cannot write those three lines, I do not have a concern. I have a preference. A preference is "I would have built it differently". A concern is "at around 50 tenants this query goes from 20ms to 2s, and here is why".

### Step 1 — admit the concern is late, then raise it anyway

If the design was presented and agreed in a meeting with the whole team, then it is the team's decision. It does not belong to the person who proposed it. That matters for how I raise it.

It also means the right moment was that meeting, and I missed it. I say so when I raise it. Not as an apology — as information. A late concern costs the team more than an early one, and the reason it is late is me.

Being late is a reason to be careful about how I raise it. It is not a reason to stay quiet. A design that is wrong stays wrong whether or not I noticed in time.

### Step 2 — the person who proposed it, privately, first

A short 1-on-1. I describe the concern, the trade-off, and what I think happens in six months if we keep the design as it is.

I do this for two reasons. The first is respect: they hear it from me before they hear it in front of the team. The second is that they may simply show me I am wrong, and then nothing goes further. I end the conversation by telling them I plan to raise it with the team, so that is not a surprise either.

### Step 3 — then the team, in writing

I post it in the team channel and mention the team. In writing rather than in a meeting, on purpose: nobody has to react live, and the person who proposed the design reads it alone before anyone else replies.

I do not go to my manager first. That turns a technical question into an authority question, and it teaches the team that I escalate instead of talk. The manager is in the channel and reads it with everyone else.

### Step 4 — how I frame it

I bring evidence, not an opinion. A small benchmark, a proof of concept — a throwaway build that tests one question and is then deleted — or an incident that already happened to us. The argument then belongs to the evidence instead of to me. The person who proposed the design can change their mind without losing to a colleague.

I ask about the risk instead of announcing the flaw. "What happens to this at 50 tenants?" invites the team to think. "This will not scale" invites them to defend. The content is the same. The result is not.

I say what I think happens in six months, with numbers wherever I have them.

And I price my own fix. If what I want costs two weeks now, I say two weeks out loud. A concern with no cost attached is easy to dismiss, and it deserves to be.

### Step 5 — what I actually ask for

I am not asking the team to reverse the decision. Under delivery pressure that ask loses, and it should. The team weighed this once already, and I am the one who is late.

What I want is not a different decision. It is for this decision to stay cheap to change. So I ask for the smallest things that keep the door open:

| Ask | Cost now | What it buys |
|---|---|---|
| write the risk into the decision record | about zero | when the symptom appears, someone recognises it instead of debugging blind |
| measure the thing I say will move | small | turns a prediction into an alarm |
| keep one seam loose — an interface, not a hard-wired call | small | makes the later fix a change in one place |
| agree a trigger: "if X crosses Y, we revisit" | about zero | the revisit is agreed in advance, so it is not a new argument later |

The last row is the one I care about. The expensive argument is not this one. It is the one in six months, when the problem is real and the team is busier than it is today. Agreeing the trigger now means nobody has to be persuaded twice — the decision to revisit is already made, and only the number has to arrive.

If I get one of those four, I take the trigger.

Then the lead decides. That is the right shape, and I do not need the decision to go my way. I need it to be made with the risk written down and a way to see it coming.

### Step 6 — disagree and commit, and what that really means

Most of the time the team says go anyway. Then I build it. Properly, at full speed, with my name on it.

That means no slow-walking. No half-effort so the thing fails in a way that proves me right. No "as discussed, this was not my idea" in the commit messages or the code comments. If the design fails because I built it badly, I cannot tell the difference between my prediction and my own sabotage, and neither can anyone else. The prediction becomes worthless.

"Disagree and commit" is often used to mean "stop talking now". That is not what it means here. It means two things at once, and both of them are mine to keep:

- **I commit to the work.** The team's decision is now my decision. I do not get to hold a private exception.
- **I keep the trigger visible.** The measurement from Step 5 stays on a dashboard. If it moves, I say so — early, once, without a speech.

The second half is the part people drop. A concern that is raised loudly and then abandoned teaches the team that my concerns expire, which makes the next one cheaper to ignore.

One more thing I owe the person who proposed the design: if it works, I say so out loud, in the same channel where I raised the doubt. Section 4 is about that.

### When I would escalate anyway

Everything above assumes the decision can be changed later. Most can. Some cannot, and for those the calculation is different.

I use reversibility as the test. Not how strongly I feel, and not how expensive the mistake would be — how hard it is to undo.

| Kind of decision | What I do |
|---|---|
| We can change it in a month | Raise it once, take the trigger, build it |
| Expensive to change, but possible | Raise it, ask for the loose seam, accept the answer |
| Cannot be undone | Escalate, and keep escalating until someone with the authority has said yes in writing |

The third row is small but real. It covers a short list:

- **Data we would lose or corrupt** and cannot rebuild from anywhere.
- **A security or privacy hole.** A leaked record cannot be un-leaked. There is no rollback for it.
- **A promise to a customer or a regulator** that the design cannot keep.
- **A one-way door in the data model.** A schema or a tenant boundary that everything else will be built on top of. In six months it is not a decision any more, it is the ground.

For those I go to the manager, and if needed past the manager. I say plainly that I am escalating and why, and I tell the team I am doing it — escalating behind people is how you win once and lose the room.

Then I still accept the answer. Escalation is asking for a decision to be made at the level that owns the consequence. It is not a way to keep voting until I win.

I want to be honest about the size of this list. In my experience it is short. Most designs I have disliked turned out to be fine, or were quietly replaced later without any drama. If I escalated every concern that felt strong at the time, the ones that actually mattered would have arrived sounding exactly like the rest.

---

## 2. A real disagreement

### The change

At a previous company we had a paid feature called crosspost. A customer listed an item on our main marketplace — call it Marketplace A — and crosspost copied that listing onto a second, smaller marketplace we also ran, Marketplace B. Fewer than 15% of our customers paid for it.

The company decided to make it free for everyone. I was the senior engineer doing the work.

### The number I had

Crosspost ran on events. Whenever a listing was created, updated or deleted, we published a message to an **Amazon SQS queue**. SQS is Simple Queue Service, a managed queue: it holds messages until something reads them. The Marketplace B side read from that queue and did the copying.

Making the feature free for everyone meant every existing listing of every customer became a message. We had around 19,000 customers with roughly 100 listings each. About 1.5 million messages, published as fast as we could publish them.

Nobody knew what Marketplace B could actually process per second. That was my concern in one sentence: we were about to hand another team a workload nobody had measured, to be consumed by a service nobody had load tested.

### What I asked for, and why that was the mistake

I raised it with my manager rather than in the team channel. This was a cross-team dependency, not a design disagreement, and he owned that boundary. I still think that part was right.

I asked that we tell the Marketplace B team to expect a large volume, so they could prepare. He agreed, and he told them.

That ask was the mistake, and it was mine. Read it again. It has no number in it. No rate, no window, and no way to check the answer. I had 1.5 million written in my own notes and I did not put it in the message. Nobody ever said what "prepared" would mean, so nobody could confirm it — and everybody could agree to it.

A phased rollout was also discussed and the product team rejected it, for a real reason. Marketing had been advertising free crosspost for about a month. Turning it on for some customers and not others would produce exactly the complaints we were trying to avoid. I accepted that, and I took it to mean everything had to move at once.

### At the door

On the day, just before running it, I asked my manager whether I needed written confirmation from the Marketplace B team that they were ready. He said no — deliver what we said we would deliver, and the rest is on him.

I said once more what I thought would happen. If they were not ready, the queue would back up and customers would notice. He told me to proceed. I proceeded, properly. I was a senior individual contributor and not the person who owned the release, and I do not think going along with it was wrong.

But notice when I asked. Minutes before execution, at the door. That is the most expensive possible moment to say "wait", and it is the moment where the answer is almost always "go". A cross-team dependency belongs in the plan, in writing, a week earlier.

### What happened

Fifteen minutes in, the queue latency climbed and kept climbing. Marketplace B was not prepared. The backlog took about an hour to clear.

The people who felt it were the wrong ones. Our existing paying crosspost customers now sat behind 1.5 million backfill messages, so their own listing updates stopped appearing on Marketplace B in any reasonable time. A change that gave the feature away for free degraded it for the customers who had been paying for it.

Customer support started receiving complaints, the issue was escalated to the CTO, and we ran an emergency session. The fix we landed on was a second SQS queue, used only for the backfill, so the live production queue was left alone. I re-ran the backfill through it. That worked.

### What I would do differently now

**Put the number in the ask.** Not "expect a large volume". Instead: "this is 1.5 million messages, we would like to drain it in about four hours, that is roughly 100 per second on top of your normal traffic — can you take that, and how would we know?" That version is answerable. More usefully, answering it honestly forces the other team to go and measure, which is the thing that never happened.

**Isolate the backfill from live traffic, from the start.** A one-time bulk load and ongoing real-time events are two different workloads, and we put them through one queue. Whichever is behind, the other one waits. The separate queue we invented in the incident room was available to us on day one and I did not think of it. That is the part I find hardest to write down.

**Separate "who can use it" from "how fast we backfill".** This is the one I would most want back. Product's constraint was about availability — every customer gets the feature on the same day, because that is what marketing promised. I heard that as "all 1.5 million messages go at once". Those are not the same thing. We could have switched the feature on for all 19,000 customers at the same moment and still drained the historical backlog through the isolated queue at a controlled rate over a day. New listings would cross-post immediately for everyone, which is what the promise actually said. Both constraints survive, and I did not see it at the time.

**Agree the abort number before starting.** I watched for fifteen minutes and saw latency rise. Nobody had agreed beforehand what number meant stop, so the decision to keep going or pull back got made live, in a chat channel, by whoever was most senior at the time. Any number agreed in advance would have been better than that.

### The lesson that went into section 1

I was right about the risk and it did not help, because what I asked for could be granted without anything changing. "Let them know" is awareness, and awareness is not an ask.

That is why section 1 argues for a measurement and an agreed trigger instead. It is not a framework I read about. It is the thing I did not do here.

---

## 3. A real mentoring story

### What I was given

I had been a Lead Software Engineer for about one month, with three engineers on my team. I was then asked to mentor and evaluate two junior engineers from another team. They were on a three-month probation contract and they were in the last month of it. Their first two months had been with a different lead.

So the honest description of the task is not "mentor two juniors". It is "decide, in four weeks, whether to keep two people who have already spent two months not working out somewhere else".

I did not say that out loud at the time. I should have.

### What I tried

I started with a 1-on-1 with each of them, to understand what they were good at, what they struggled with, and how they communicated.

What I found was worse than I expected. They did not know how to build software. They said they knew basic PHP, a web programming language, and that was close to the whole of it.

So I gave them a small, self-contained task: a basic employee management page with **CRUD** operations — Create, Read, Update and Delete, the four basic things an application does to records in a database. It is the kind of exercise a university student finishes in a few days. They agreed a one-week deadline. I told them they could pair with me or with anyone on my team, and I told my team to help them if asked.

Then I deliberately left them alone for two days. I wanted to see whether they would ask anyone for help.

On day three I asked how it was going. They said there were no issues. A week later the task was not finished, and they again said there were no issues, and that they would finish that week. I stayed hands-off through that second week too, still watching whether they would reach out to the team.

In week three, with the task still not done, I started pairing with them one to two hours a day. By the end of week four it was still not finished.

I recommended to my Engineering Manager that their contracts not be extended. He made the decision and he spoke to them.

### The hardest part

It was not the decision. By week three the decision was obvious.

The hardest part was that the gap was much bigger than the job allowed for. They did not need help with our codebase or our domain. They needed to be taught how to write software, from close to the beginning. At the same time I had my own deliverables and three other engineers whose daily blockers I was there to clear.

The teaching that would have actually helped them was full-time work, and I had a few hours a week. I knew that by the end of week one, and I kept going anyway, as if four weeks of part-time attention might somehow be enough.

### What I got wrong

**I never told them they were failing.** Not once, not in those words. I assumed the probation contract said it for me — they knew they were on probation, so surely they knew what "not finished after three weeks" meant.

That assumption was the mistake, and it is the thing I would change first. Being on probation tells someone the stakes. It does not tell them they are currently losing. Those are different pieces of information, and only one of them is actionable. They also knew their previous lead had been evaluating them for the first two months. I do not think they understood that I was now the one doing it.

**I read "no issues" as information.** It is not. A junior engineer who is three weeks behind and reports no problems is telling you one of two things: they do not know enough to see that they are stuck, or they are too frightened to say so. One month from a contract decision, fear is the more likely one. I should have stopped asking about status and started asking to see the code. The work itself would have told me in ten minutes what two weeks of check-ins did not.

**My two weeks of observing cost them more than it cost me.** I wanted to learn whether they would ask for help. That is a fair thing to want to know. But I ran it as a silent test, on people who did not know they were being tested, using half of the only time they had left. I could have learned the same thing by pairing on day one and watching how they behaved when help was in front of them.

**I handed over the conversation.** Recommending the decision to my Engineering Manager was right — it was his to make, not mine. Asking him to deliver it was not. I did that because I had been a lead for one month and did not know how to have that conversation. That was honest at the time, and it is still the part I am least comfortable with. The right version is that I am in the room for a decision I recommended.

### The same month, a different engineer

One of my own three team members was, by my judgement, the least skilled person on the team.

He is also the clearest example of mentoring working that I have. He said out loud, most days, what he was stuck on. The team helped him. He grew visibly week by week, and the amount of supervision he needed went down steadily until it was close to none.

Setting those two stories side by side is uncomfortable, and it is the most useful thing in this section. The engineer who succeeded was not the most able one. He was the one who surfaced being stuck. The two who failed stayed silent and said everything was fine.

And I ran an environment that rewarded exactly that difference. Help was available to anyone who asked for it. The person who already knew how to ask got better every day. The two who did not know how to ask got two weeks of my silence, in the last month they had.

I do not think that explains away the outcome. They were a long way from the bar, and four weeks was not going to close it. But "help is available if you ask" is not a support system. It is a filter, and it filters for a skill that juniors often do not have yet.

### What I would do differently

1. **Say the words, in week one.** "This should take a week. If it slips, tell me the same day. The contract decision depends on this." An assumption is not a message.
2. **Ask to see the work, not the status.** Open the branch together. "No issues" from someone who is behind means nothing.
3. **Pair from day one.** If I want to know whether someone asks for help, I can learn that with help sitting next to them, instead of running a silent experiment with their job as the stake.
4. **Name the real shape of the task before accepting it.** Four weeks, part-time, for two people who need teaching from the ground up, is an evaluation dressed as a mentorship. I should have said that to my manager at the start and asked what a fair test would actually look like.
5. **Be in the room.** I would recommend the same decision today, and I would deliver it myself.

---

## 4. Being wrong

### How I would know

I write the concern down as a claim that can fail. A number and a date. "At 50 tenants this query passes 500ms, and we reach 50 tenants around March." That is what Step 0 was for.

So finding out is not complicated. March arrives, we have 60 tenants, the query is still at 40ms. I was wrong. There is nothing to interpret.

A vague concern cannot do that. "This will not scale" is never wrong. It just sits there, quietly true, making every later conversation about the design a little heavier. Being specific is what makes being wrong possible, and that is the point of being specific.

My colleagues are evidence too. If two or three people I trust tell me I have this wrong, that is a strong signal — usually about something I cannot see from where I sit, like what the business actually plans to do next year. But I treat it as a reason to go back and check my numbers, not as the answer. I cannot have it both ways. Section 1 only makes sense if a team that agrees can still be wrong, so a team that disagrees with me can be wrong too.

The case I watch hardest is the half-hit: the design does run into trouble, but not for the reason I gave. That is not being right. It is a different problem that arrived on schedule, and if I count it as a win I learn nothing from it.

### How I handle it in front of the team

I say it in the same place I raised it. The team channel, not a private message to the person who proposed the design. A doubt raised in public and dropped in private does not go away — it stays attached to the design, and the person who proposed it is the one carrying it.

I say what I got wrong, not only that I was wrong. "The cache absorbed the load I expected to hit the database" is useful to everyone reading. "My bad" is noise. And I say plainly that the other person was right.

Then I stop. No long apology. Over-apologising turns the moment back into a conversation about me, and it teaches the team that being wrong here is expensive.

That last part is the whole reason this matters. Being wrong is not a big deal, and the useful thing is to let people see that. A senior engineer who is publicly wrong, briefly, and then gets back to work is showing every junior on the team what will happen to them when they are wrong. Telling them it is safe does not work. Watching it does.

---

## Where this answer is weak

**Section 1 assumes a team where being wrong is safe.** Posting a concern in the team channel works when disagreement is normal there. On a team where it is not, the same message reads as an attack on the person who proposed the design, and everyone spends the thread managing that instead of the risk. On a team like that I would keep it to 1-on-1 conversations and accept that it moves slower, and I would treat the fact that I had to do that as its own problem worth raising with the manager separately.

**The trigger only works if somebody is still watching.** Section 1 rests on agreeing a measurement and a number that means "revisit". Six months later, the people who agreed it have moved to other work, and the dashboard nobody looks at is one of the most common objects in our industry. An alert that pages someone is better than a chart. Even then, the honest version is that this reduces the chance of being surprised rather than removing it.

**Section 3 is a story about mentoring failing.** I have not presented it as a success and I do not want it read as one. Two people lost their jobs. I think the recommendation was right, and I still do not know whether a better four weeks — or an honest conversation in week one — would have changed the outcome for either of them. I cannot claim it would have. I also cannot claim it would not have.

**My authority was different in each story, and it was never very much.** Section 2 is a senior individual contributor who did not own the release. Section 3 is a lead of one month standing, with three engineers. Neither is a story about someone with the power to simply decide. That is worth knowing when reading section 1, which is written as though the room will listen. Sometimes it does not, and I have less experience of changing that than I would like.

**Section 1 is reasoned, not remembered.** It is what I believe I would do, and it is built out of what section 2 taught me. But section 2 is a case where I did not do it. I have not yet run the full method — number, private heads-up, written ask, agreed trigger — from start to finish and watched it work. The theory is sound and it is not yet tested by me.

**Nothing here covers the case where I am overruled repeatedly on things that matter.** Section 1 ends with "then the lead decides", which is the right answer once. It is not the right answer for the fifth time in a row on the same kind of risk. At that point the problem is not the architecture, it is that my judgement is not trusted or the team is not run well, and both need a different conversation than this document describes.

---

## Summary

| Move | What it buys | What it costs |
|---|---|---|
| write the concern as a number and a date | it can be checked, and it can be wrong | a vague worry feels safer, because it can never be disproved |
| private heads-up, then the whole team | the person who proposed it is never surprised in public | slower than just saying it, and it looks like lobbying if done badly |
| ask for a trigger, not a reversal | costs the team almost nothing today, and it ends the argument in six months before it starts | the risk stays in the product; I have made it visible, not gone |
| price my own fix out loud | the team can weigh it honestly | it is easier to dismiss a concern once it has a bill attached |
| disagree and commit, properly | the team keeps moving, and my prediction stays worth something | I own the bad outcome too, and I cannot say I told them so |
| escalate only what cannot be undone | the rare serious concern arrives sounding different from the rest | I let real problems through, and some of them will hurt |
| be visibly wrong, briefly, in public | it shows every junior what happens to them when they are wrong | it spends a little credibility each time, and the account is finite |
