# gald3r Readiness Report — Mistral Vibe CLI

> An honest accounting of how much of the gald3r framework installs natively on this
> platform, what degrades to an approximation, and what has no native home yet.
> Generated from a live documentation crawl on 2026-06-02.

**Overall readiness: ⚠️ Partial.** Mistral Vibe CLI is an open-source terminal coding agent
with genuinely strong native primitives. gald3r's skills, agents, and MCP layers land as
first-class citizens; its instruction and command layers fit only as a single layered blob,
and its lifecycle hooks have no verified host yet. (Scope: Vibe CLI only — Mistral Code and
Le Chat are not file-config surfaces.)

## C.R.A.S.H. capability grid

| | Capability | Native? | What gald3r gets here | The gap |
|---|---|:---:|---|---|
| **C** | Commands | ⚠️ | Slash commands work via `user-invocable: true` skills → `/skill-name` autocompletes in the prompt | No flat command-file directory — gald3r's `@g-*` command files must each be wrapped as a skill (heavy) or described in AGENTS.md (lossy) |
| **R** | Rules | ⚠️ | Always-on instructions via layered `AGENTS.md` (closer files override); optional custom system prompt via `system_prompt_id` | No scoped/glob rule loader — gald3r's per-file `g-rl-*` rules collapse into one AGENTS.md blob with no on-demand targeting |
| **A** | Agents | ✅ | Native custom agents + subagents: `.toml` profiles in `.vibe/agents/`, selected via `--agent`; `task`-tool subagents | Format mismatch — Vibe agents are TOML behavior profiles; gald3r's markdown `g-agnt-*` roles need markdown→TOML conversion (`safety` is a hint, not enforced) |
| **S** | Skills | ✅ | Native Agent Skills (`SKILL.md`, agentskills.io spec); folder-per-skill from `.vibe/skills/`, `.agents/skills/`, or `skill_paths` | Minor frontmatter drift — Vibe wants `allowed-tools` / `user-invocable`; gald3r's extra keys are ignored, so the fit is near-exact |
| **H** | Hooks | ⚠️ | Experimental hooks system with a single `post-agent-turn` lifecycle point (v2.9.0) | No published schema, no before-tool / session-start / pre-commit events — gald3r's PowerShell hooks have no verified wiring target (issue #531 still open) |

_Legend: ✅ native · ⚠️ partial / approximated · ❌ no native mechanism · ❓ unverified_

**Beyond C.R.A.S.H. — MCP: ✅** Fully native and well-documented — `[[mcp_servers]]` in
`config.toml` over http / streamable-http / stdio, namespaced tools filtered via
`enabled_tools` / `disabled_tools`. gald3r's MCP backend connects directly (caveat: no
OAuth-authenticated servers yet).

## Adoptable extras (non-C.R.A.S.H.)

Platform-native strengths gald3r can lean on, and which need wiring:

| Feature | Status | gald3r fit |
|---|:---:|---|
| Custom system prompts (`prompts/<id>.md` + `system_prompt_id`) | ✅ present | A real lever for injecting gald3r's base persona/system layer |
| Per-tool permission gating + agent `safety` levels | ✅ present | Covers some guardrail ground gald3r hooks would otherwise serve |
| Built-in `/loop` command (recurring prompts) | ✅ present | Extra automation surface; maps to gald3r recurring-workflow patterns |
| Custom compaction prompts (v2.11.1) | ⚙️ needs customization | Could tune context-compaction to preserve gald3r state across turns |
| Trusted-folders gate (`trusted_folders.toml`) | ⚙️ needs customization | Project `.vibe/` (and its skills/agents/prompts) only loads when trusted — install must account for it |
| Remote agents / Vibe Code Web | ➖ n.a. | Orchestration features, not file-config primitives — no gald3r install surface |
| Plugin support (Discussion #497) | ➖ n.a. | Requested, not yet shipped — no extensibility surface to target |

## The honest ceiling

gald3r adapts to this platform the way any third-party layer must — by mapping our commands,
rules, agents, skills, and hooks onto whatever extension points the platform happens to
expose. Where those points exist, the fit is clean. Where they don't, adaptation can only
*approximate* the real thing — a stand-in that covers the common case but not the edges.

That isn't a knock on the platform. It's the ceiling of bolting *any* framework onto a
surface that was never built to host it.

Full functional parity isn't something we can reach from the outside. It lives in the native
build — **gald3r_agent**, running on the **gald3r throne** over the **gald3r_world_tree** —
where commands, rules, agents, skills, and hooks aren't *adapted* to the platform, they *are*
the platform.

> ### gald3r_agent — coming soon. 🌳

---

<sub>Capabilities verified against the platform's official documentation on 2026-06-02, and
re-verified each release via the gald3r platform-docs crawl. This report describes gald3r's
third-party adaptation surface; it is not an endorsement or critique of the platform itself.</sub>
