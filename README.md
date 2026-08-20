# Response to Reviewers - Paper #174
## "Evaluating Open-Weight LLMs for Hyperledger Fabric Chaincode Security: Complementarity, Coverage, and Limitations"

We thank the reviewers for their careful and constructive feedback. We are grateful that two of three reviewers recommend acceptance, and encouraged that Reviewer 1 called the paper "a useful paper" they "would like to see published in some form" despite the Weak Reject score. We address every comment below.

## Reviewer 1

**Comment 1 (V-05 contradiction).** Confirmed: HFCCT's `check_re_addr()` genuinely implements detection for category V-05 (Reified Object Addresses), and this has been present in the tool's code, unchanged, since its original release. The root of the contradiction is different: the tool's own publication (Li et al., Table 2 and Section 6) states that HFCCT covers only 15 of the 17 taxonomy categories and explicitly lists V-05 as one of the two categories it does not detect. There is therefore a discrepancy between what the tool's authors documented and what the code actually does — a working detector that was not listed in the tool's own documentation. Our Table III correctly reproduced the published claim (V-05 not detected); the inconsistency is located in our Section IV-C, which reports V-05 findings from an actual execution of the tool, contradicting our own Table III. We have corrected this by describing the V-05 detector as *undocumented* by the tool rather than *not implemented*, and revised Table III and the corresponding sentence in Section IV-B accordingly. We also found the three chaincode names in the Table V footnote were incorrect due to a transcription error; the correct chaincodes are cp-digibank, cp-magneto, and token-utxo. Finding counts and Precision figures are unaffected.

**Comment 2 (pre-filter agent).** The automated pre-filter is DeepSeek V4 Pro 0423, prompted to classify each finding for verdict correctness, taxonomy category, and evidentiary support. We agree this should not be left implicit and have added the specification to Section III-E, noting the GLM-5.2 divergence (~45% automated versus ~51% manual estimate) as a useful calibration check, now discussed in Section IV-A.

**Comment 3 (reasoning correctness oversold).** We agree that the three metrics do not display the same weight in our work. Hence, we revised the contribution statement to focus on two quantitative metrics, Response Rate and Precision, while also mentioning one qualitative observation on reasoning faithfulness, rather than stating that we cover three independently measured dimensions.

**Comment 4 (statistical uncertainty).** We computed 95% Wilson intervals for all five models (n = TP+FP):

| Model | Precision | 95% CI |
|---|---|---|
| GLM-5.2 | 51.0% | [37.7%, 64.1%] |
| MiMo-V2.5-Pro | 63.6% | [35.4%, 84.8%] |
| Kimi-K2.6 | 50.0% | [28.0%, 72.0%] |
| Step-3.7-Flash | 61.1% | [38.6%, 79.7%] |
| DeepSeek-V4-Flash | 0.0% | [0.0%, 16.8%] |

MiMo-V2.5-Pro and GLM-5.2 overlap substantially given MiMo's small sample (n=11), so the point-estimate ranking does not support a claim of relative superiority; the text is revised accordingly. DeepSeek-V4-Flash remains the sole statistically distinct result, supporting our claim of a systematic domain-knowledge gap for that model.

**Comment 5 (pedagogical corpus).** Added an explicit Limitations statement noting that fabric-samples chaincodes are pedagogical and do not represent production complexity. Softened the framing of the auction/EndAuction finding accordingly.

**Comments 6-9.** All incorporated: the abstract now distinguishes confirmed-TP from candidate-only categories; Section IV-A is retitled to align with RQ1; "coverage" is clarified as candidate-generation coverage, not recall; and Section III-E clarifies that pre-filter and manual estimates treat outside-scope findings identically.

**Comment 10 (CNSM fit).** We revised the introduction and related work to position chaincode assurance as a network- and service-management concern, citing the TNSM guest editorial on blockchain for network and service management and recent CI/CD security work, consistent with the shift-left framing already in Figure 1.

## Reviewer 2

**Single-run variability.** Elevated to an explicit, prominent limitation in Section V, with multi-run stability analysis listed as the top future-work priority.

**Single-reviewer validation.** Moved to the opening of Section IV, framing all Precision figures as single-reviewer estimates pending dual-reviewer validation with Cohen's kappa.

**Repository-level failures.** This distinction is already present in the manuscript: MiMo-V2.5-Pro's 68 failed invocations are attributed to provider-level errors across four full repositories (17 agents each), and Kimi-K2.6's 17 failed invocations to a pipeline-level failure in repository `irs`. Both counts reconcile exactly. We added a sentence to Section IV-A making this attribution explicit.

**Data contamination.** Added a Limitations paragraph acknowledging the risk of pretraining-data overlap. As future work, we plan a contamination-free corpus built from unreleased, proprietary chaincode with deliberately injected known vulnerabilities, which would also enable a proper recall measurement.

## Reviewer 3

We thank the reviewer for the positive assessment. The concerns raised, single-run execution and a small corpus, overlap with points above and are addressed by the same revisions. We list multi-run execution and corpus expansion as concrete near-term follow-on work.

We thank all three reviewers again and believe these revisions address every substantive concern raised.
