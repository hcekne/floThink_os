---
type: flothink-workflow
name: Company Research Custom Prompt
version: 4
trigger:
  position:
    x: -70
    y: 200
  type: manual
  params:
  - name: Company
    type: string
    required: true
  - name: Sector
    type: string
    required: true
  - name: Industry
    type: string
    required: true
  - name: FinalPrompt
    type: string
    required: true
status: draft
contract:
  output:
    name: research_brief
    type: file
    format: md
    source: step_33
    description: Research brief answering the supplied final prompt.
  inputs:
  - name: Company
    type: string
    required: true
  - name: Sector
    type: string
    required: true
  - name: Industry
    type: string
    required: true
  - name: FinalPrompt
    type: string
    required: true
    description: Complete instructions and relevant context for the final research brief. Paste the prompt
      text, not a file path.
  provider_policy: byo
steps:
- id: step_23
  name: Industry research
  provider: codex_remote
  model: ''
  thinking: medium
  prompt: Research the industry in which {Company} operates. Summarise the market size and growth, key
    trends and disruptions, major competitors, customer segments, value chain, business models, regulatory
    environment, and key risks and opportunities. Focus especially on developments that could materially
    affect {Company} over the next 3–5 years, and support important claims with credible sources.
  inputs:
  - trigger
  output:
    as: text
  position:
    x: 362
    y: -49
- id: step_24
  name: Company Research
  provider: codex_remote
  model: ''
  thinking: medium
  prompt: 'Research {Company}. Summarise its business model, products and services, customer segments,
    geographic footprint, ownership and leadership, financial performance, competitive positioning, strategy,
    recent developments, and key risks and opportunities. Highlight the most important factors shaping
    the company’s performance and outlook over the next 3–5 years, and support important claims with credible
    sources.

    '
  inputs:
  - trigger
  output:
    as: text
  position:
    x: 360
    y: 238
- id: step_25
  name: Sector Research
  provider: codex_remote
  model: ''
  thinking: medium
  prompt: 'Research the {Sector} in which {Company} operates. Summarise the sector structure, size and
    growth, key segments, major players, customer groups, value chain, important trends and disruptions,
    regulatory environment, and key risks and opportunities. Focus especially on developments that could
    materially affect {Company} over the next 3–5 years, and support important claims with credible sources.

    '
  inputs:
  - trigger
  output:
    as: text
  position:
    x: 360
    y: 98
- id: step_26
  name: AI and Data Research
  provider: codex_remote
  model: ''
  thinking: medium
  prompt: 'Research the most important AI and data topics relevant to the {Industry}. Summarise how companies
    are using AI, machine learning, automation and data today, the highest-value use cases, emerging trends,
    leading adopters and vendors, common technology and data challenges, regulatory considerations, and
    areas of future opportunity. Focus on developments likely to materially affect the industry over the
    next 3–5 years, and support important claims with credible sources. '
  inputs:
  - trigger
  output:
    as: text
  position:
    x: 359
    y: 382
- id: step_29
  name: Summarise and Combine
  provider: codex_remote
  model: ''
  thinking: high
  prompt: Combine the outputs from the previous research steps into one coherent and logically consistent
    narrative about {Company}. Integrate the company, sector, industry, and AI & data research, removing
    duplication and resolving overlaps or inconsistencies. Structure the synthesis around the most important
    themes, clearly connecting the external market context to {Company}'s business model, competitive
    position, strategy, risks, opportunities, and potential implications of AI and data. Prioritise the
    most decision-relevant insights rather than simply summarising each input separately.
  inputs:
  - step_23
  - step_25
  - step_24
  - step_26
  output:
    as: text
  position:
    x: 741
    y: 141
- id: step_30
  name: Claude POV
  provider: claude_code
  model: ''
  thinking: xhigh
  prompt: 'Based on the summarised view of {Company}, develop a clear and distinctive strategic point
    of view on what the company should do to grow and win over the next 3–5 years.


    The POV must be sharp enough to crystallise into **one compelling headline sentence** that captures
    the core strategic idea, supported by a **clear descriptive paragraph** explaining the rationale and
    implications.


    Identify the most attractive growth opportunities, strategic priorities, capabilities to build, areas
    to invest in or deprioritise, and key risks to address. Make clear the choices and trade-offs involved,
    and translate the analysis into a focused set of actionable recommendations that could strengthen
    {Company}''s competitive position and long-term performance.


    Avoid generic strategy statements. The POV should be specific to {Company}, differentiated, evidence-based,
    and strong enough to guide strategic decision-making.

    '
  inputs:
  - step_29
  output:
    as: text
  position:
    x: 1085
    y: 64
