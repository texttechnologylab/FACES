# The Project

**FACES: Feasibility, Acceptance, and Data Quality of New Multimodal Surveys**
{ .lead }

| | |
|---|---|
| **Funding** | Deutsche Forschungsgemeinschaft (DFG), project [539621548](https://gepris.dfg.de/gepris/projekt/539621548?language=en) |
| **Programme** | Infrastructure Priority Programme [SPP 2431 *New Data Spaces*](https://www.new-data-spaces.de/en-us/) |
| **Duration** | 1 October 2024 – 30 September 2027 |
| **Institutions** | [Text Technology Lab](https://www.texttechnologylab.org/), Goethe University Frankfurt · Departments 2 and 3, [LIfBi](https://www.lifbi.de/), Bamberg |

## Why

Survey methodology is caught between two pressures. Conventional face-to-face
interviewing produces rich, high-quality data but is increasingly expensive and
increasingly hard to field: response rates fall, panels attrit, and recruiting
interviewers is difficult. The cheaper digital modes that replace it (telephone, web,
self-administered questionnaires) discard almost everything
except the answer itself. The interaction that produced the answer, and with it
most of the evidence about whether the answer is any good, is simply not
recorded.

FACES takes a third route, built on three converging developments:

- **Multimodality.** Audio and video carry information the answer alone does
  not: hesitation, tone, emotional expression, comfort. A system designed to
  capture these gets them consistently and at scale, rather than through
  post-hoc coding.
- **Extended reality.** In an XR interview, the spatial configuration itself
  becomes controllable. Avatars, voices, rooms and interfaces can be
  manipulated as experimental conditions, and the interview space is widely
  understood to shape the interview.
- **Informational networking.** Borrowing from hypertext, interview data can be
  represented as a network rather than a list of question–answer pairs.
  Questionnaire items, multimodal recordings and contextual signals become
  nodes; their temporal and behavioural relations become typed links.

Taken together, these shift the interview from a mechanism for collecting
responses to an instrument for capturing and interpreting interconnected,
context-rich interaction data.

## Research questions

1. What are the advantages of avatar-based interviews compared to video-based
   interviews in terms of acceptance, feasibility and data quality?
2. Which combinations of features reduce interviewer effects, and how do they
   interact?
3. How can the results be integrated into a theory for training virtual
   interviewers?

## Approach

<div class="faces-grid" markdown>

<div class="faces-card" markdown>

<span class="faces-chip faces-chip--released">Released</span>

### 1 · Build the platform

An open-source avatar and video interview environment, usable from a VR headset
or an ordinary browser, with multimodal capture and relational storage built in
rather than bolted on. See [Deliverables](deliverables/index.md).
</div>

<div class="faces-card" markdown>

<span class="faces-chip faces-chip--complete">Complete</span>

### 2 · Preliminary experiments

Test avatar characteristics and levels of immersion, and establish that the
instrument is usable, acceptable and stable enough to field. See
[Studies](studies.md).
</div>

<div class="faces-card" markdown>

<span class="faces-chip faces-chip--ongoing">Ongoing</span>

### 3 · Validation

Validate the approach with former [NEPS](https://www.neps-data.de/) panel
participants, a population whose conventional-mode survey history is already
known. This main study is under way now, fielded using InterView, including
its browser client (see [InterView](deliverables/interview.md#in-the-browser)).
</div>

</div>

## System requirements, and where they stand

The platform was specified against seven requirements before it was built. This
table is the honest state of each one.

<div class="scrollable" markdown>

| | Requirement | Status |
|---|---|---|
| **A** | **Supports questionnaires.** A software-based survey tool the interviewer reads from and enters responses into, while the interviewee sees the answer categories visually. | :material-check-circle:{ style="color:#004A6F" } **Implemented.** Any browser-accessible survey tool can be embedded; LimeSurvey is used in production. Answer options render on a panel inside the scene. |
| **B** | **Avatar customisation.** Participants can tailor their avatar-based appearance, including voice, increasing embodiment and providing a form of anonymisation. | :material-check-circle:{ style="color:#004A6F" } **Implemented** for appearance and selection. Voice transformation and emotional expression are advancing through [ReEmote](publications.md#reemote). |
| **C** | **Environment customisation.** The environment is interchangeable and customisable for different interview needs. | :material-check-circle:{ style="color:#004A6F" } **Implemented.** Scenes are defined over the backend API and can be created and edited without rebuilding the client. |
| **D** | **Multi-platform participation.** Desktop, mobile and VR headsets, including concurrent use. | :material-check-circle:{ style="color:#004A6F" } **Implemented.** A VR client and a browser client join the same room; participants using either are represented to the other. |
| **E** | **Platform-specific multimodality.** Interaction modalities appropriate to each device, representing each participant to the others as richly as the hardware allows. | :material-check-circle:{ style="color:#004A6F" } **Implemented.** VR contributes gaze, facial expression, hand and body tracking; the browser client contributes video or an emulated avatar with more limited capture. |
| **F** | **Data collection and linkage.** Everything the system produces is stored in an accessible relational format that preserves the networked structure of the interview. | :material-check-circle:{ style="color:#004A6F" } **Implemented.** See the [data model](deliverables/index.md#the-data-model): 4.57 M records across six linked entity groups in the evaluation study alone. |
| **G** | **LLM-assisted interviews.** Large language models supporting the interview, whether for accessibility or as fully automated embodied interviewers. | :material-progress-clock:{ style="color:#E5007D" } **Designed, not yet realised.** The backend supports an LLM client and the architecture reserves a place for it, but it was not part of the evaluation study. |

</div>

## Division of work

<div class="faces-grid" markdown>

<div class="faces-card" markdown>

### <span class="faces-tag faces-tag--gu">Goethe University</span> Text Technology Lab

Platform architecture and development, the multimodal data model, capture and
synchronisation, gaze and speech processing, and the analysis pipeline.
</div>

<div class="faces-card is-lifbi" markdown>

### <span class="faces-tag faces-tag--lifbi">LIfBi</span> Departments 2 and 3

Survey methodology, experimental design, questionnaire construction, fieldwork,
and validation against the NEPS panel.
</div>

</div>

See the [Team](team.md) for who does what.
