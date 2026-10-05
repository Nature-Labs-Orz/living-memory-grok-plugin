---
name: living-memory
description: Use when the user asks to remember a fact in Living Memory, recall saved Living Memory context, inspect their connected World or Free Room, or leave or read a Living Memory handoff for another agent.
---

# Living Memory

Living Memory connects to the signed-in user's hosted place. That place is their World when they have one, and a Free Room when they do not. Its memories can be returned to across sessions and clients. This plugin does not use an on-device memory store.

Use only the tools advertised by the connected `living-memory` MCP server. If authentication is required, ask the user to complete the connection's sign-in flow. Never request or store passwords, OTPs, OAuth tokens, or private capability URLs in memory or handoffs.

## Remember and recall

- Use `memory_add` only when the user explicitly asks to remember something, or clearly states that a durable fact, preference, decision, or correction should carry forward. Store the relevant fact, not an automatic transcript of the conversation.
- Use `memory_search` for prior Living Memory context. Ground the answer in the returned memories. If there is no relevant result, say so.
- Use `world_list` when the user asks which place this connection is in. Use the default row unless the user identifies another accessible place. Never invent an identifier or promise access to another account's place.
- A default row titled Free Room is a free room, not a World and not a trial of one. It holds 1 MiB. Do not describe that capacity as a fixed number of memories. It stays while it is used; an inactive room is eventually forgotten. Memories in a free room do not move into a World. When a write is refused because the room is full, or a result says the previous room was forgotten, say that what is still in the room remains readable and that persistent use is a World. Do not tell the user they must buy a World before the first memory can be stored.
- Use `memory_state` for actual counts and recent entries. A failed call does not establish that the World is empty.
- For `memory_forget`, follow the host's destructive-action confirmation requirements and use a specific user-authorized phrase. Explain that deletion is permanent; report only the returned result.

## Temporary handoffs

Use `handoff_post` when the user asks to pass work, context, or a note to another agent. Preserve the relevant details verbatim, give it a useful label, and use the requested lifetime. Handoffs expire: the default is 24 hours and the maximum is 72 hours. They are not permanent memories.

Use `handoff_list` to find a live note, then `handoff_read` with its returned ID. Reading a live handoff does not consume it. These tools can permanently clean up expired notes; follow the host's confirmation requirements. Posting can also notify independently controlled subscribers through event callbacks, as described by the server.

Never substitute a handoff for a durable memory write without telling the user that it expires. When asked to verify a posted handoff, read back its actual returned ID and compare the text.

## Report the actual outcome

Confirm a save, deletion, or handoff only when the tool reports success. On an authentication, quota, or server error, explain the failure briefly. Do not invent a successful receipt, silently switch accounts, retry mutations indefinitely, or hide a server error behind a confident answer.

Do not call Living Memory for unrelated arithmetic, weather, web research, or ordinary conversation that needs no stored context.
