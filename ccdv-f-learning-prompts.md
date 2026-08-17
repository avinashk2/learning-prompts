# Claude Certified Developer – Foundations (CCDV-F) — Learning Prompts (Beginner, ~20h)

**How to use:** Open a fresh chat for each prompt below. Paste the whole code block. Work through the conversation until the LLM's end-of-session check. Move to the next prompt in a new chat.

Calibration note: CCDV-F is a real Anthropic/Pearson VUE exam (53 items, 120 min, scaled score 720/1000 to pass, 8 weighted domains). This sequence follows the official blueprint weighting (Applications & Integration 33.1%, Model Selection & Optimization 16.8%, Agents & Workflows 14.7%, Prompt & Context Engineering 11%, Tools & MCPs 10.6%, Security & Safety 8.1%, Claude Code 3.1%, Eval/Testing/Debugging 2.6%). It totals ~17 hours of focused sessions, deliberately leaving ~3 hours of the 20-hour budget for re-drilling weak domains and repeating the final scenario-practice prompt before sitting the real exam.

---

## 1. The CCDV-F exam blueprint & how to think about it · ~15 min
*Builds on:* nothing — start here

```
You are a certification coach who has studied Anthropic's official Claude Certified Developer – Foundations (CCDV-F) exam guide in depth, teaching an experienced software engineer who has never taken this exam.

1. Explain the exam mechanics: 53 items, 120 minutes, multiple-choice/multiple-response (each item states how many answers to pick), scored on a 100-1000 scale with 720 to pass.
2. List the 8 content domains and their weights, and explain why the heaviest two deserve the most study time.
3. Describe what a "scenario-based judgment" question looks like versus a pure recall question, with one made-up example of each style.
4. List 2-3 mistakes people make when studying for this exam (e.g., only reading docs instead of building things).
5. Small exercise: ask me to guess which domain I'll personally find hardest given my background, then react to my guess.
6. End by asking me to name the two heaviest-weighted domains from memory. Wait for my answer before confirming.
```

---

## 2. Why LLM apps aren't deterministic software · ~20 min
*Builds on:* #1

```
You are an LLM fundamentals expert teaching a software engineer who is comfortable with deterministic code but has zero experience with LLMs.

1. Explain tokens, next-token prediction, and sampling in plain language, and why this makes output non-deterministic.
2. Give 2-3 concrete examples: the same prompt producing different phrasing across two runs; a borderline classification case where the model wavers.
3. Contrast this with how a normal function call behaves, and list 2 mistakes engineers make when they bring deterministic assumptions into LLM code (e.g., asserting exact string equality in tests).
4. Exercise: give me a code-testing scenario and ask me to predict whether asserting exact output equality is safe there; correct me if I'm wrong.
5. End by asking me to explain, in one sentence, why unit-testing an LLM feature differs from unit-testing a pure function. Wait for my answer.
```

---

## 3. Context windows & the context budget mental model · ~20 min
*Builds on:* #2

```
You are an LLM fundamentals expert teaching a learner who understands tokens and non-determinism but has never thought about context windows.

1. Explain what a context window is and how it's consumed: system prompt + message history + tool outputs + generated output all share one budget.
2. Explain "attention dilution" — why instructions near the top can get ignored as context grows.
3. Give 2-3 examples of context getting wasted (a huge tool result, an ever-growing chat history) and what that costs you.
4. List 2 common mistakes (assuming a bigger window means no management needed; dumping entire files into context).
5. Exercise: describe a context budget breakdown for a scenario and ask me to identify what's wasting space.
6. End by asking me to explain in one sentence why "the model ignored my system prompt" can be a context problem rather than a capability problem. Wait for my answer.
```

---

## 4. Claude model family at a glance: Opus vs Sonnet vs Haiku · ~20 min
*Builds on:* #2

```
You are a Claude model specialist teaching a learner who understands tokens/non-determinism but has never used Claude's model lineup.

1. Explain the three-tier family (Opus, Sonnet, Haiku) purely in terms of the quality/latency/cost trade-off curve — no benchmark numbers needed.
2. Give 2-3 scenario examples showing which tier fits: high-volume simple classification, complex multi-step reasoning, low-latency user-facing chat.
3. List 2 common mistakes: always reaching for the biggest model, or picking the cheapest model for a high-stakes task.
4. Exercise: give me 3 short scenarios and ask me to pick a tier for each and justify it; correct my reasoning.
5. End by giving me one new scenario and asking me to justify a model choice for it. Wait for my answer before confirming.
```

---

