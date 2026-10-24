# Quipu Vision

**Evidence-driven visual change inspection and spatial-persistence verification using OpenCV 5.**

Quipu Vision compares a reference image with an observed image, detects pixel-change regions,
and optionally processes a user-provided follow-up image. It emits structured observations,
provenance, a verification status, and recommended next actions.

> Status: local OpenCV 5 and AegisForge A2A/web integration were tested. AWS deployment
> remains unverified. This is not an object classifier or a physical-safety certification.

## Python package (standalone engine)

Requires Python 3.11+ and the dependencies specified in `pyproject.toml`.

```bash
python -m pip install -e .
python -m unittest discover -s tests -p test_workflow.py -v
python examples/evaluation/evaluate.py --json-out outputs/evaluation-results.json
```

The tests cover workflow behavior; the synthetic evaluation uses 24 labeled scenarios.
Previous results on OpenCV 5.0.0: initial-change accuracy 75.00% (TP=12, TN=6,
FP=4, FN=2); persistence accuracy 85.71% (TP=4, TN=2, FP=0, FN=1);
33/33 functional tests passed. These are **synthetic**, not real-world performance estimates.

See `docs/competitions/opencv/evaluation.md` and `docs/competitions/opencv/architecture.md`.

## AegisForge A2A + browser UI

The files under `integrations/aegisforge/` are the plugin adapter and front-end **integration
assets**, not a standalone hosted UI or a complete copy of AegisForge. The tested web
experience uses the AegisForge runtime (`a2a_server.py` and `executor.py`) from
[the host repository](https://github.com/ivanjojo369/AegisForge_agent).

After the host repository has been updated to include the tested integration, its
`/demo/vision` interface and A2A `quipu_vision` capability can be reproduced from that host.
Do not claim the hosted interface works by cloning this package alone.

## Deployment

`integrations/aws/vision-lambda.yaml` (if present) is a template prepared for the
AegisForge container image. It does not constitute AWS deployment evidence and cannot
be used directly without building/publishing a compatible image and authorized AWS access.

## Notes

- Follow-up images are supplied by the operator/client; camera capture is not automatic.
- `verified: true` means **pixel-region persistence**, not object recognition or safety.
- No `.env`, credentials, virtual environments, runtime artifacts, or private media
  should be published. Review the staged files before pushing.
- No software license is asserted here. Add a LICENSE only after choosing and
  confirming the desired terms.
