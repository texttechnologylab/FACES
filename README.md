# FACES

**Feasibility, Acceptance, and Data Quality of New Multimodal Surveys**

🌐 **[Project website](https://texttechnologylab.github.io/FACES/)**

A multimodal data space for survey research: avatar-based interviews in virtual
reality and video, both extending and offering an alternative to the face-to-face
interview.

Funded by the Deutsche Forschungsgemeinschaft (DFG), project
[539621548](https://gepris.dfg.de/gepris/projekt/539621548?language=en), within
the Infrastructure Priority Programme
[SPP 2431 *New Data Spaces*](https://www.new-data-spaces.de/en-us/).
October 2024 – September 2027.

Run jointly by the [Text Technology Lab](https://www.texttechnologylab.org/) at
Goethe University Frankfurt and Departments 2 and 3 of the
[Leibniz Institute for Educational Trajectories (LIfBi)](https://www.lifbi.de/)
in Bamberg.

## This repository

This repository contains the **project website** only. The software lives
elsewhere:

| Repository | Contains |
|---|---|
| [InterView](https://github.com/texttechnologylab/InterView) | The interview platform and its deployment stack |
| [Va.Si.Li-Lab](https://github.com/texttechnologylab/Va.Si.Li-Lab) | The Unity VR framework the headset client is built on |
| [Va.Si.Li-Lab-backend](https://github.com/texttechnologylab/Va.Si.Li-Lab-backend) | Logging API, Ubiq room server, chatbot and speech services |
| [Janus-Gateway](https://github.com/texttechnologylab/Janus-Gateway) | Pinned, reproducible Janus WebRTC image |

## Building the site locally

```bash
pip install mkdocs-material
mkdocs serve          # http://127.0.0.1:8000
mkdocs build --strict # what CI runs
```

Pushing to `main` builds the site and deploys it to the `gh-pages` branch via
[GitHub Actions](.github/workflows/mkdocs.yml).

## Layout

```
mkdocs.yml                     site configuration
overrides/
  main.html                    shell; adds the partners & funding strip
  home.html                    landing page: hero + fact strip
  partials/funders.html        funder logo slots
docs/
  index.md                     home
  project.md                   description, requirements (A)-(G) and their status
  deliverables/                InterView, Va.Si.Li-Lab, infrastructure
  studies.md                   the two completed studies and their results
  team.md                      team grid
  publications.md              citations and BibTeX
  stylesheets/faces.css        FACES palette and components
  assets/                      screenshots, figures, portraits, logos
```

## Placeholders

Logo slots and team portraits currently render **visible placeholders**: see
[LOGOS.md](LOGOS.md) for how to swap in real files. Nothing renders broken, and
nothing ships to a reviewer by accident.

## Citation

See the [Publications](https://texttechnologylab.github.io/FACES/publications/)
page.
