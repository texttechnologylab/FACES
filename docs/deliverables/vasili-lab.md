# Va.Si.Li-Lab

<div class="faces-brand">
  <span class="logo--placeholder">Va.Si.Li-Lab<small>logo in design</small></span>
  <div markdown>

**A VR lab for simulation-based learning,** and the framework InterView is
built on.
[:material-github: Repository](https://github.com/texttechnologylab/Va.Si.Li-Lab) ·
[:material-book-open-variant: Documentation](https://texttechnologylab.github.io/Va.Si.Li-Lab/)
  </div>
</div>

Va.Si.Li-Lab is a Unity framework for collaborative, multi-user VR experiences
with customisable avatars and environments. It was established in the DigiTeLL
project at Goethe University Frankfurt and has since become the substrate for
several research projects, FACES among them.
{ .lead }

## Why FACES builds on it

Simulation-based research runs into a trade-off: the technological conditions
that make behaviour observable tend to constrain how openly people can behave.
Va.Si.Li-Lab was designed around that problem. Its data model uses hypergraphs
to represent multimodal learning and interaction data, interleaved with
ISO-Space to describe distributed documents from the perspective of how they
were interactively generated.

For FACES this matters because an interview is exactly such a case: the answer,
the question, the room, the avatars, the gaze and the timing are not separate
records with a shared key, they are a structure. InterView inherits that
structure rather than reinventing it, and extends it with the interview-specific
entities: question windows, survey items, responses.

## What FACES added

- An **OS-agnostic embedded web browser** as the primary questionnaire
  interface inside the VR scene, with reactive events driven by browser content,
  so answer options can be shown to the interviewee only.
- **Interview-specific scene and role handling**, including the answer-option
  panel and the self-view mirror.
- **Gaze replay against scene geometry**, allowing captured eye tracking to be
  raycast against real colliders after the fact.
- Integration with the **Janus** media layer, so a VR participant and a browser
  participant occupy the same room.
- Emotional expression for avatars through
  [ReEmote](../publications.md#reemote).

## The backend

[Va.Si.Li-Lab-backend](https://github.com/texttechnologylab/Va.Si.Li-Lab-backend)
is a monorepo of independent modules. A minimal deployment needs only the first
two.

| Module | Purpose | |
|---|---|---|
| `database-api/` | Scene, level and role definitions, plus the logging API that all tracking and event data is written through. Scenes can be created and edited entirely over this API. | **required** |
| `Ubiq-server/` | Room and session server: keeps avatars, transforms and ownership in sync. | **required** |
| `chatbot/` | Host process that dynamically loads chatbot clients over a socket and exposes them as one endpoint. | optional |
| `speech2text/` | Speech recognition based on OpenAI Whisper. | optional |
| `docker-images/` | Shared base images for the other modules. | n/a |

!!! warning "Set `X_API_KEY` explicitly"
    It defaults to the empty string, which accepts unauthenticated requests. See
    [Deployment](https://texttechnologylab.github.io/Va.Si.Li-Lab-backend/deployment/#secrets).

For a full VR interview deployment, [InterView](interview.md) runs these
services together with Janus, a TURN relay and the web client.

## Citing Va.Si.Li-Lab

```bibtex
@inproceedings{Mehler:et:al:2023:a,
  author    = {Mehler, Alexander and Bagci, Mevl{\"u}t and Henlein, Alexander
               and Abrami, Giuseppe and Spiekermann, Christian and Schrottenbacher, Patrick
               and Konca, Maxim and L{\"u}cking, Andy and Engel, Juliane and Quintino, Marc
               and Schreiber, Jakob and Saukel, Kevin and Zlatkin-Troitschanskaia, Olga},
  title     = {A Multimodal Data Model for Simulation-Based Learning with Va.Si.Li-Lab},
  booktitle = {Digital Human Modeling and Applications in Health, Safety,
               Ergonomics and Risk Management},
  publisher = {Springer Nature Switzerland},
  address   = {Cham},
  pages     = {539--565},
  year      = {2023},
  doi       = {10.1007/978-3-031-35741-1_39}
}
```

Further Va.Si.Li-Lab papers are listed under
[Publications](../publications.md#framework-foundations).