- id: step_31
  name: Codex POV
  provider: codex_remote
  model: ''
  thinking: xhigh
  prompt: 'Based on the summarised view of {Company}, develop a clear and distinctive strategic point
    of view on what the company should do to grow and win over the next 3–5 years.


    The POV must be sharp enough to crystallise into **one compelling headline sentence** that captures
    the core strategic idea, supported by a **clear descriptive paragraph** explaining the rationale and
    implications.


    Identify the most attractive growth opportunities, strategic priorities, capabilities to build, areas
    to invest in or deprioritise, and key risks to address. Make clear the choices and trade-offs involved,
    and translate the analysis into a focused set of actionable recommendations that could strengthen
    {Company}''s competitive position and long-term performance.


    Avoid generic strategy statements. The POV should be specific to {Company}, differentiated, evidence-based,
    and strong enough to guide strategic decision-making.

    '
  inputs:
  - step_29
  output:
    as: text
  position:
    x: 1077
    y: 192
- id: step_32
  name: Aggregate POV
  provider: codex_remote
  model: ''
  thinking: xhigh
  prompt: 'Review the alternative strategic points of view for {Company} and determine the strongest overall
    POV. Evaluate each based on strategic relevance, distinctiveness, evidence, internal logic, growth
    potential, feasibility, and ability to create sustainable competitive advantage over the next 3–5
    years.


    Do not simply select one by default. Where the strongest answer combines complementary elements from
    multiple POVs, merge them into a single coherent and logically consistent strategic point of view.
    Resolve contradictions, remove duplication, and avoid combining ideas that create an unfocused or
    internally inconsistent strategy.


    The final POV must be specific to {Company}, make clear strategic choices and trade-offs, and be sharp
    enough to crystallise into **one compelling headline sentence** that captures the central strategic
    idea. Support this with a **clear descriptive paragraph** explaining why this is the strongest direction,
    the key growth opportunities it targets, the priorities and capabilities required, what {Company}
    should invest in or deprioritise, and the main risks or execution challenges.


    Prioritise a strong, distinctive and actionable point of view over a broad collection of recommendations.

    '
  inputs:
  - step_30
  - step_31
  output:
    as: text
  position:
    x: 1380
    y: 113
- id: step_33
  name: Custom Final Brief
  provider: codex_remote
  model: ''
  thinking: high
  prompt: '{FinalPrompt}'
  inputs:
  - step_32
  - step_29
  - trigger
  output:
    as: file
    format: md
    filename: '{Company}_AI_research_brief'
  position:
    x: 1700
    y: 328
edge_routes:
- source: step_29
  target: step_33
  waypoints:
  - x: 1068.4
    y: 372.5
  routing: smooth
- source: trigger
  target: step_33
  waypoints:
  - x: 355.9
    y: 565.3
  - x: 895.7
    y: 556.7
  - x: 1290
    y: 496.4
  routing: smooth
catalog:
  id: maxos.company-research-custom-prompt
  name: Company Research Custom Prompt
  industries:
  - consulting
  - e-commerce
  job_group: research-strategy
  job_group_label: Research & strategy
  outcome: Research a company and answer your own final strategic question
  input_summary: Company, sector, industry, and your complete final prompt
  output_summary: A cited Markdown research brief tailored to your final prompt
  source: maxos
  publisher: floThink
  version: 1.0.0
---

# Company Research Custom Prompt

## Goal
Research a company and its market, then produce a decision-focused brief answering your own final prompt.

## Setup
In Workflow Builder, use Node table to choose your Codex and Claude connections and models. This portable template includes no account credentials, private documents, or preselected models.

## Inputs
- **Company**: the company to research.
- **Sector**: its sector.
- **Industry**: its industry.
- **FinalPrompt**: the full instructions for the final brief, including objective, relevant context, evidence standards, and output requirements. Paste prompt text; a file path alone does not attach a document.

## Steps
Four parallel research branches cover the company, industry, sector, and AI/data context. A synthesis feeds two strategic points of view, which are combined into an aggregate POV. The final brief consumes the synthesis, aggregate POV, and runtime inputs. Its prompt is exactly `{FinalPrompt}`.

## Outputs
A Markdown file named `{Company}_AI_research_brief`, exposed as `research_brief`.

## Quality checklist
- Supply all four inputs and a non-empty FinalPrompt.
- Distinguish company-specific evidence, parent-group information, and inference.
- Check citations, material gaps, and recommendations before sharing externally.
- The custom prompt changes only the final node; earlier research remains general.
- Run only after choosing connections and reviewing any private context you supply.
