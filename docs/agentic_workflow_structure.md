# Agentic Workflow Structure

This project can keep the current Streamlit, API, and export code intact while the agentic layer is introduced around it.

## Current stable modules

- `Hosting/` for the Streamlit UI and user input handling
- `API/` for CMS data access and caching
- `FileExport/` for DOCX and PDF generation
- `Testing/` for unit tests

## New workflow scaffold

- `Models/` for Pydantic data contracts such as `FacilityData`, `FacilityAnalysis`, and `ValidationResult`
- `Workflow/` for LangGraph orchestration and routing logic
- `Agents/` for agent prompts, node logic, and tool wrappers
- `Validation/` for deterministic checks before and after agent execution

## Suggested flow

1. Streamlit collects CCN and manual inputs.
2. The data pipeline builds `FacilityData`.
3. Agent 1 produces `FacilityAnalysis`.
4. Deterministic validation checks schema, evidence, and numerical correctness.
5. Agent 2 critiques the evidence and validation results.
6. If approved, export to PDF and DOCX.
7. If rejected, revise and revalidate up to the retry limit.

## Why this shape works

- It keeps UI, data access, validation, and agent reasoning separate.
- It makes LangGraph a coordination layer instead of a dumping ground.
- It preserves the current tests while the workflow evolves.
