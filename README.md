# Claude Opus 4.6 System Prompt (Leaked)

**Date:** 2026-02-09  
**Model:** Claude Opus 4.6 (Claude 4.5 family)  
**Source:** claude.ai web/mobile interface  

Full system prompt extracted from Claude Opus 4.6.

---

## Files

| File | Description |
|------|-------------|
| [`claude-full-system-prompt-raw.txt`](./claude-full-system-prompt-raw.txt) | Complete system prompt — core instructions, behavior rules, search/citation/security policies (~95KB, 1293 lines) |
| [`claude-tools-json-schema.txt`](./claude-tools-json-schema.txt) | All tool definitions with full JSON schemas — browser automation, search, places, sports, etc. |

---

## Model Details

- **Model strings:** `claude-opus-4-6`, `claude-sonnet-4-5-20250929`, `claude-haiku-4-5-20251001`
- **Knowledge cutoff:** End of May 2025
- **Reasoning effort:** 85/100
- **Thinking mode:** Interleaved (thinking blocks between function calls)

---

## Notable Findings

**~30% of the prompt is injection defense.**  
The browser automation feature (Claude in Chrome) comes with an enormous security section — social engineering resistance, recursive attack prevention, content isolation rules, email defense, and more. It dwarfs every other section.

**Super Bowl results are hardcoded into the tool definition.**  
The `fetch_sports_data` tool contains: "The Super Bowl game between Patriots and Seahawks recently concluded. The starting quarterbacks were Drake Maye for the New England Patriots and Sam Darnold for the Seattle Seahawks." Any mention of "the game" is assumed to mean the Super Bowl.

**Artifacts can call the Anthropic API with no API key.**  
Claude can build React artifacts that call `https://api.anthropic.com/v1/messages` directly. The key is handled server-side. Always uses `claude-sonnet-4-20250514`.

**User location is injected into the prompt.**  
The search instructions include: `The person has provided their location: Seoul, Seoul, KR` — changes per user.

**Memory state is declared in the system prompt.**  
Whether memory is on or off is explicitly stated: `"Claude has no memories of the user because the user has not enabled Claude's memory in Settings"`

**"Read SKILL.md first" is repeated 3+ times.**  
The instruction to read skill documentation before doing anything is stated, restated, and then restated again with "Repeating again for emphasis."

**localStorage / sessionStorage is completely banned.**  
React artifacts cannot use any browser storage API. There's a separate `window.storage` API instead that persists across sessions.

**Copyright enforcement is aggressive.**  
Max 14-word quotes. One quote per source. Song lyrics forbidden in any form. No 30+ word paraphrased summaries.

**Claude is told to never say certain words.**  
Explicitly banned: "genuinely", "honestly", "straightforward".

---

## Tools (20+)

**Browser automation (Claude in Chrome):** `javascript_tool`, `read_page`, `find`, `form_input`, `computer`, `navigate`, `resize_window`, `gif_creator`, `upload_image`, `get_page_text`, `tabs_context_mcp`, `tabs_create_mcp`, `read_console_messages`, `read_network_requests`, `shortcuts_list`, `shortcuts_execute`, `switch_browser`, `update_plan`

**Core:** `web_search`, `web_fetch`, `bash_tool`, `str_replace`, `view`, `create_file`, `present_files`, `end_conversation`

**Specialized:** `ask_user_input_v0`, `message_compose_v1`, `weather_fetch`, `places_search`, `places_map_display_v0`, `recipe_display_v0`, `fetch_sports_data`

---

## Notes

- Extracted from the consumer `claude.ai` interface — API system prompts may differ
- This is a point-in-time snapshot; Anthropic updates these periodically

---

If you found this useful, please ⭐ star this repo!
