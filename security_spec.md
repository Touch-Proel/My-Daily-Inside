# Security Specification: My Daily Insight

## Data Invariants
1. **Posts**: Must have a unique slug, valid category from the allowed set, and complete metadata.
2. **Messages**: Anyone can send a message, but they cannot read or modify any message once sent.
3. **Categories**: Read-only for the public, updateable only by admins.

## The Dirty Dozen Payloads (Target: DENIED)

1. **Anonymous Post Update**: Attempt to update a post's content without authentication.
2. **Post Spoofing**: Attempt to create a post with a fake `authorId` or current user.
3. **Message Scraping**: Attempt to list/read the `/messages` collection as a guest.
4. **Message Modification**: Attempt to update an existing contact message.
5. **Category Injection**: Attempt to create a new category via the client.
6. **Post Deletion**: Attempt to delete a post as an authenticated (non-admin) user.
7. **Invalid Category**: Attempt to create/update a post with a category not in the enum.
8. **Resource Poisoning**: Use a 1MB string for a `slug`.
9. **Identity Spoofing**: Setting `author` field to another user's name during post creation.
10. **Bypassing Validation**: Sending a post without a `required` field like `publishedAt`.
11. **Direct Message ID Guessing**: Attempting to `get` a specific message by its ID.
12. **Spamming Messages**: Multiple high-frequencywrites to messages (rate limiting is hard in rules, but size checks help).

## Test Runner (firestore.rules.test.ts)
I will implement tests to verify these scenarios.
