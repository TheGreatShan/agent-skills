---
name: pre-merge-check
description: Review code changes for clean code, correctness, security, and test readiness. Use this when reviewing a change, preparing a commit, validating whether a change is ready to be committed, or checking whether tests and formatting have been run.
license: MIT
---

# Pre-Commit Check

## Purpose
Help software engineers review code to a high standard before committing or merging changes.

Focus on clean code, correctness, security, and test readiness so that bugs and maintainability issues are caught early.

## Use this skill when
- reviewing a code change
- preparing a commit
- validating whether a change is ready to be committed
- checking whether tests and formatting have been run
- validating whether changes are ready to be merged into `main` or `master` through a pull request

## Review goals
Always focus on the following points during the review:

Use the `PM2-CleanCode-Handbuch.pdf` as a reference for all Java projects you are reviewing.

1. **Readability**
   - clear naming
   - small, focused methods
   - low nesting where possible
   - avoid unnecessary complexity

2. **Maintainability**
   - identify code duplication
   - check separation of concerns
   - prefer code that is easy to test
   - prefer understandable logic over overly complicated solutions
   - prefer well-known and proven libraries over custom code unless custom code is required

3. **Correctness**
   - check for obvious logic issues
   - verify proper error handling
   - check for consistent logging
   - consider edge cases
   - check consistency with existing patterns in the codebase

4. **Security**
   - check for security risks such as missing authentication validation, insecure defaults, hard-coded secrets, or unsafe input handling

5. **Testing**
   - verify the existing test cases
   - verify whether tests are still valid after the change
   - identify missing test coverage in critical code paths
   - highlight if coverage expectations are not met

## Required behavior
1. Review the changed files for clean code, correctness, and security issues.
2. Suggest concrete improvements where needed.
3. Run the relevant tests when possible.
4. If the repository uses .NET, run `dotnet test` to execute the tests and verify that they pass. If the repository uses Java run `gradle test` to execute the tests and verify that they pass.
5. If a repository quality gate script exists, prefer using that script.
6. Summarize whether the change appears ready to be committed or merged.

## Output format
Return your response in the following format:

1. Summary
2. Security threats
3. Findings
4. Suggested fixes
5. Tests / quality gate
6. Commit readiness
