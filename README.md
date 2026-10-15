# Pocket Stats: public files

- `index.html`: privacy policy (English and Italian), published with GitHub Pages.
- `ranked-rules.json`: Ranked point rules read by the app at startup.

## How to edit `ranked-rules.json`

The app reads the file at startup. Outside every period listed in `rules`, it uses the standard rules built into the app:
10/13/16/19/22 points per win (streak 1 to 5+), -10 per loss, never below 810.

Each entry in `rules`:

| Field   | Meaning |
|---------|---------|
| `id`    | Free label (not used by the app). |
| `from`, `to` | First and last day of the period, `yyyy-MM-dd`, both included, phone's local time. |
| `win`   | Points for the 1st, 2nd, 3rd... win in a row. Beyond the last value, the last value applies. |
| `loss`  | Points lost per defeat (0 = no loss). |
| `floor` | Points never go below this value because of a loss. |
| `bands` | Optional. From `min` points upward, use these `win` / `loss` values instead (e.g. Master Ball). |

Limits checked by the app: `schema` must be 1; up to 50 periods; `win` 1 to 20 values between 0 and 200;
`loss` 0 to 100. If anything is invalid the whole file is ignored and the app keeps the last valid version.
JSON does not allow comments: check the file with a JSON validator before committing.
Changes reach the app within a few minutes (GitHub cache), at the next app start.
