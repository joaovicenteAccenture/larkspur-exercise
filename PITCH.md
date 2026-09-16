# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A disruption-care chat agent for Larkspur Airlines, built on the Claude Messages API with 9 policy tools, a sensitive-case guardrail (flag_sensitive_case), and two MCP-served tools (next_available_day, fare_rules).
Does: It looks up a stranded customer's booking, checks their flight status, applies Larkspur policy, and tells them what they are owed — rebooking waiver, voucher, escalation, or refund path — in one conversation without a human.
Number: 5 shapes resolved in 19 turns total (3.8 turns per contact); 82,904 tokens in across the set, 3,218 schema tokens on every turn regardless of what fires.
Guardrail: flag_sensitive_case fires on sensitive bookings (e.g. unaccompanied minors) before any policy is applied; proven on the gate's probe in Build 2, attempt 1 of 3.
Next: Add a tone gate for abusive messages on the way in, enable prompt caching to cut per-turn token cost, and close the confirm_rebooking loop with a real customer confirmation token.
Still broken: Abusive messages (R8KD3F) get a calm, helpful answer with no tone check. The agent cannot detect aggression in the customer's opening message; Build 4 closes this gap.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
