# Pixelkiez ElevenLabs Batch Contract v1.3 — Variable Map

**Contract ID:** `pixelkiez-elevenlabs-batch-contract-v1.3`  
**Version:** `1.3.0`  
**Source SHA-256:** `ed9924084c479c3627ceb2648ef301162d5b99bbfddfe3fefe265c7cec915d38`  
**Fields:** 96 total  
**Transport:** `phone_number`  
**Custom Dynamic Variables:** 95  
**Case-sensitive:** yes

## Binding rule

The full v1.3 contract is the provider/batch boundary. `phone_number` is transport only. All other 95 field names remain available as case-sensitive ElevenLabs custom Dynamic Variables when provisioning a v1.3-compatible agent/batch.

This does **not** mean all 95 values belong in Julia's stable system prompt. The prompt bootstrap subset is intentionally bounded in `agents/julia/target-config.json`. Internal, optional and production-gate fields are supplied at the correct runtime/tool/batch layer and are not automatically spoken.

Never silently rename, add, remove or case-normalize contract fields. Unknown extra columns or missing expected columns are contract drift.

## EL_RUNTIME_REQUIRED (2)
- `company_name`
- `company_website`

## EL_RUNTIME_DEFAULTED (18)
- `recipient_number`
- `call_stage`
- `interest_level`
- `confirmed_relevance`
- `meeting_readiness`
- `opt_out`
- `needs_human`
- `prospect_name`
- `prospect_salutation`
- `call_compliance_status`
- `call_compliance_note`
- `lead_source`
- `consultant_name`
- `meeting_description`
- `offer_process`
- `website_analysis_report`
- `agency_name`
- `verified_finding`

## INTERNAL_RECORD (48)
- `customer_website`
- `website_language`
- `restaurant_name`
- `city`
- `prospect_company`
- `audit_id`
- `audit_date`
- `audit_method_scope`
- `audit_overall_score`
- `audit_score_scale`
- `audit_score_status`
- `audit_limitations`
- `audit_strength_1_observation`
- `audit_strength_1_evidence_pointer`
- `audit_strength_1_confidence`
- `audit_hook_1_id`
- `audit_hook_1_dimension`
- `audit_hook_1_priority`
- `audit_hook_1_evidence_class`
- `audit_hook_1_observation`
- `audit_hook_1_evidence_pointer`
- `audit_hook_1_confidence`
- `audit_hook_1_spoken`
- `audit_hook_1_possible_relevance`
- `audit_hook_1_prohibited_claims`
- `audit_hook_1_selector_score`
- `audit_hook_2_id`
- `audit_hook_2_dimension`
- `audit_hook_2_priority`
- `audit_hook_2_evidence_class`
- `audit_hook_2_observation`
- `audit_hook_2_evidence_pointer`
- `audit_hook_2_confidence`
- `audit_hook_2_spoken`
- `audit_hook_2_possible_relevance`
- `audit_hook_2_prohibited_claims`
- `audit_hook_2_selector_score`
- `audit_hook_3_id`
- `audit_hook_3_dimension`
- `audit_hook_3_priority`
- `audit_hook_3_evidence_class`
- `audit_hook_3_observation`
- `audit_hook_3_evidence_pointer`
- `audit_hook_3_confidence`
- `audit_hook_3_spoken`
- `audit_hook_3_possible_relevance`
- `audit_hook_3_prohibited_claims`
- `audit_hook_3_selector_score`

## OPTIONAL (14)
- `lead_id`
- `customer_name`
- `customer_salutation`
- `customer_locale`
- `customer_role`
- `district`
- `restaurant_category`
- `cuisine_type`
- `prospect_role`
- `prospect_locale`
- `preferred_followup_time`
- `consultant_id`
- `meeting_duration_minutes`
- `customer_email`

## PRODUCTION_GATE_ONLY (13)
- `campaign_id`
- `customer_language`
- `website_role`
- `primary_customer_type`
- `lead_source_current`
- `compliance_status`
- `do_not_contact`
- `jurisdiction`
- `contact_type`
- `ai_disclosure_required`
- `recording_status`
- `meeting_offer`
- `meeting_timezone`

## Julia prompt bootstrap subset

Julia's stable prompt references only:

- `company_name`
- `company_website`
- `prospect_name`
- `prospect_salutation`
- `call_compliance_status`
- `call_compliance_note`
- `do_not_contact`
- `lead_source`
- `consultant_name`
- `meeting_duration_minutes`
- `meeting_description`
- `offer_process`
- `website_analysis_report`
- `agency_name`
- `verified_finding`

This is a prompt/context minimization decision, not a reduction of the canonical v1.3 batch contract.
