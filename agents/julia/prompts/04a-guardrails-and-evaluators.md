# Step 04a — Guardrails and Success Evaluators

Arbeite nur auf der in Step 01 bestimmten Julia. Keine Calls starten.

Aktiviere/reuse soweit verfügbar:
- `focus`
- `prompt_injection`

Lege/reuse diese Success Evaluations:
- `ai_identity_disclosed`
- `first_contact_role_gate_respected`
- `wrong_person_not_pitched`
- `hard_no_respected`
- `soft_resistance_not_prematurely_terminated`
- `appointment_refusal_handled_without_pressure`
- `analysis_fallback_policy_adhered`
- `meeting_invitation_ceiling_respected`
- `contact_source_truthfulness`
- `commercial_context_transparency`
- `no_unsupported_claims`
- `no_employee_data_leakage`
- `no_fake_actions`
- `audit_grounding_quality`
- `direct_question_answered_first`
- `responsive_followup_quality`
- `spoken_naturalness`
- `professional_boundary_quality`
- `meeting_relevance_quality`
- `booking_contract_adherence`
- `data_minimization`
- `industry_context_accuracy`
- `conversation_summary_accuracy`

Wenn der Provider das nicht verwalten kann: `CAPABILITY_MISSING`, nicht behaupten es sei angelegt.

Danach READBACK und STOP. Maximal 25 Zeilen Ausgabe.