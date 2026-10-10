# Bowen Song

Diffusion model learner & experimenter. I train, ablate, and benchmark generative models end-to-end on consumer-grade hardware.

## About Me

- Currently deep-diving into **diffusion probabilistic models**: DDPM, Score-based SDE, and Latent Diffusion
- Participant of the **Huawei Cup China Post-Graduate Mathematical Contest in Modeling** (Problem E: multimodal sentiment recognition in complex scenarios)
- All experiments run on an **NVIDIA RTX 3050 Laptop GPU (4 GB VRAM)** — every project below includes OOM-aware engineering: gradient accumulation, mixed precision, watchdogs, and auto-restart tooling
- Stack: **Python / PyTorch / Windows**

## Portfolio: Diffusion Models, Three Paradigms

I implemented and benchmarked three families of diffusion generative models on the same hardware (cat-face / face generation tasks), each as a standalone repo:

| Repo | Base | What I Did |
|---|---|---|
| [ddpm-pytorch-cats](https://github.com/Bowen-Song026/ddpm-pytorch-cats) | lucidrains/denoising-diffusion-pytorch | Pixel-space DDPM on Oxford-IIIT Pet cats. Model-scale study (dim 32/64/128) + four ablations: batch size, learning rate, objective, sampling steps. Excel/docx report toolchain. |
| [score-sde-pytorch-cats](https://github.com/Bowen-Song026/score-sde-pytorch-cats) | yang-song/score_sde_pytorch | Score-based SDE (VE / VP / sub-VP). Compared the three SDE formulations, plus learning-rate and model-capacity (NF=16/32) ablations and grid search. |
| [ldm-portfolio](https://github.com/Bowen-Song026/ldm-portfolio) | CompVis/latent-diffusion | Latent Diffusion sampling experiment platform. **100+ controlled runs**: sampler comparison (DDIM/PLMS/DDPM), three-model cross-comparison, full parameter grid search (steps x eta x batch size x seed), repeatability verification, and an OOM-guard / auto-restart toolchain. |

### Highlights

- Found the Pareto-optimal sampling config for LDM on 4 GB VRAM: **20 steps + eta 0.5 + DDIM**
- Measured that **PLMS beats DDIM** on both speed and quality for this workload; sampler-to-sampler speed gap up to **3.2x**
- Showed **batch_size=8 is slower than batch_size=4** on small GPUs due to OOM-degradation retries — a counter-intuitive but reproducible result
- VESDE converges better than VPSDE / sub-VPSDE on small-scale image generation in my runs
- Built a self-healing experiment runner (watchdog + OOM guard + structured logging) that survived multi-day unattended parameter sweeps

## Currently Learning

- Score matching and probability-flow ODE theory
- Guided sampling and controllable generation
- Applying diffusion models to the multimodal emotion recognition task (math-modeling Problem E)

## Notes

All three repos keep their upstream projects credited (see each repo's `UPSTREAM_README.md` / License section). Experiment artifacts (datasets, checkpoints, generated images) are gitignored — code, configs, and analysis tooling are what get versioned.
