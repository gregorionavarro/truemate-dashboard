# TrueMate Voice Supervisor – n8n V1

Objetivo: recibir una llamada terminada desde Retell AI, normalizar datos, enviar transcript y metadatos al AI Supervisor, recibir un JSON estructurado de QA y preparar el resultado para dashboard/alertas.

## Flujo V1

1. Webhook Retell (call_analyzed o evento equivalente configurado en Retell)
2. Normalize Call Data
3. Ignore non-conversations (voicemail/no-answer/very short calls)
4. Build Supervisor Payload
5. OpenAI Responses API with Structured Output
6. Parse QA Result
7. Save/forward result to dashboard storage
8. Alert only if critical=true or overall_score below threshold

## Campos mínimos esperados desde Retell

- call_id
- agent_id
- transcript
- recording_url (cuando esté disponible)
- duration_ms o duración equivalente
- disconnection_reason
- start_timestamp/end_timestamp

## Regla importante

Transcript QA puede evaluar comprensión, repeticiones, exactitud y flujo. Pronunciación, tono, solapamiento de voces e interrupciones NO deben marcarse como hechos confirmados sin evidencia de audio o métricas temporales.

## Próximo paso

Importar `truemate-voice-supervisor-v1.json` en n8n y reemplazar los placeholders de credenciales/URLs. Luego hacer una llamada real y revisar el payload exacto de Retell antes de activar en producción.