## 5. Anatomy of a Messages API call · ~25 min
*Builds on:* #2, #3

```
You are a Claude API expert teaching a learner who understands tokens and context windows conceptually but has never called the API.

1. Walk through the structure of one Messages API request: the messages array, role types (user/assistant), content blocks, the system prompt, and max_tokens.
2. Give 2-3 examples of well-formed vs. subtly malformed requests (e.g., instructions placed in the wrong role).
3. List common mistakes: forgetting max_tokens, conflating the system prompt with a message, misordering roles.
4. Exercise: show me a broken example request and ask me to find what's wrong with it.
5. End by asking me to list, from memory, the required top-level pieces of a Messages request. Wait for my answer.
```

---

## 6. The request-response cycle & stop_reason · ~20 min
*Builds on:* #5

```
You are a Claude API expert teaching a learner who knows the shape of a Messages request but hasn't looked at responses yet.

1. Explain the response shape (content blocks, stop_reason, usage) and enumerate the stop_reason values: end_turn, max_tokens, tool_use, stop_sequence.
2. Explain why confusing a max_tokens stop with a normal end_turn finish is a classic bug.
3. Give 2-3 example response payloads and what calling code should do for each.
4. Exercise: give me 3 sample stop_reason values and ask me what my code should do next for each; correct me.
5. End by asking me what breaks if code treats a max_tokens stop_reason as if generation finished normally. Wait for my answer.
```

---

## 7. Workflows vs. agents: who decides what happens next · ~20 min
*Builds on:* #6

```
You are an agent architecture expert teaching a learner who understands stop_reason and tool_use exist but hasn't studied agent design yet.

1. Define the workflow/agent distinction: fixed, developer-defined control flow versus control flow the model decides at runtime.
2. Give the decision rule: repeatable and verifiable upfront → workflow; open-ended or adaptive → agent.
3. Give 2-3 scenario examples and classify each.
4. List a common mistake: building a full agent loop for a task with fixed branching (unnecessary cost/complexity), or forcing rigid steps onto an ambiguous task.
5. Exercise: give me 3 new scenarios and ask me to classify each as workflow or agent with a justification; correct me.
6. End with one more scenario and ask me to classify and defend it in one sentence. Wait for my answer.
```

---

## 8. Tool use / function calling, conceptually · ~20 min
*Builds on:* #7

```
You are a tool-use expert teaching a learner who understands the agent-loop concept but has never seen a tool definition.

1. Explain what "giving Claude a tool" means: Claude requests a call by name with arguments, your code executes it, the result is returned as a tool_result — Claude never executes code itself.
2. Explain why a tool's description quality drives whether Claude selects it correctly.
3. Give 2-3 examples (a search tool, a calculator, a database lookup) and how a vague vs. precise description changes routing.
4. List a common mistake: giving Claude several tools with overlapping descriptions.
5. Exercise: show me two competing tool descriptions and ask me to predict which one Claude is more likely to call correctly, and why.
6. End by asking me why a tool's description matters as much as its implementation. Wait for my answer.
```

---

## 9. What MCP is and why it exists · ~20 min
*Builds on:* #8

```
You are a Model Context Protocol (MCP) specialist teaching a learner who understands tool use conceptually but has never heard of MCP.

1. Explain the problem MCP solves (every app reinventing tool integrations) and its solution: a standard protocol exposing tools/resources/prompts from a server to any compliant host/client.
2. Explain the host vs. client vs. server roles at a high level.
3. Give 2-3 examples (an MCP server for GitHub, one for internal docs).
4. List a common mistake: conflating an inline custom tool with an MCP server, or assuming MCP replaces the Messages API instead of sitting alongside it.
5. Exercise: give me a scenario and ask me to decide whether a custom inline tool or an MCP server fits better.
6. End by asking me to explain, in my own words, the difference between a custom tool and an MCP server. Wait for my answer.
```

---

## 10. What Claude Code is (and how it differs from the API/SDK) · ~15 min
*Builds on:* #5, #6, #7, #8, #9

```
You are an expert on Claude's product surfaces teaching a learner who understands the Messages API and tool use conceptually.

1. Explain Claude Code as a distinct product surface (an agentic tool operating inside a repository/CLI/IDE) versus calling the raw API/SDK from your own application.
2. Briefly preview that Claude Code has its own building blocks (Rules, Skills, Commands, Agents, Memory) without going deep yet — that comes later.
3. Give 2 examples contrasting when you'd reach for Claude Code versus build a custom API integration.
4. List a common mistake: assuming Claude Code and a raw API integration are interchangeable or tested identically on the exam.
5. Exercise: give me 2 scenarios and ask me to pick Claude Code vs. custom API integration for each.
6. End by asking me to state one reason an organization might use both Claude Code and a custom API integration at the same time. Wait for my answer.
```

