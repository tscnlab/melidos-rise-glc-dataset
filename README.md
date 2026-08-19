# MeLiDos RISE GLC dataset

This repository contains the Borås, Sweden site data collected by RISE
Research Institutes of Sweden for the MeLiDos field study. It is a GLC Schema
3.0.2 Data Package derived from the
[original MeLiDos dataset](https://github.com/MeLiDosProject/NilssonTengelinEtAl_Dataset_2026).

The package entry point is `datapackage.json`. Core metadata are stored in
`data/`; participant-level CSV files referenced by `data/datasets.json` are
organized under `data/files/` by sensor, longitudinal-report, questionnaire,
and study-timing resource.

The source dataset is:

> Nilsson Tengelin, M., Svensson, I., Källberg, S., Zauner, J., & Spitschan,
> M. (2026). *Personal light exposure dataset for Borås, Sweden* [Data set].
> https://doi.org/10.5281/zenodo.18925834

The refactoring converts the source repository's processed tabular RData
resources to UTF-8 CSV, separates records by participant, preserves R factor
ordering as numeric value/label metadata, and supplies GLC 3.0.2 metadata.

## Important source-processing notes

- RISE_S002 wrist timestamps were shifted backward by 13 hours in the source
  pipeline.
- Two RISE_S005 head-device source files were combined. The first file was
  shifted forward by one hour, and both streams were aligned to 10-second
  timestamps.
- RISE_S013 chest timestamps were shifted forward by 14 hours.
- RISE_S011 head data were sampled at one second and ended after approximately
  18 hours when device memory filled.
- The RISE_S014 wrist device stopped recording on 2025-10-11 at 15:53:01.
- The source notes identify early timestamp jumps in RISE_S015 wrist data and
  consider the stream usable from 2025-10-06 16:13:12 onward.
- The source sleep-correction workbook documents manual corrections to dates,
  AM/PM interpretation, swapped fields, removals, and implausible sleep times.
- For the source MCTQ overview calculation, `alarm_f` was forced to `FALSE`.
  The source script states that participants who used an alarm on free days
  must be excluded from formal analyses of the affected chronotype measures.
- The health import contained non-participant screening IDs `1` and `2`; these
  were excluded. RISE_S007 and RISE_S011 each have two screening responses.
  Both are retained in their health dataset, while the later response in
  source order supplies the single participant-characteristic summary.

## Calibration-date note

The source metadata workbook supplies device delivery dates but no separately
identified calibration dates. These delivery dates are used provisionally as
calibration-date proxies and require confirmation against calibration records.

## Validation

The package is validated against GLC Schema 3.0.2 with validator 0.5.2.
Validation also runs automatically through
`.github/workflows/validate-glc-dataset.yml`.

## License

The dataset is licensed under the Creative Commons Attribution 4.0
International License (CC BY 4.0). See `LICENSE`.
