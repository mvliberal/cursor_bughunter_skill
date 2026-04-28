README.md
Here’s a production-ready, Cursor-optimized version of your bug hunter skill. It’s structured as a system prompt + execution workflow designed for Cursor’s agentic mode, with explicit guardrails, phased analysis, and a standardized output template. You can paste this directly into .cursorrules, a Custom Agent prompt, or a skills/bug-hunter.md file.

🛠️ Cursor-Specific Tooling & Rules
    Use @codebase and file search to trace callers, not just diffs.
    Run terminal commands explicitly: git diff, grep -n, npm test -- --watch=false, etc.
    Respect Cursor's context limits: analyze in chunks if files > 500 lines.
    If using MCP tools (Slack, Jira, GitHub), append findings to the designated channel/ticket only after validation.
    Always prefix agent output with [BUG-HUNTER] for filtering.

🚀 How to Use in Cursor
    Save as .cursorrules or add to Custom Agents > Bug Hunter.
    Trigger with: Audit last 7 days of commits for critical correctness/security bugs. Fix if confidence ≥4. Follow workflow strictly.
    Cursor will execute phases sequentially, stop on uncertainty, and output the exact template above.
    Review the generated problem_fixed_details.md before approving.

💡 Pro Tips for Best Results
    Specify stack explicitly if Cursor isn't inferring correctly: Target: TypeScript/Node.js/PostgreSQL
    Pin context: Focus only on changes in /src/auth, /src/db, /src/workers
    Force dry-run first: Phase 1–3 only. Output findings. Do not modify code yet.
    Add monitoring hooks: Suggest adding structured logs or metrics around the fixed path in problem_fixed_details.md.