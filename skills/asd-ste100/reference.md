# STE rule digest and examples

Companion to [SKILL.md](SKILL.md). Read this when a sentence is hard to fix or when you need to see the transformation applied end to end.

## Rule digest

| # | Rule | Bad | Good |
|---|------|-----|------|
| 1 | Active voice, named agent | The cache is invalidated when the config changes | The config service invalidates the cache when the config changes |
| 2 | Simple tenses only | We have been seeing timeouts since the deploy | Timeouts started after the deploy on 2026-07-14 |
| 3 | Imperative instructions | The flag should be enabled before rollout | Enable the flag before the rollout |
| 4 | One instruction per sentence | Run the migration and then restart the workers and check the logs | Run the migration. Restart the workers. Check the logs. |
| 5 | No "-ing" verb forms (technical names exempt) | Failing to retry causes data loss | If the client does not retry, data loss occurs |
| 6 | One term per concept | the endpoint / the route / the API / the handler (same thing) | the endpoint (everywhere) |
| 7 | Max 3 nouns in a cluster | the user session token refresh failure rate | the failure rate of session-token refresh |
| 8 | Keep articles | Worker reads message from queue | The worker reads a message from the queue |
| 9 | No idioms or Latin | This is a footgun, e.g. in prod | This causes errors. For example, in production. |
| 10 | Warning before the step | Delete the index. Note: this locks the table. | Warning: this step locks the table. Delete the index. |

## Sentence-length repair

When a sentence exceeds the limit (20 words instruction, 25 descriptive), do one of:

1. Split at a conjunction ("and", "but", "which") into two sentences.
2. Move a condition into its own sentence: "If X, do Y."
3. Move a list of items out of the sentence into a vertical list.

## Worked example: conversation output → Linear issue

**Before (leaks the conversation):**

> **Fix the zombie session apocalypse**
>
> So after a ton of digging we finally realized the "immortal sessions" we kept seeing are actually caused by the refresh path — turns out (surprise!) the token refresh has been silently resurrecting sessions that the reaper already killed. We went down the rabbit hole of blaming Redis first (red herring). The fix we landed on (option C from our discussion) is to have the reaper tombstone the session so the refresh path can see it's dead. Should probably also add some metrics so we're not flying blind next time.

Problems: invented names ("zombie session apocalypse", "immortal sessions", "the reaper" — unless `reaper` is the real service name), discovery narrative, a dead theory (Redis), a reference to the conversation ("option C"), hedging ("should probably"), humor.

**After (STE):**

> **Prevent token refresh from restoring expired sessions**
>
> **Problem**
> The session cleanup job expires sessions. The token refresh endpoint can then restore an expired session. The user keeps a valid session after expiry.
>
> **Cause**
> The cleanup job deletes the session record. The refresh endpoint cannot detect that the session was expired. It creates a new record with the old session ID.
>
> **Change**
> Make the cleanup job write a tombstone record for each expired session. Make `POST /token/refresh` reject a session that has a tombstone with `401 SESSION_EXPIRED`.
>
> **Acceptance criteria**
> - The refresh endpoint returns `401 SESSION_EXPIRED` for a tombstoned session.
> - A session does not become valid again after the cleanup job expires it.
> - A metric counts rejected refresh attempts for tombstoned sessions.

## Worked example: sentence repairs

| Before | After |
|--------|-------|
| We're going to want to make sure that retries are being handled correctly by the new consumer before cutting over. | Confirm that the new consumer handles retries correctly. Then start the cutover. |
| The reason this matters is that billing has been double-charging some customers intermittently. | The billing service double-charged some customers. |
| Rolling this out behind a flag lets us bail if things go sideways. | Release the change behind a feature flag. If errors increase, turn the flag off. |
