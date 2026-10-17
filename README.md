# Automated News Digest Pipeline (Make.com)

![Workflow architecture](architecture.png)

End-to-end automation that extracts articles from a public RSS feed, transforms them into concise summaries with a generative-AI model, and loads the result into a formatted email — built visually on the Make platform, no hand-written code.

## Architecture Overview

Classic ETL pattern, three modules chained:

| Stage | Module | Responsibility |
| :---- | :----- | :------------- |
| Extract | `RSS Watcher` | Polls the TechCrunch AI feed on a schedule and emits each new item as a bundle. |
| Transform | `Make AI Toolkit` (Summarize Text) | Takes the item's `Description` and produces a short summary using the lightweight "Small" model. |
| Load | `Gmail` (Send an Email) | Renders an HTML body from the mapped variables and delivers it to the recipient inbox. |

## Data Mapping

The value of this scenario is the variable wiring between modules, not the modules themselves:

- Gmail **Subject** ← `RSS.Title`
- Gmail **Body** ← `RSS.Title`, `AI Toolkit.Summary`, `RSS.URL` (injected into an HTML template)
- AI Toolkit **Text to summarize** ← `RSS.Description`

Each `{n.field}` placeholder is a live reference resolved at runtime, so the email always reflects the article that triggered the run.

## Troubleshooting Log

**HTTP 403 — insufficient authentication scopes.** On the first send attempt the Gmail module failed even though the connection looked "Verified". Root cause: the initial OAuth consent had granted read/manage scopes but not the *send-on-your-behalf* scope. Fix: recreate the Gmail connection and, on the Google consent screen, confirm the "Send email on your behalf" permission is checked before continuing. After re-authorization the send succeeded.

**Empty run / no email received.** A first execution finished in under a second with status *Success* but delivered nothing, because the RSS trigger was set to *From now on* and there were no items newer than the moment of creation. Switching the trigger to *Select the first RSS feed item* forced it to process the latest existing article and produced a real payload. This is the difference between a green checkmark and an actually working pipeline.

## Output Evidence

![Delivered digest email](output-email.png)

Real message received in the inbox: headline pulled from the feed, AI-generated summary in the body, and a working button linking back to the source article.

## How To Replicate

1. Create a free account at https://www.make.com.
2. New scenario → add **RSS / Watch RSS feed items**, URL `https://techcrunch.com/category/artificial-intelligence/feed/`, start point *Select the first RSS feed item*, max items `3`.
3. Add **Make AI Toolkit / Summarize Text**, model *Small*, map *Text to summarize* to the RSS `Description` field.
4. Add **Gmail / Send an Email**, authorize the connection making sure the *send* scope is granted, set *To* to your address, *Body type* to *Raw HTML*, and map Subject/Body to the RSS and AI Toolkit variables as shown above.
5. Save, click **Run once**, and verify the email arrives. Toggle the scenario to *Active* for scheduled runs.

---

*Built as a portfolio artifact demonstrating low-code orchestration, dynamic variable mapping, OAuth scope debugging, and ETL design.*
