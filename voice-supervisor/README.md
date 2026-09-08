# TrueMate Voice Agent Supervisor

Automated QA supervisor for Retell AI voice agents.

## Purpose

Review the real quality of every AI-agent phone conversation and detect degradation before it costs leads, conversions, or money.

This project does **not** audit whether GHL/n8n automations completed correctly. Its primary responsibility is the behavior and quality of the voice agent itself.

## Target architecture

Retell AI -> n8n -> Voice Supervisor -> QA storage/dashboard -> Alerts

Retell AI -> n8n -> GHL remains a separate operational branch.

## V1 scope

The first version evaluates call quality using transcript and call metadata. Audio review is added for pronunciation, timing, interruptions, silence, and naturalness when audio is available.

### Core QA dimensions

- Pronunciation
- Naturalness
- Listening / comprehension
- Interruptions / turn-taking
- Repetition / loops
- Response accuracy
- Flow adherence
- Customer-question handling
- Closing quality
- Critical behavior errors

## Status levels

- HEALTHY
- MONITOR
- DEGRADED
- CRITICAL

## Finding severity

- INFO
- LOW
- MEDIUM
- HIGH
- CRITICAL

## Development order

1. Define normalized call input schema
2. Define deterministic QA rules and scoring
3. Build supervisor prompt and structured output
4. Test with known good/bad calls
5. Connect Retell webhook through n8n
6. Add audio QA
7. Store call-level QA history
8. Add trend/degradation detection
9. Add dashboard and alerts

## Important design rule

The supervisor must distinguish between evidence and inference. It should never report a pronunciation or audio-quality error from transcript alone. Audio-dependent findings require audio evidence.
