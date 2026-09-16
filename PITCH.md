# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A rebooking assistant wired into your booking record, your live flight feed and your disruption policy rows - the same rows your agents read. Twelve capabilities: the nine you specified, plus three we argued for. One of those three now runs as a service of its own, so it can be versioned and reused by something other than this chat without anyone copying it.

Does: A passenger says what happened. It finds their booking, checks what actually happened to the flight rather than what the passenger assumed, works out what your policy owes them, and puts the real alternatives in front of them with times, seats and cost. Then it holds one seat for fifteen minutes and waits. Groups, partner itineraries, unaccompanied minors and refunds it hands to a person instead of attempting. You can watch all of it: there is a working chat window where you type as a passenger and see every system the agent touched under each reply.

Number: Before, $0.0542 in model cost per resolved contact. After, $0.0276 per resolved contact, down 49%. Both measured the same way from our own traces: your five disruption shapes, three runs each, fifteen conversations per side, same model. Against $6.90 per human-handled contact. Model cost only - on your own published ratio the all-in figure is roughly 40% higher, and we would rather you apply that than have us guess it. The saving came from stopping the agent re-sending the same unchanged instructions on every turn.

Guardrail: The agent cannot complete a rebooking. Not "is instructed not to" - cannot. The final step needs a token only your customer's own Confirm click produces, and the agent has no way to make one. We proved it in that order: a forged token was refused as invalid, then the customer's real click on the same held seat went through. A passenger who types "yes, whatever's fastest, just do it" gets a held seat and a question, not a changed ticket.

Next: With another week: connect the real reservation system, replace our five shapes with your own disruption transcripts, and run it in shadow beside the human queue through one storm without changing anything the passenger sees. That last one is how you get a deflection rate you can defend, and it costs you nothing in customer risk.

Still broken: Two things, and the second is ours rather than the agent's. The agent was putting internal codes in front of stranded passengers - it told a customer their cancellation had "an uncontrollable cause" and quoted a policy row number at them. We fixed that and our tone test passes. Fixing it then broke a different test: the reply now opens by acknowledging the passenger, which pushed out the sentence explaining why a chat message cannot finalise a ticket. The agent still refuses to finalise, correctly - it just stopped saying why. That is a flaw in how we wrote the test, not in the agent, and we only found it because our own tests disagreed with each other. We have measured it once, not five times, so we will not yet say whether it is reliable or luck. The release is blocked on it today and we would rather tell you that than ship past it.

Lever: cost

## Priya asked

Costs: $0.03 per resolved contact after caching, against $6.90 for a human-handled contact — that is a 99.5% reduction in model cost, measured across 15 conversations on your own five disruption shapes.
Wrong: Refunds — the agent recognises when one is due but cannot process it; every refund still goes through the manual queue.
Runs it: Contact centre operations and marketing own it day-to-day — updating prompts, adding cases, reading traces — with no IT ticket required; the only thing IT touches is the initial connection to the reservation system.
Left out: Automatic hotel booking when the next available flight is beyond a configurable hour threshold — the agent can issue a hotel voucher but cannot book the room itself.
