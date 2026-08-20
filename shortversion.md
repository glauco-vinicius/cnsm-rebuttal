# Response to Reviewers - Paper #174
## "Evaluating Open-Weight LLMs for Hyperledger Fabric Chaincode Security: Complementarity, Coverage, and Limitations"

We thank the reviewers for their careful feedback. We are grateful two of three reviewers recommend acceptance, and that Reviewer 1 called the paper "useful" and would "like to see it published in some form" despite the Weak Reject score. We address every comment below.

## Reviewer 1

**Comment 1 (V-05 contradiction).** Confirmed: HFCCT's `check_re_addr()` genuinely implements V-05 (Reified Object Addresses) detection, present unchanged since the tool's original release. The contradiction's root is different: the tool's own publication (Li et al., Table 2, Sec. 6) states HFCCT covers only 15/17 taxonomy categories and explicitly lists V-05 as undetected. There is a discrepancy between what the tool's authors documented and what the code does: a working detector absent from the tool's own documentation. Our Table III correctly reproduced the published claim; the inconsistency lies in Section IV-C, which reports V-05 findings from an actual run, contradicting Table III. We corrected this by describing the detector as *undocumented* rather than *not implemented*, revising Table III and Section IV-B accordingly. We also found the three chaincode names in the Table V footnote were wrong due to a transcription error; correct names are cp-digibank, cp-magneto, and token-utxo. Finding counts and Precision are unaffected.

**Comment 2 (pre-filter agent).** The automated pre-filter is DeepSeek V4 Pro 0423, prompted to classify each finding for verdict correctness, taxonomy category, and evidentiary support. Added this specification to Section III-E, noting the GLM-5.2 divergence (~45% automated vs. ~51% manual) as a calibration check, now discussed in Section IV-A.

**Comment 3 (reasoning correctness oversold).** Agreed the three metrics carry unequal weight. Revised the contribution statement to focus on two quantitative metrics (Response Rate, Precision) plus one qualitative observation on reasoning faithfulness, rather than three independently measured dimensions.

**Comment 4 (statistical uncertainty).** Computed 95% Wilson intervals for all five models (n = TP+FP):

| Model | Precision | 95% CI |
|---|---|---|
| GLM-5.2 | 51.0% | [37.7%, 64.1%] |
| MiMo-V2.5-Pro | 63.6% | [35.4%, 84.8%] |
| Kimi-K2.6 | 50.0% | [28.0%, 72.0%] |
| Step-3.7-Flash | 61.1% | [38.6%, 79.7%] |
| DeepSeek-V4-Flash | 0.0% | [0.0%, 16.8%] |

MiMo-V2.5-Pro and GLM-5.2 overlap substantially given MiMo's small sample (n=11); point estimates do not support a superiority claim, and text is revised accordingly. DeepSeek-V4-Flash is the sole statistically distinct result, supporting our claim of a systematic domain-knowledge gap.

**Comment 5 (pedagogical corpus).** Added a Limitations statement noting fabric-samples chaincodes are pedagogical and do not represent production complexity. Softened the auction/EndAuction finding's framing accordingly.

**Comments 6-9.** All incorporated: the abstract distinguishes confirmed-TP from candidate-only categories; Section IV-A is retitled to align with RQ1; "coverage" is clarified as candidate-generation coverage, not recall; Section III-E clarifies pre-filter and manual estimates treat outside-scope findings identically.

**Comment 10 (CNSM fit).** Revised introduction and related work to position chaincode assurance as a network/service-management concern, citing the TNSM guest editorial on blockchain for network and service management and recent CI/CD security work, consistent with the shift-left framing in Figure 1.

## Reviewer 2

**Single-run variability.** Elevated to an explicit limitation in Section V, with multi-run stability analysis as top future-work priority.

**Single-reviewer validation.** Moved to the opening of Section IV, framing all Precision figures as single-reviewer estimates pending dual-reviewer validation with Cohen's kappa.

**Repository-level failures.** Already distinguished in the manuscript: MiMo-V2.5-Pro's 68 failed invocations are attributed to provider-level errors across four full repositories (17 agents each); Kimi-K2.6's 17 failures are attributed to a pipeline-level failure in `irs`. Both counts reconcile exactly. Added a sentence to Section IV-A making this explicit.

**Data contamination.** Added a Limitations paragraph on pretraining-data overlap risk. Future work includes a contamination-free corpus built from unreleased, proprietary chaincode with deliberately injected known vulnerabilities, enabling a more accurate recall measurement.

## Reviewer 3

We thank the reviewer for the positive assessment. The concerns raised, single-run execution and a small corpus, overlap with points above and are addressed by the same revisions. We list multi-run execution and corpus expansion as concrete near-term follow-on work. Finally, it is hard to adjust the paper to a short paper, but we accept the decision of the CNSM reviewers and chair. We prefer to have the paper accepted in its full version; reducing it to five pages could require removing tables, figures, and other contributions the reviewers themselves considered valuable and relevant.

We thank all three reviewers again and believe these revisions address every substantive concern raised.
