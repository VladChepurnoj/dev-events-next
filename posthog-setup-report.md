<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the DevEvent Next.js App Router application. The following changes were made:

- **`instrumentation-client.ts`** (new file): Initializes PostHog client-side using the Next.js 15.3+ recommended approach. Configured with EU host, reverse proxy ingestion path, exception capture, and debug mode for development.
- **`next.config.ts`**: Added reverse proxy rewrites so PostHog events are routed through `/ingest/*` on the same domain, reducing the chance of being blocked by ad blockers. Also set `skipTrailingSlashRedirect: true` as required by PostHog.
- **`components/ExploreBtn.tsx`**: Added `posthog.capture('explore_events_clicked')` to the existing button click handler.
- **`components/EventCard.tsx`**: Converted to a client component (`'use client'`) and added `posthog.capture('event_card_clicked', { title, slug, location, date })` to the Link's `onClick` handler.
- **`.env.local`**: Created with `NEXT_PUBLIC_POSTHOG_KEY` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables (EU region).

| Event Name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the 'Explore events' CTA button on the homepage, indicating intent to browse featured events | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks on an event card to view event details, representing a key conversion funnel step | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard**: [Analytics basics](https://eu.posthog.com/project/136584/dashboard/555049)
- **Insight**: [Explore Events Clicks (Daily)](https://eu.posthog.com/project/136584/insights/xrAoySFc) — daily CTA button click count
- **Insight**: [Event Card Clicks (Daily)](https://eu.posthog.com/project/136584/insights/ejKg3W6K) — daily event card click count
- **Insight**: [Explore to Event Click Funnel](https://eu.posthog.com/project/136584/insights/v4Azq3Ui) — conversion funnel from CTA to event card click
- **Insight**: [Most Clicked Events (by slug)](https://eu.posthog.com/project/136584/insights/f0CtMsA2) — which events attract the most clicks
- **Insight**: [Weekly Active Users (Explore & Click)](https://eu.posthog.com/project/136584/insights/QllyyE8d) — weekly unique users engaging with events

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