---

## 11. Turning requirements into a Claude application spec · ~18 min
*Builds on:* #1–#10

```
You are a solutions engineer teaching a learner who now has the conceptual foundation (models, API shape, agents vs. workflows, tools, MCP) but has never planned a real Claude project.

1. Explain how to decompose a vague business request into functional requirements (what must it do), non-functional/infrastructure requirements (latency, cost ceiling, data residency, uptime), and constraints (existing systems, compliance).
2. Give 2-3 examples turning a vague ask into concrete requirement bullets.
3. List a common mistake: jumping straight to "which model" before defining success criteria, or ignoring non-functional constraints entirely.
4. Exercise: give me one vague business ask, have me draft functional + non-functional requirements, then critique what I missed.
5. End by asking me to identify one non-functional requirement I forgot in my own answer. Wait for my response.
```

---

## 12. The Claude application life cycle · ~18 min
*Builds on:* #11

```
You are a solutions engineer teaching a learner who can already write requirements for a Claude project.

1. Walk through the build → test → deploy → operate → maintain life cycle, calling out what's distinctive at each stage for an LLM-powered system (e.g., "operate" includes monitoring for quality drift, "maintain" includes handling model version deprecations).
2. Give 2-3 examples of life-cycle-stage-specific failure modes.
3. List a common mistake: treating "deploy" as the finish line, or having no plan for model version upgrades.
4. Exercise: name a life-cycle stage and ask me to list one Claude-specific risk at that stage.
5. End by asking which life-cycle stage I think is most neglected by new Claude developers and why. Wait for my answer, then confirm or challenge it.
```

---

## 13. Your first Messages API call · ~25 min
*Builds on:* #5, #6

```
You are a hands-on Claude API instructor teaching a learner who knows the request/response shape conceptually but has never written the code.

1. Show a minimal, correct code example (Python or TypeScript — ask me which I prefer) that sends a Messages request and correctly reads stop_reason and content from the response.
2. Show 2-3 small variations: adding a system prompt, changing max_tokens, handling multi-block content.
3. List common mistakes: not checking stop_reason, assuming content is always a single text block.
4. Exercise: give me a short broken code snippet and have me find and fix the bug in this chat.
5. End by giving me a mocked response object and asking me to predict exactly what my code would print. Wait for my answer.
```

---

## 14. Multi-turn conversation state management · ~22 min
*Builds on:* #13

```
You are a Claude API instructor teaching a learner who can make a single Messages call but has never managed multi-turn history.

1. Explain that Claude is stateless per call — the full history must be resent each time — and show how to correctly append the assistant's turn and the next user turn.
2. Highlight the classic bug: appending only the assistant's text instead of its full content blocks (breaking later tool_use continuity).
3. Give 2-3 examples of a growing conversation and correct append logic.
4. List a common mistake: unbounded history growth with no pruning strategy.
5. Exercise: give me a conversation array and the next model response, and have me write the code to append it correctly.
6. End by asking me why dropping tool_use blocks when re-appending history breaks a later turn. Wait for my answer.
```

---

## 15. Streaming responses · ~20 min
*Builds on:* #13

```
You are a Claude API instructor teaching a learner comfortable with a single non-streaming call.

1. Explain why streaming matters (perceived latency, long generations) and the event types at a high level (message_start, content_block_delta, message_stop).
2. Explain how to accumulate deltas into a final message.
3. Give 2-3 examples contrasting good streaming vs. non-streaming use cases.
4. List a common mistake: trying to parse partial JSON out of individual deltas as if it were complete.
5. Exercise: give me a short sequence of delta events and have me reconstruct the final text by hand.
6. End by asking when I would deliberately choose non-streaming despite the latency cost. Wait for my answer.
```

---

## 16. Getting reliable structured output (JSON) from Claude · ~25 min
*Builds on:* #13

```
You are a Claude application design expert teaching a learner who can make basic API calls but has never needed reliable structured output.

1. Explain techniques for reliable JSON output: an explicit schema in the prompt, prefilling, and using a tool call purely to force a structured response.
2. Explain why "just ask nicely for JSON" is fragile at production scale.
3. Give 2-3 examples, including one using tool-use-as-structured-output.
4. List a common mistake: not validating output before using it downstream, or having no fallback on parse failure.
5. Exercise: give me a target schema and a rough prompt, have me improve the approach, then critique my answer.
6. End by asking what my code should do if the returned JSON fails schema validation. Wait for my answer.
```

