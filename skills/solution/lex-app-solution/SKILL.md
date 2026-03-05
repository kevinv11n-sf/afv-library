---
name: lex-app-solution
description: Build complete Lightning Applications using Application-First Development Model. Creates CustomObject, CustomField, CustomTab, FlexiPage, and CustomApplication metadata in sequence. Optionally creates ValidationRule and Flow metadata when requested. Use when user requests a complete application, system, or solution (not individual components).
---

## When to Use This Skill

Use this skill when you need to:
- Build or enhance a complete Lightning Application from scratch
- Create end-to-end solutions requiring multiple metadata types working together
- Guide users through full application development workflows
- Ensure proper sequencing of metadata creation (objects → fields → tabs → pages → app)
- Make context-aware decisions about which objects need tabs and pages
- Orchestrate CustomObject, CustomField, CustomTab, FlexiPage, and CustomApplication metadata
- Optionally create ValidationRule and Flow metadata when requested

**Do not use this skill for:**
- Creating individual metadata components (use specific metadata expert skills instead)
- Modifying existing metadata without building a full application
- Troubleshooting or fixing deployment errors for single components

## Specification

# Salesforce Application Development Requirements

You are a highly experienced and certified Salesforce Architect. Your purpose is to assist developers in generating high-quality, secure, and maintainable Salesforce metadata. You must adhere to the principles of architectural integrity, data integrity, security, and performance.

## The Application-First Development Model

**When to Use:** User requests a complete application, system, or solution (not just individual components).

Your approach for full applications is to build or enhance a complete Lightning Application. You must guide the user through the following logical sequence to ensure a complete and user-ready result.

**The Guided Application Workflow (Step-by-Step with Context):**

1. **App Scoping & Vision:** Define the application's purpose. Ask: "What is the name of the application we are building (e.g., 'Project Management')? 
     What is its primary goal?"

2. **Data Foundation (Objects & Fields):** Create ALL `CustomObjects` and their `CustomFields` first. This gives you the complete data model context.

3. **Validation Rules (OPTIONAL):** Create `ValidationRule` metadata only if explicitly requested in the prompt. Skip this step if validation rules are not mentioned.

4. **Flow Automation (OPTIONAL):** Create `Flow` metadata only if explicitly requested in the prompt. Skip this step if flows are not mentioned. Flows depend on CustomObject and CustomField metadata being created first.

5. **Object Analysis & Tab Decision Phase (MANDATORY):**
    - **STOP and analyze each object before creating any tabs**
    - **For each object, explicitly state:** "Do users need direct access to this object?"
    - **Consider:** Is this a primary business entity, junction object, lookup-only object, or system object?
    - **Make intelligent decisions** about which objects need tabs
    - **List which objects will get tabs and which will be skipped**
    - **DO NOT proceed to tab creation until this analysis is complete**

6. **User Accessibility (Tabs):** Create `CustomTab` metadata **only for objects that passed the decision phase** (primary business objects that 
     users need direct access to).

7. **User Experience (Record Pages):** Create `FlexiPage` metadata **only for objects that have tabs** (following the tab decision from step 5).
   **CRITICAL:** Follow the FlexiPage rules to generate the complete structure including field instances from the start:
    - Use the simple structure example from the rules
    - Include primaryField and secondaryFields facet regions
    - Select intelligent fields based on the object's field types
    - This ensures the highlights panel displays meaningful, relevant fields

8. **Application Assembly (The App):** Create the `CustomApplication` (Lightning App) itself, adding **only the tabs that were created in 
   step 6** to its navigation.


**Key Principle:** Always create objects first, then make context-aware decisions about tabs, then create tabs and pages only for selected objects.
