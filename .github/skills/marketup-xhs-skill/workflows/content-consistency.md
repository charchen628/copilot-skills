# Content Consistency

Use this workflow before writing titles, body copy, carousel pages, or image plans; run it again after drafting and before validation. Its purpose is to keep one explainable line from audience to business problem, promise, method, product connection, and CTA.

Read `schemas/content-spine-fields.md`, `workflows/task-routing.md`, `workflows/validation-repair.md`, the active Profile, and current-task material rules.

## Establish the content spine

Create these fields before production:

```text
audience
→ business_problem
→ topic
→ promised_takeaway
→ product_connection
→ cta
```

Use the user's current request and current-task materials to establish the spine. The active Profile validates product facts, gives default audience and style boundaries, and sets compliance limits; it must not silently choose the topic.

If topic, audience, or deliverable is unclear, return to `workflows/task-routing.md`. Do not use keywords, reference samples, or product capabilities to decide it for the user.

## Consistency checks

Check in this order:

1. The title and cover promise the business problem that the body or carousel actually answers. A numbered promise such as “3 steps” must have the same supported number of methods or pages; otherwise add supported steps, correct the promise, or ask for confirmation.
2. The body, carousel sequence, and CTA continue the same business problem rather than switching topics.
3. Every method, paragraph, and page advances the promised takeaway; off-topic functionality is removed or compressed.
4. Product capability appears as a natural way to execute the method, not as a sudden product list.
5. Audience language, scene, example, and CTA match the stated audience.
6. The CTA is the natural next step from the conclusion, not an unrelated hard sell.
7. Carousel pages collectively advance one line; each page has a role in the same problem-to-solution path.
8. Remove each product-connection section in turn. The topic must still make sense without it; if it does not, check whether the capability has displaced the topic or whether the topic itself needs confirmation.

Record failures under `schemas/validation-issue-fields.md` and send them to `workflows/validation-repair.md`.

## Failure handling

Use the validation-repair workflow.

### AUTO_FIX

- align mildly inconsistent title, cover, CTA, page role, or wording with the existing spine;
- correct a numbered title or cover promise when the draft does not provide the promised number of supported methods or pages;
- delete or compress a disconnected product paragraph, feature list, or page;
- repair an individual carousel page that does not serve the spine.

Recheck the entire spine after every repair.

### CONFIRM

- the user topic and required capability cannot form one coherent path;
- multiple unrelated topics are required at once;
- audience, CTA, or deliverable conflict;

### BLOCK

- the core article depends on an unapproved product capability;
- no explainable business spine exists and the user does not confirm a new direction.

Do not invent a new topic to escape a blocked or unconfirmed spine.
