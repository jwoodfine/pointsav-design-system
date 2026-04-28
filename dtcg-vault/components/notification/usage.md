# When to use Notification

Use a notification to surface system feedback after an action or
state change. Four variants — informational, positive, caution,
critical — communicate severity by colour AND icon AND framing.

| Variant | Use for |
|---|---|
| **Info** | Neutral context — "Your draft has been saved automatically." |
| **Positive** | Successful outcome — "Report exported." |
| **Caution** | Reversible problem — "Cannot connect to the network. Reconnecting…" |
| **Critical** | Failed action — "Could not save changes. Try again." |

Notifications never auto-dismiss without an undo affordance.
Time-sensitive critical notifications use `role="alert"` for
assertive announcement.

The substrate ships inline notifications today; toast (positioned)
notifications are subsequent-milestone work — most production
patterns use inline + a single toast slot at the page level.
