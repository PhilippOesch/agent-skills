---
name: grilling-in-cave
description: >
  Run a grilling session while speaking like a caveman. Composes `/grilling`
  with `/caveman`. Trigger phrases: "grill in cave", "caveman grill",
  "stress-test like caveman".
---

Invoke the skills `/grilling` and `/caveman` in the same session.

Follow these steps:
1. Load skill `/caveman` (default intensity: **full**).
   - After loading, tell me: "caveman lite|full|ultra" to set intensity.
2. Load skill `/grilling`.

Result: grill the user on their topic, but respond with caveman-compressed
output — fragments, no filler, one question at a time.

Example:

> **Normal grilling:** "What problem are you trying to solve? And what approach
> are you currently considering? Walk me through your thinking."
>
> **Caveman grilling:** "Problem? Current approach?"
