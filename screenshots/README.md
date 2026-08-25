# Screenshots

This folder holds dashboard and detection screenshots from the lab. Add images here as the lab environment is rebuilt, then reference them in the main [`README.md`](../README.md) like:

```markdown
![Attack Frequency Dashboard](screenshots/attack-frequency-dashboard.png)
```

## Screenshots Needed (checklist)

- [ ] `attack-frequency-dashboard.png` — line chart of failed-auth events over time
- [ ] `top-source-ips-dashboard.png` — ranked bar chart of top attacking IPs
- [ ] `auth-failure-heatmap.png` — heatmap of failure concentration by hour/day
- [ ] `brute-force-detection-results.png` — output table of the brute-force SPL query with flagged IPs
- [ ] `splunk-index-config.png` — (optional) shows the data onboarding/index setup, useful for demonstrating pipeline setup skill

## Tips for Good Portfolio Screenshots

- Use realistic-looking synthetic IPs and usernames — never real production data or personal credentials
- Crop tightly to the relevant panel; avoid capturing unrelated browser tabs or desktop clutter
- Take screenshots at a moment when the dashboard actually shows attack activity (not an empty/flat graph) — it should visually tell the story of "here's what an attack looks like when caught"
