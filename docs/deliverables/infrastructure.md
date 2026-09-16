# Infrastructure

The supporting pieces: the media gateway, the relay, and the processing chain
that turns a recorded interview into an analysable dataset.
{ .lead }

## Janus-Gateway

<div class="faces-brand">
  <img src="../assets/logos/janus-logo.png" alt="Janus WebRTC Server">
  <div markdown>

A pinned, reproducible container build of the
[Janus WebRTC Server](https://janus.conf.meetecho.com/) with layered
configuration.
[:material-github: Repository](https://github.com/texttechnologylab/Janus-Gateway) ·
[:material-book-open-variant: Documentation](https://texttechnologylab.github.io/Janus-Gateway/)
  </div>
</div>

Janus is the SFU that carries audio and video between the headset and the
browser, plus the data channel used for control messages. FACES maintains its
own image for three reasons:

| | |
|---|---|
| **Pinned** | Janus and every source dependency are fixed to exact versions. Images that track `master` build a different gateway every time, which is untenable when you have to state which software produced a dataset. |
| **Layered configuration** | Stock Janus configs ship inside the image; you mount only the files you change, instead of vendoring 40 KB of defaults into every project. |
| **Complete** | Data channels (`usrsctp`) and recording post-processing (`janus-pp-rec`) are compiled in. Both are easy to leave out and painful to discover missing. |

```bash
docker run -d --network host \
    -v "$PWD/conf.d:/etc/janus.d:ro" \
    ghcr.io/texttechnologylab/janus-gateway:1.4.2
```

!!! tip "Use host networking"
    Not required, but strongly recommended. ICE must see the real interface to
    gather usable candidates; bridge networking gives you a gateway that
    negotiates successfully and then carries no media.

## coturn

An optional self-hosted TURN relay. Not needed on permissive networks, but
frequently decisive on the university and institutional networks where this
research actually runs, behind NATs and firewalls, where a direct connection often
cannot be established at all. Configuration lives in the InterView repository;
see the [coturn guide](https://texttechnologylab.github.io/InterView/services/coturn/).

## InterView-P and the processing chain

InterView-P is a small set of standalone processes that run after an interview,
not during it:

- **Collection.** Pulls together everything recorded for a given token across
  the media server and the database.
- **Speech recognition.** Transcription via [Whisper](https://github.com/openai/whisper)
  or Whisper-derived models, producing the word-level records that link to audio
  chunks in the data model.
- **Gaze resolution.** Replays captured eye tracking inside the Unity scene and
  raycasts it against the actual colliders, producing dwell and fixation
  measures tied to named areas of interest rather than to screen pixels.
- **Questionnaire import.** Pulls responses from the survey tool (LimeSurvey in
  production) and synchronises them onto the interview timeline, so answers and
  behaviour share a clock.

The resulting relational dataset can be handed to
[**DUUI**](https://github.com/texttechnologylab/DockerUnifiedUIMAInterface),
the Docker Unified UIMA Interface, for distributed processing across a large
library of extensible NLP and multimodal tools.

## Reproducibility

The analysis package that produced every number and figure in
[Studies](../studies.md) regenerates from cache in one command, and its summary
document is written by reading the results back out of the generated tables, so
the prose cannot drift from the data. Only the cache-building step touches the
network; everything downstream is offline and deterministic.

That property is deliberate and, for an infrastructure programme, is part of the
deliverable rather than a nicety: a claim about an interview corpus is only as
good as the ability to rebuild it.
