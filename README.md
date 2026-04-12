# AutoDock Vina Drug Repurposing Pipeline

> Developing a new drug from scratch costs ~$2.6 billion and takes 10-15 years. Drug repurposing starts with compounds that already passed safety trials and asks: what else can they treat? Molecular docking is how you screen thousands of candidates computationally before touching a single test tube.

## The Idea Behind Computational Drug Repurposing

You've identified a protein target involved in your disease. Maybe it's a hub gene from a WGCNA analysis, or a receptor from your pathway enrichment. Now you want to know: are there existing approved drugs that could bind to this target?

Instead of testing 10,000 compounds in a wet lab, you computationally dock each compound into your protein's binding site and rank them by predicted binding affinity. This is how Nintedanib was identified as a repurposing candidate for COPD.

## What the Binding Affinity Score Actually Means

Vina reports binding affinity in kcal/mol. More negative = stronger predicted binding.

- **-9 to -12 kcal/mol**: Strong binding. Worth investigating experimentally.
- **-7 to -9 kcal/mol**: Moderate. Could be interesting depending on context.
- **Above -7 kcal/mol**: Weak. Probably not worth pursuing.

But here's the critical caveat: docking scores are approximations. A compound ranked #1 might fail in vitro, and #50 might be your actual hit. Treat docking as a filter, not ground truth.

## Usage
```bash
python dock_pipeline.py --receptor protein.pdb --ligands library/ --site "ARG120,TYR355,GLU524"
```

## From Docking to Publication

A docking study alone won't get published in a good journal. You need: molecular dynamics to validate top poses, ADMET predictions, and ideally experimental validation. But this pipeline gives you the starting point.