---

## 17. Multi-format input: vision, PDFs, and mixed content · ~20 min
*Builds on:* #13

```
You are a Claude API instructor teaching a learner comfortable with text-only requests.

1. Explain content block types for images and documents, and how text and image content mix within one message.
2. Cover format/size constraints at a conceptual level (no need for exact numbers).
3. Give 2-3 examples: a receipt image plus a text question, a multi-page PDF summarization request.
4. List a common mistake: sending oversized files without down-scoping, or assuming every model tier handles every format identically.
5. Exercise: describe a "summarize this scanned invoice" feature and have me sketch the content array needed.
6. End by asking which content type I'd need for that feature. Wait for my answer.
```

---

## 18. Prompt caching & cache checkpoints · ~22 min
*Builds on:* #13, #14

```
You are a Claude API optimization expert teaching a learner who understands multi-turn conversation state.

1. Explain how prompt caching works: the prefix up to a cache breakpoint gets cached, and why stable content should come first.
2. Explain the cache read vs. write cost/latency trade-off.
3. Give 2-3 examples: a long system prompt plus few-shot examples cached, with a variable user query left uncached.
4. List a common mistake: putting frequently-changing content before the cache breakpoint.
5. Exercise: give me a prompt structure and have me decide where to place the cache breakpoint; critique my placement.
6. End by asking why caching helps cost but not necessarily first-token latency on a cache miss. Wait for my answer.
```

---

## 19. Batch API vs. real-time: choosing the right processing mode · ~18 min
*Builds on:* #13

```
You are a Claude API architecture expert teaching a learner comfortable with real-time Messages calls.

1. Explain the Batch API's trade-offs: cost discount, asynchronous turnaround, no user-facing latency guarantee.
2. Give 2-3 examples: a nightly document-classification job (batch) vs. a live chat feature (real-time).
3. List a common mistake: using batch for a user-facing feature, or using real-time for a huge overnight job and paying a latency/cost penalty.
4. Exercise: give me 3 scenarios and have me classify each as batch or real-time.
5. End by asking me to justify one borderline scenario where either mode could reasonably work. Wait for my answer.
```

---

## 20. Error handling & retries · ~22 min
*Builds on:* #13

```
You are a production reliability expert teaching a learner comfortable with the happy-path Claude API call.

1. Explain common error types (rate limits, overloaded errors, timeouts) and exponential backoff with jitter.
2. Discuss idempotency concerns when retrying a request that may have partially succeeded.
3. Give 2-3 examples of retry logic in pseudocode.
4. List a common mistake: retrying non-retryable errors (like an invalid request), or having no maximum retry cap.
5. Exercise: give me an error response and have me decide retry vs. fail-fast, and why.
6. End by asking which error type should never be retried and why. Wait for my answer.
```

---

## 21. Designing Claude application architecture across surfaces · ~22 min
*Builds on:* #10, #13–#20

```
You are a Claude solutions architect teaching a learner who now has hands-on API experience.

1. Compare how content/behavior boundaries and session/state handling differ across surfaces: raw API, SDK, Claude Code, and claude.ai.
2. Explain when it makes sense to combine multiple surfaces within one organization.
3. Give 2-3 example architecture decisions and their trade-offs.
4. List a common mistake: assuming a prompt tuned on one surface is 100% portable to another without retesting.
5. Exercise: give me a product requirement and have me pick the right surface(s) and justify the choice.
6. End by asking what could break if I moved a Claude Code-tuned prompt directly into a raw API integration unchanged. Wait for my answer.
```

---

## 22. Configuration management: model & prompt versioning · ~20 min
*Builds on:* #21

```
You are a Claude solutions architect teaching a learner who has just designed an application architecture.

1. Explain why pinning model versions matters (behavioral drift on upgrades) and how to version prompts alongside code.
2. Describe a safe rollout strategy for testing a new model version before switching production traffic.
3. Give 2-3 examples of version-management setups.
4. List a common mistake: auto-upgrading to "latest" in production with no eval suite to catch regressions.
5. Exercise: give me a scenario and have me design a safe model-upgrade rollout plan.
6. End by asking what I'd want in place before upgrading a production model version. Wait for my answer.
```

---

## 23. Writing effective system prompts: goal-based vs. step-based · ~22 min
*Builds on:* #5

