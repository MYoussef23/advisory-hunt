# Advisory Hunt Agent for Claude

## Install and run once

Use **Plugins → + Add → Upload plugin** and select the downloaded ZIP as it is. Open a new Cowork task and type **Hunt this advisory: [URL]**. To select the workflow explicitly, type **/**, find **Advisory Hunt Agent → hunt**, and supply the URL or CVE. The qualified command is **/advisory-hunt:hunt**. No project upload is required. The plugin uses Claude's existing web research and document capabilities. It does not require Ollama, an API key or a SIEM connection.

The result is a downloadable Word hunt guide for Microsoft Sentinel, Sumo Logic, Cortex XDR and Splunk. A run researches primary sources, identifies affected builds, writes hunting queries and detection rules, states what was validated, and gives analysts triage and remediation guidance. Provide approved schemas or redacted samples if you want tenant-specific mappings.

## Choose a model once

For full hunts, the recommended combination is **Claude Opus 5.5, High effort**. Use **Sonnet 5.5** for routine revisions or as a full-hunt alternative. **Haiku 5.5** suits extracting fields from bulletins. **Fable 5.2** is an optional second review of a difficult evidence conflict if your role and quota allow it. Model guidance checked 19 November 2026.

The workspace and task settings supply the active model. To choose the model for a repeating job, go to **Cowork → Scheduled → New task → Set up manually** and select the model there. Enterprise admins can set the default model and effort for a SOC custom role under **Organization settings → Roles → [SOC role] → Models**. If needed, use **Always start with the default model and effort level** for that role. Granting the role, selecting the model and enabling tools are separate workspace controls.

## Optional unattended hunt

Create a scheduled task only after deciding which official source to watch, how often to run, and where its reports and completion register should live. Choose an approved location accessible to each scheduled run. Configure web search and file creation as permitted by your workspace, then run the task on demand once to check that it can read the feed, save a Word file and find its own register on the next run.

Copy the following into the scheduled task, replacing the bracketed values.

> Review [official advisory feed URL] for new or updated advisories matching [products or inclusion criteria]. Use the installed Advisory Hunt Agent workflow for each match. On first run, start at [explicit start date and time zone]. For later runs, check the last successful interval with an overlap of one feed publication cycle. In [approved persistent output location], key completed reports by canonical advisory ID and vendor revision or last-modified date. Skip a revision only when its completed report is present. Save each Word guide before marking that revision complete. Preserve failures for retry. If this is a subsequent run and the completion register is unavailable, report the gap. Report zero matching updates only after successfully reading the feed.

Installation alone does not start a scheduled task or change a model, connect to a SIEM, or enable production detections.

## Anthropic references

- [Install and invoke plugins](https://claude.com/docs/plugins/overview)
- [Set a default model or effort by role](https://support.claude.com/en/articles/15330088-set-a-default-model-for-your-organization)
- [Schedule a Cowork task and select its model](https://support.claude.com/en/articles/13854387-schedule-recurring-tasks-in-claude-cowork)
- [Model and effort controls](https://support.claude.com/en/articles/8664678-change-the-model-effort-and-thinking-settings)
- [Web search](https://support.claude.com/en/articles/10684626-enable-and-use-web-search) and [Word file creation](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude)
