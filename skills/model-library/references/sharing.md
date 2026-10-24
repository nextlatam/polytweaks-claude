# Sharing and feedback

Resolve the intended saved `assetVersionId` and use the current tool schema. Opening a private model and granting public access are separate actions.

| Request | Tool | Result |
| --- | --- | --- |
| Open my saved model | `get_model` | Private `viewerUrl`, requiring existing Polytweaks access |
| Share for viewing | `create_share_link` | `shareUrl`, view-only by default |
| Invite review comments | `create_feedback_link` | `feedbackUrl`, enabling comments and editing one's own comments |
| Share in AR | `create_ar_link` | Separate expiring public `arUrl` and QR result |
| Read feedback | `list_comments` | Comments on the selected version |
| Post text or a reply | `add_comment` | Confirmed comment; `parentId` only for a real reply target |

Viewer/review shares default to anyone-with-link access and seven-day expiry. Both allow supported-device AR, never model editing. Downloads are independent and off by default; set `allowDownloads: true` only when the user requests download/export access. Review requests do not imply downloads.

Use `includeQr: true` for a requested QR of the same viewer/review URL. It does not create another share. Explicit `expiresAt` values are Unix milliseconds within the next 30 days. Report the returned `expiresAtIso`; do not calculate expiry from an assumed current time.

For requested password protection, use the user's chosen password and ask only if it is missing. Do not invent or echo the password. A protected guest enters a name and password. Anyone-with-link access is not private. An account-only request should use the existing private `viewerUrl`.

AR supports `duration` values `5m`, `1h`, `24h`, `7d` and `30d`, defaulting to `24h`. The returned link grants access to anyone holding it until expiry. Show the actual URL and returned QR when available without claiming an embedded viewer opened. The tool does not convert files; keep missing authored-USDZ warnings explicit for iOS.

Creating a link does not authorize sending it through email, Slack or another service. An AR request does not authorize creating a feedback link. Use the permissions and expiry actually returned by the tool.

`add_comment` supports text and replies. Comment editing, deletion, resolution and new 3D annotation placement are not exposed here. Use the normal viewer for those actions. Do not call a new comment a resolution or invent spatial coordinates. Reading feedback does not authorize posting a summary.

Each requested write has its own stable operation key. Retain the original key and inputs for an uncertain retry; no fresh key merely because the response was lost.