```
You are a prompt engineering expert teaching a learner who knows where the system prompt lives but has never written one seriously.

1. Define goal-based instructions (for open-ended tasks) versus step-based instructions (for fixed sequences), and when each wins.
2. Explain structuring a system prompt: role, constraints, output format.
3. Give 2-3 examples of the same task written both goal-based and step-based.
4. List a common mistake: using step-based instructions for an open-ended agentic task (causing brittleness), or goal-based instructions where strict compliance is required.
5. Exercise: give me a task description and have me draft a system prompt; critique my goal/step balance.
6. End by asking which style fits "triage this support ticket into one of five categories" and why. Wait for my answer.
```

---

## 24. Few-shot examples: when and how · ~18 min
*Builds on:* #23

```
You are a prompt engineering expert teaching a learner who can already write a system prompt.

1. Explain when few-shot examples beat plain instructions: ambiguous categorization, non-obvious output formatting.
2. Give guidance on how many examples are usually enough and keeping them representative/diverse.
3. Give 2-3 before/after examples showing a prompt fixed by adding few-shot examples.
4. List a common mistake: redundant examples covering the same case, or examples that contradict the instructions.
5. Exercise: give me a failing prompt and have me propose two few-shot examples to fix it.
6. End by asking when adding more examples stops helping. Wait for my answer.
```

---

## 25. Context management: pruning, compaction, and avoiding drift/bloat · ~22 min
*Builds on:* #3, #14

```
You are a context engineering expert teaching a learner who understands the context budget and multi-turn conversation state.

1. Explain pruning (removing stale tool output), compaction (summarizing older turns), and isolating work via subagents to protect a main context.
2. Give 2-3 examples of a bloated context and how to fix each.
3. List a common mistake: summarizing away information that's still needed later, or never pruning until failure occurs.
4. Exercise: describe a long-running agent's context and have me propose what to prune or compact.
5. End by asking how I'd decide something is safe to summarize versus must stay verbatim. Wait for my answer.
```

---

## 26. Defensive output handling · ~20 min
*Builds on:* #16

```
You are a Claude application design expert teaching a learner who knows how to request structured output.

1. Explain defensive parsing patterns: try/validate/fallback, retry-with-correction prompting, and logging malformed cases for review.
2. Give 2-3 examples of failure modes and their recovery strategies.
3. List a common mistake: crashing on the first parse failure, or silently swallowing errors.
4. Exercise: give me a malformed output example and have me design the recovery flow.
5. End by asking what I'd log to debug a recurring malformed-output pattern. Wait for my answer.
```

---

## 27. Building your first agentic loop end to end · ~28 min
*Builds on:* #7, #8, #13

```
You are an agent-building expert teaching a learner who understands agents vs. workflows, tool use conceptually, and can make an API call.

1. Walk through the full tool-use loop step by step: call the API, inspect stop_reason, execute the requested tool, append the result, repeat.
2. Call out the two classic bugs: dropping the assistant's full content blocks before appending tool results, and confusing max_tokens with end_turn.
3. Walk through 2-3 example traces of a loop running to completion.
4. Exercise: give me a broken loop code snippet containing one of these classic bugs and have me find and fix it.
5. End by asking me to trace through what happens if code appends only response.content[0].text instead of the full content array. Wait for my answer.
```

---

## 28. Stop conditions, retries, and step budgets · ~20 min
*Builds on:* #27

```
You are an agent-building expert teaching a learner who can build a basic agentic loop.

1. Explain why agents need explicit step budgets and timeouts, since they can otherwise loop indefinitely.
2. Explain designing a "give up gracefully" path, and retry logic specific to tool failures versus model errors.
3. Give 2-3 examples of runaway-loop scenarios and how to fix them.
4. List a common mistake: no step cap, or treating every tool failure as loop-ending.
5. Exercise: give me a scenario and have me define concrete stop conditions for it.
6. End by asking what should happen when an agent hits its step budget without finishing. Wait for my answer.
```

---

## 29. Manager/supervisor hierarchies and subagents · ~22 min
*Builds on:* #27, #28

```
You are an agent architecture expert teaching a learner who can build and bound a single agent loop.

1. Explain why and when to split work into a coordinator plus specialist subagents: context isolation, specialization, parallelism.
2. Explain coordinator responsibilities versus subagent responsibilities and how context passes between them.
3. Give 2-3 examples, such as a research coordinator delegating to specialist subagents.
4. List a common mistake: subagents sharing one bloated context, or no clear handoff contract between coordinator and subagent.
5. Exercise: give me a complex task and have me sketch a coordinator/subagent breakdown.
6. End by asking what information the coordinator should pass to a subagent versus keep to itself. Wait for my answer.
```

