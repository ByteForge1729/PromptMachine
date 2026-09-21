# Share links

**Tier:** v0 (question sets and plans) · v1 (personal AI questions) · **Sources:** D5, D11, A16, A35

## Behaviour
1. A student can share a topic's question set or their plan by link.
2. Anyone with the link can open it without an account.
3. Links use long random tokens, are excluded from search engines, show a clean preview in
   WhatsApp, and hide the owner's name unless they opt in.
4. The owner can revoke a link.

## Acceptance criteria
- [ ] Given a revoked link, then it shows "This link was turned off".
- [ ] Given a shared page, then search engines are told not to index it.
