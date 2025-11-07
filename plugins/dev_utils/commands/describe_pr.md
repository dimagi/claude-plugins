---
description: Generate comprehensive PR descriptions following repository templates
allowed-tools: Bash(gh pr view:*), Bash(gh pr diff:*), Bash(gh pr list:*), Bash(gh pr checks:*)
argument-hint: [PR number]
---

# Generate PR Description

You are tasked with generating a comprehensive pull request description following the repository's standard template.

**Usage**: /describe_pr $1

## If no PR number is provided, identify the PR to describe
- Check if the current branch has an associated PR: `gh pr view --json url,number,title,state 2>/dev/null`
- If no PR exists for the current branch, or if on main/master, list open PRs: `gh pr list --limit 10 --json number,title,headRefName,author`
- Ask the user which PR they want to describe

## Steps to follow:

1. **Read the PR description template:**
   - Read the template at `.github/pull_request_template.md` carefully to understand all sections and requirements

2. **Gather comprehensive PR information:**
   - Get the full PR diff: `gh pr diff {number}`
   - If you get an error about no default remote repository, instruct the user to run `gh repo set-default` and select the appropriate repository
   - Get commit history: `gh pr view {number} --json commits`
   - Review the base branch: `gh pr view {number} --json baseRefName`
   - Get PR metadata: `gh pr view {number} --json url,title,number,state`

3. **Analyze the changes thoroughly:** (ultrathink about the code changes, their architectural implications, and potential impacts)
   - Read through the entire diff carefully
   - For context, read any files that are referenced but not shown in the diff
   - Understand the purpose and impact of each change
   - Identify user-facing changes vs internal implementation details
   - Look for breaking changes or migration requirements

4. **Generate the description:**
   - Fill out each section from the template thoroughly:
     - Answer each question/section based on your analysis
     - Be specific about problems solved and changes made
     - Focus on user impact where relevant
     - Include technical details in appropriate sections
     - Write a concise changelog entry
   - Ensure all checklist items are addressed (checked or explained)

5. **Save the description:**
   - Write the completed description to `{number}_description.md` (DO NOT COMMIT THIS FILE)
   - Show the user the generated description

6. **Update the PR:**
   - Update the PR description directly: `gh pr edit {number} --body-file {number}_description.md`
     - This requires the 'project' GitHub scope. If the command fails you can check the scope with `gh auth status`.

## Important notes:
- Be thorough but concise - descriptions should be scannable
- Focus on the "why" as much as the "what"
- Include any breaking changes or migration notes prominently
- If the PR touches multiple components, organize the description accordingly
- Always attempt to run verification commands when possible
- Clearly communicate which verification steps need manual testing