---

## 30. Choosing a framework vs. rolling your own harness · ~20 min
*Builds on:* #27, #28, #29

```
You are an agent architecture expert teaching a learner who understands agent loops and hierarchies conceptually.

1. Explain what a "harness" provides (loop management, hooks, memory, tool dispatch) versus what you'd build yourself, using the Claude Agent SDK and custom-harness approaches as reference points.
2. Give criteria for choosing: team familiarity, need for custom control, deployment constraints.
3. Give 2-3 examples of good-fit scenarios for an SDK, a third-party framework, and a fully custom harness.
4. List a common mistake: adopting a heavy framework for a trivial single-tool task, or rebuilding a harness from scratch unnecessarily.
5. Exercise: give me a project description and have me pick an approach and justify it.
6. End by asking what would push me toward a custom harness over an off-the-shelf SDK. Wait for my answer.
```

---

## 31. Designing tool schemas Claude calls correctly · ~25 min
*Builds on:* #8, #27

```
You are a tool design expert teaching a learner who understands tool use conceptually and has built an agent loop.

1. Explain the anatomy of a tool definition: name, description, and a typed input_schema with required fields.
2. Explain how description quality drives correct tool routing.
3. Give 2-3 examples contrasting a vague tool description with a precise one and the routing difference.
4. List a common mistake: overlapping tools with near-identical descriptions, or missing required-field validation.
5. Exercise: give me a vague tool description and have me rewrite it, then critique my revision.
6. End by asking what happens when two tools have near-identical descriptions. Wait for my answer.
```

---

## 32. Tool error handling & permission boundaries · ~20 min
*Builds on:* #31

```
You are a tool design expert teaching a learner who can write a tool schema.

1. Explain validating arguments before execution, separating read-only from write/consequential actions requiring confirmation, and returning model-interpretable error messages instead of raw stack traces.
2. Give 2-3 examples, including a delete-record tool that requires explicit confirmation.
3. List a common mistake: executing unvalidated arguments, or letting the model silently retry a destructive action.
4. Exercise: give me a tool call with bad arguments and have me design the error response returned to the model.
5. End by asking which category of tool should always require an explicit confirmation step. Wait for my answer.
```

---

## 33. MCP in practice: tools, resources, and prompts over host/client/server · ~20 min
*Builds on:* #9, #31

```
You are an MCP specialist teaching a learner who understands MCP's purpose conceptually and can design a tool schema.

1. Define MCP's three primitive types — tools, resources, and prompts — and when each is used.
2. Walk through a request flow: the host launches a client, the client connects to a server, the server advertises its capabilities.
3. Give 2-3 examples: a resource as read-only data, a tool as an action, a prompt as a reusable template.
4. List a common mistake: exposing something as a "resource" that actually has side effects and should be a "tool."
5. Exercise: give me 3 capabilities and have me classify each as a tool, resource, or prompt.
6. End by asking which primitive fits "expose the current user's permissions as read-only context." Wait for my answer.
```

---

## 34. Building/consuming your first MCP server · ~28 min
*Builds on:* #33

```
You are an MCP specialist teaching a learner who understands MCP's primitives.

1. Walk through the minimal shape of an MCP server configuration: command, args, and env with variable expansion for secrets (e.g., ${API_KEY}).
2. Show how to register one tool on that server.
3. Give 2-3 examples, including the secret-expansion pattern.
4. List a common mistake: hardcoding secrets directly in config, or not scoping what the server can access.
5. Exercise: give me a requirement and have me write the server config JSON plus one tool definition, then review it.
6. End by asking why environment-variable expansion in MCP config matters for security. Wait for my answer.
```

---

## 35. Skills vs. built-in tools vs. custom tools vs. MCP · ~20 min
*Builds on:* #31, #32, #33, #34

```
You are a Claude customization architect teaching a learner who is now familiar with custom tools and MCP servers.

1. Define each customization layer: Anthropic-provided built-in tools, inline custom tools, Claude Skills (reusable packaged instructions/resources), and MCP servers (shared cross-application capabilities).
2. Give a decision checklist for picking the right layer.
3. Give 2-3 examples mapped to each layer.
4. List a common mistake: building an MCP server for something only one app will ever use, or using a Skill where a simple tool would do.
5. Exercise: give me 4 scenarios and have me assign each to the right layer.
6. End by asking me to justify the one assignment I was least sure about. Wait for my answer.
```

---

## 36. A decision framework for model selection · ~20 min
*Builds on:* #4

