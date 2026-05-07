# SonarQube Agentic Analysis — VERIFY Directive

## After generating or modifying code

You must strictly follow this analyze-then-commit workflow for every code
modification. No code is considered complete until it has passed the following
SonarQube verification loop:

1. Read Phase: After any modification or before commit, use the `Read` tool
   to load the current state of all relevant source files.
2. Analysis Phase: For every new or modified file, call
   `run_advanced_code_analysis` with:
   - `projectKey`: The SonarQube Cloud project key
   - `branchName`: The active development branch
   - `filePath`: Project-relative path (e.g., `src/main/java/MyClass.java`)
   - `fileScope`: `MAIN` or `TEST` depending on the code type
3. Evaluation & Remediation:
   - Call `show_rule` for every issue
   - Mandatory fix any issue with `impacts[].severity` of HIGH or BLOCKER, or any issue with `impacts[].softwareQuality` of SECURITY
4. Verification: Re-run analysis after fixes to confirm resolution and
   no regressions
