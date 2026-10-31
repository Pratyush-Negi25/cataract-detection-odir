# Experiment Notes

## Evaluation

The three main architectures used the same patient-disjoint splits.
A separate ResNet18 experiment compared equal-sized healthy-only and
mixed-negative training cohorts using shared initialization.

Validation AP selected checkpoints and the primary architecture.
An additional operating threshold maximized validation specificity
subject to sensitivity of at least 90%. This target was not guaranteed
on the test set. Thresholds were not retuned after test evaluation.

Patient-level percentile bootstrap intervals used 2,000 paired samples.
Intervals were pointwise and not adjusted for multiple comparisons.
They describe sampling variability for fixed fitted models, not
training-seed variability.

## Data and implementation limitations

- Dataset annotations were not independently clinically adjudicated.
- The study excluded some ambiguous annotations and image-quality issues.
- The dHash near-duplicate screen was rejected because of excessive
  false matches. It was not used for removal or split grouping.
- No reliable near-duplicate clearance or external validation was achieved.
- The test set contained only 41 cataract-positive images.
- Negative-cohort image counts were matched, but patient counts and
  completed training durations differed.
- The baseline included interrupted/resumed training. Equivalence to
  uninterrupted training was not established.
- Weighted training loss and unweighted validation loss are different
  quantities. Sigmoid outputs were not calibrated probabilities.
- The cache benchmark measured CPU data loading, not end-to-end training
  speed or architecture-only performance.

## Explainability

Grad-CAM used the frozen EfficientNet-B0 model and validation examples.
Cataract and non-cataract targets were explained separately.
Maps were independently normalized.

Original validation batch context was retained after a numerical
difference was observed between single-image and batched inference.
Input equivalence and saved-score checks passed with the corrected method.

Partial parameter randomization changed maps. Fully randomized variants
yielded degenerate maps, making their correlation comparison inconclusive.
No automatic sanity-check pass or clinically correct localization was claimed.

## Reproduction status

The notebook was executed incrementally with checkpoint recovery.
A fresh end-to-end Run All replay has not been verified.
Retain setup definitions, recovery setup, saved manifests, configurations,
checkpoints, prediction receipts and the frozen evaluation protocol.