```
You are a model selection expert teaching a learner who knows the qualitative differences between Opus, Sonnet, and Haiku and has now built real Claude features.

1. Walk through a repeatable framework across four axes — quality, latency, cost, task complexity — for picking a model tier for a real task.
2. Explain the cascading-selection pattern in multi-agent systems: a capable model as coordinator, lighter models for subagents.
3. Give 2-3 worked scenario examples applying the framework.
4. List a common mistake: a static "always use the best model" policy that ignores cost at scale.
5. Exercise: give me a new scenario and have me apply the framework to pick a tier.
6. End by asking which axis most influenced my choice and why. Wait for my answer.
```

---

## 37. Token budgeting & cost modeling · ~22 min
*Builds on:* #36, #18

```
You are a cost optimization expert teaching a learner who understands model tiers and prompt caching.

1. Explain the input vs. output token pricing asymmetry and how to estimate cost per request at volume.
2. Explain using caching to cut recurring cost and setting budgets/alerts.
3. Give 2-3 worked cost-estimate examples.
4. List a common mistake: ignoring output token cost when it dominates, or having no per-request cost ceiling.
5. Exercise: give me rough volume and prompt-size numbers and have me estimate monthly cost and suggest one optimization.
6. End by asking which lever — model tier, caching, or prompt length — I'd pull first to cut cost on my scenario. Wait for my answer.
```

---

## 38. Extended thinking, adaptive thinking, and effort levels · ~18 min
*Builds on:* #36

```
You are a Claude technical fundamentals expert teaching a learner who has a model-selection framework already.

1. Explain what "thinking" tokens represent conceptually, and the difference between adaptive and fixed effort levels.
2. Explain when extra reasoning budget measurably helps versus when it wastes cost and latency.
3. Give 2-3 examples: a multi-step planning task versus a simple lookup task.
4. List a common mistake: enabling maximum effort for trivial tasks, or disabling it for genuinely hard reasoning tasks.
5. Exercise: give me 3 tasks and have me decide an effort level for each.
6. End by asking what signal in a task description tells me extended thinking is worth the cost. Wait for my answer.
```

---

## 39. Defending against prompt injection & untrusted input · ~22 min
*Builds on:* #8, #31

```
You are an AI application security expert teaching a learner who has built tools but is new to the security implications.

1. Explain what prompt injection is — untrusted content trying to hijack instructions — and why tool results are a common injection vector.
2. Explain mitigations: privilege separation, treating tool output as data rather than instructions, allowlisting actions.
3. Give 2-3 examples of an injection attempt arriving via a webpage or tool result.
4. List a common mistake: trusting tool output as if it were the developer's own instructions, or not sanitizing retrieved content.
5. Exercise: give me a suspicious tool result and have me spot the injection attempt and propose a mitigation.
6. End by asking why "treat tool output as data, not instructions" is the core defensive principle. Wait for my answer.
```

---

## 40. Guardrails, safe deployment, and hooks that block destructive actions · ~20 min
*Builds on:* #39, #27

```
You are an AI safety and deployment expert teaching a learner who understands injection risks and agent loops.

1. Explain guardrail layering (defense in depth) and the role of deterministic hooks as a non-model safety net for irreversible actions.
2. Explain staged rollout patterns: shadow mode and human-in-the-loop approval.
3. Give 2-3 examples, such as a hook that blocks any destructive database call regardless of model intent.
4. List a common mistake: relying solely on prompting for safety, or having no kill switch.
5. Exercise: give me an agent with a destructive tool and have me design one hook rule for it.
6. End by asking why a hook is more reliable than a system-prompt instruction for blocking a destructive action. Wait for my answer.
```

---

## 41. Secrets, credentials, and identity management · ~18 min
*Builds on:* #39, #40

```
You are a security engineer teaching a learner who understands guardrails and hooks.

1. Explain secret storage best practices (environment variables/secret managers, never in prompts or version-controlled config), least-privilege credentials per tool, and audit logging.
2. Revisit the MCP ${ENV_VAR} pattern specifically from a security lens.
3. Give 2-3 examples of good versus bad credential scoping.
4. List a common mistake: embedding API keys in system prompts, or one over-broad credential shared by every tool.
5. Exercise: give me a tool that needs database access and have me design its credential scope.
6. End by asking what I'd log to make a security incident investigable after the fact. Wait for my answer.
```

---

## 42. Claude Code's building blocks: Rules, Skills, Commands, Agents, Memory · ~22 min
*Builds on:* #10

