---
description: Generate QA test cases from a story, file, or feature description via QAEverest
argument-hint: [story text, a file path, or a feature description]
---

Generate QA test cases with QAEverest for: **$ARGUMENTS**

Steps:
1. If `$ARGUMENTS` names a file in the repo, read it and use its contents as the source story. Otherwise treat `$ARGUMENTS` as the story/feature description directly. If it's empty, ask the user what to generate tests for.
2. Choose the right QAEverest tool:
   - Plain functional/system requirement → `generate_testcases`
   - An OpenAPI/Swagger spec or Postman collection, or an API description → `generate_api_tests`
   - An end-to-end browser UI flow → `generate_ui_tests`
   - A mobile app flow → `generate_mobile_tests`
3. Pass `domain_name` / `module_name` when they're obvious from context, and put any focus areas or constraints in `additional`.
4. Present the returned Gherkin scenarios. Offer to save them to a `.feature` file or scaffold automation from them.

Note: each generation call consumes QAEverest credits. Run `/qaeverest:usage` first if the user wants to check their balance.