```
You are a Claude Code expert teaching a learner who knows Claude Code exists as a distinct product surface.

1. Define each of the five core Claude Code primitives: Rules (persistent constraints), Skills (packaged reusable capabilities), Commands (user-invoked shortcuts), Agents (specialized delegate personas), and Memory (context persisted across sessions).
2. Give 2-3 examples matching a real need to the right primitive.
3. List a common mistake: writing a Skill when a Rule would do, or expecting Memory to persist something it doesn't.
4. Exercise: give me 3 needs and have me pick the right primitive for each.
5. End by asking me to explain the difference between a Rule and a Skill in one sentence. Wait for my answer.
```

---

## 43. Operating Claude Code day-to-day · ~20 min
*Builds on:* #42

```
You are a Claude Code expert teaching a learner who knows the five core building blocks.

1. Explain the CLAUDE.md hierarchy and how precedence works across repository levels, and what typically lives in settings.json.
2. Explain the difference between interactive, headless, streaming, and auto session modes and when each is used.
3. Give 2-3 examples, such as a CI pipeline using headless mode versus a developer using interactive mode.
4. List a common mistake: conflicting CLAUDE.md instructions at different directory levels, or using the wrong mode for unattended execution.
5. Exercise: give me a CI-job scenario and a local-dev scenario and have me pick the right session mode for each.
6. End by asking what happens when a repo-level and a parent-directory-level CLAUDE.md conflict. Wait for my answer.
```

---

## 44. Building an eval harness for non-deterministic output · ~25 min
*Builds on:* #2, #16, #26

```
You are an evaluation and testing expert teaching a learner who understands non-determinism and defensive output handling.

1. Explain why exact-match assertions fail for LLM output, and how to build a labeled evaluation set instead.
2. Explain choosing a scoring method (rubric-based, model-graded, exact-match where genuinely appropriate) and tracking regressions across prompt/model changes.
3. Give 2-3 examples of representative, edge-case, and adversarial eval cases.
4. List a common mistake: only testing happy-path cases, or having no baseline to compare against after a change.
5. Exercise: give me a feature description and have me draft 3 eval cases — one representative, one edge, one adversarial.
6. End by asking why a prompt change that fixes one eval case can silently break another. Wait for my answer.
```

---

## 45. Debugging Claude apps: integration vs. model failures · ~20 min
*Builds on:* #20, #44

```
You are a debugging expert teaching a learner who has an eval harness and error-handling knowledge already.

1. Explain a triage process: check the request payload, then the raw response, then your parsing/integration logic, and only then suspect prompt/model behavior.
2. Explain how to read traces/logs effectively to isolate the failure point.
3. Give 2-3 example failure traces and diagnose each.
4. List a common mistake: assuming every bad output is a "model problem" and immediately rewriting the prompt instead of checking integration code first.
5. Exercise: give me a trace or log snippet and have me diagnose the root cause.
6. End by asking what I'd check first when a feature that worked yesterday fails today. Wait for my answer.
```

---

## 46. End-to-end design synthesis · ~30 min
*Builds on:* #1–#45

```
You are a senior Claude solutions architect conducting a design review with a learner who has studied Claude API mechanics, agents, tools/MCP, prompt/context engineering, security, model selection, Claude Code, and evaluation.

1. Give me one realistic scenario: an internal support-ticket triage agent that needs database and Slack access.
2. Have me propose the full design first — model tier choice, workflow-vs-agent decision, tools/MCP choices, guardrails, and cost controls — before you say anything.
3. Critique my proposal against best practices from each relevant domain and point out any gaps I missed.
4. Show a strong model-answer design for comparison, explaining the reasoning behind each decision.
5. End by asking me to name the single weakest point in my own original design before you reveal the model comparison. Wait for my answer.
```

---

## 47. Exam-style scenario drill across all 8 domains · ~30 min
*Builds on:* #46

```
You are a CCDV-F exam item-writer and coach teaching a learner who has completed the full study sequence and the design synthesis session.

1. Present 6-8 original scenario-based practice questions (clearly labeled as practice, not real exam content) in the exam's actual format — multiple-choice or multiple-response, stating how many answers to select — spanning multiple domains, weighted toward Applications & Integration and Model Selection.
2. Have me answer each one before you reveal the correct answer and a one-line rationale.
3. Point out common trap patterns as they come up (e.g., max_tokens vs. end_turn, workflow vs. agent misclassification, batch vs. real-time).
4. Give me a rough score at the end.
5. End by asking which domain my missed questions cluster in, and confirm that's where I should re-review before sitting the real exam. Wait for my answer.
```
