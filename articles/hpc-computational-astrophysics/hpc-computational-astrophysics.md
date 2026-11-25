---
title: "Computational Astrophysics & HPC"
summary: "Exact general-EOS Riemann solvers adopted by Athena++, the 2D radiation-hydrodynamic code Guangqi, and high-order discontinuous Galerkin dust coagulation solvers."
tags: []
draft: false
---

# Computational Astrophysics & High-Performance Computing

Accurate modeling of stellar envelopes, planetary accretion shocks, and circumplanetary disks requires numerical methods that handle **non-ideal equations of state (EOS)**, **stiff radiation transport**, and **long-term angular momentum conservation** without sacrificing performance.

---

## 1. Exact & HLLC Riemann Solvers for General Equations of State

<div class="flex flex-col md:flex-row gap-6 items-center my-6">
  <div class="w-full md:w-2/5 max-w-xs shrink-0">
    <img src="./riemannsolver.png" alt="General-EOS Riemann solver comparison" class="rounded-md w-full" />
    <p class="text-xs text-muted-foreground mt-2 text-center">
      General-EOS shock-tube benchmark using the second-order MUSCL scheme in <code>Guangqi</code> (Chen &amp; Bai 2026).
    </p>
  </div>
  <div class="flex-1 space-y-3 text-sm sm:text-base leading-relaxed">
    <p>
      To solve hydrodynamic problems with realistic astrophysical EOS (including H<sub>2</sub> dissociation and H/He ionization), we developed a novel <b>exact general-EOS Riemann solver</b> and a corresponding <b>HLLC approximate Riemann solver</b> (<a href="https://arxiv.org/abs/1903.04568" target="_blank" rel="noopener noreferrer">Chen et al. 2019</a>).
    </p>
    <ul>
      <li>Existence and uniqueness of the exact solution are guaranteed for any monotone EOS.</li>
      <li>Matches the classical exact Euler solver in the ideal-gas limit while accurately capturing real-gas shock transitions.</li>
      <li>In <a href="https://arxiv.org/abs/2602.12545" target="_blank" rel="noopener noreferrer">Chen &amp; Bai (2026)</a>, we applied the second-order <b>MUSCL scheme</b> to the general-EOS solver for high-resolution shock capturing.</li>
      <li><b>Subsequently adopted by <a href="https://arxiv.org/abs/2005.06651" target="_blank" rel="noopener noreferrer"><code>Athena++</code></a> (Stone et al. 2020) and extended by <a href="https://scixplorer.org/abs/2020ApJS..248....7C/abstract" target="_blank" rel="noopener noreferrer">Matthew S. B. Coleman (2020)</a> as its default general-EOS hydrodynamic solver.</b></li>
    </ul>
  </div>
</div>

---

## 2. Guangqi (光启): 2D Radiation Hydrodynamics with Realistic EOS

I am the lead designer and developer of **`Guangqi`**, a two-dimensional, finite-volume radiation-hydrodynamic code written in **Fortran** and parallelized with **MPI** ([Chen & Bai 2026](https://arxiv.org/abs/2602.12545)). Key capabilities and applications include:

- **Coupled Hydrodynamics & Implicit Radiation Transport:** Solves the hydrodynamic equations simultaneously with implicit flux-limited diffusion (FLD) radiation transport.
- **Analytic LTE H/He Equation of State:** Self-consistently captures H<sub>2</sub> dissociation, H ionization, and He first/second ionization.
- **Curvilinear Geometries & PSAMA:** Supports Cartesian and spherical-polar coordinates, featuring our **Passive-Scalar Angular Momentum Algorithm (PSAMA)** for accurate angular-momentum conservation in rotating disks.
- **Scientific Applications in Stellar & Planetary Astrophysics:** `Guangqi` has been applied across our planetary and stellar programs, including planetary accretion shocks ([Chen & Bai 2022](https://arxiv.org/abs/2201.07453); [Zha & Chen 2026](https://arxiv.org/abs/2611.24615)), viscously heated circumplanetary disks ([Chen, Yang & Bai 2026](https://arxiv.org/abs/2610.21284)), and common envelope evolution / luminous red novae ([Chen & Ivanova 2024](https://arxiv.org/abs/2402.05686); [Chen 2026](https://arxiv.org/abs/2510.14173); [Chen et al. 2026](https://arxiv.org/abs/2610.05769)).

<div class="my-6">
  <div class="flex flex-col md:flex-row items-center justify-center gap-2">
    <img src="./density_disk0.png" alt="2D isolated disk initial density" class="h-56 md:h-64 w-auto max-w-full object-contain rounded-md" />
    <img src="./density_disk64.png" alt="2D isolated disk density at t = 6400 P_in" class="h-56 md:h-64 w-auto max-w-full object-contain rounded-md" />
  </div>
  <p class="text-sm text-muted-foreground mt-2 text-center">
    2D isolated accretion disk benchmark in spherical-polar coordinates evolved with <code>Guangqi</code> using PSAMA (Chen &amp; Bai 2026). <b>Left panel:</b> Initial density distribution of the isolated disk. <b>Right panel:</b> Density after 6,400 inner orbital periods (<i>t</i> = 6400 <i>P</i><sub>in</sub>), demonstrating long-term stability and angular-momentum conservation.
  </p>
</div>

---

## 3. GRACE-DG: Discontinuous Galerkin Dust Coagulation-Fragmentation

<div class="flex flex-col md:flex-row gap-6 items-center my-6">
  <div class="w-full md:w-2/5 max-w-sm shrink-0">
    <img src="./grace_dg_model.png" alt="GRACE-DG collisional outcomes model" class="rounded-md w-full bg-white p-2" />
    <p class="text-xs text-muted-foreground mt-2 text-center">
      Collisional outcome regimes (coagulation, bouncing, cratering, mass transfer, and fragmentation) modeled in <code>GRACE-DG</code> (Yang, Chen &amp; Bai 2026).
    </p>
  </div>
  <div class="flex-1 space-y-3 text-sm sm:text-base leading-relaxed">
    <p>
      I co-authored the open-source code <b><a href="https://github.com/jing-xps/GRACE-DG" target="_blank" rel="noopener noreferrer"><code>GRACE-DG</code></a></b> (GRAin Collisional Evolution – Discontinuous Galerkin; <a href="https://arxiv.org/abs/2607.13740" target="_blank" rel="noopener noreferrer">Yang, Chen &amp; Bai 2026</a>) to solve the general nonlinear coagulation-fragmentation equations for dust evolution in protoplanetary disks (<a href="https://github.com/jing-xps/GRACE-DG" target="_blank" rel="noopener noreferrer">GitHub repository</a>). Key advantages include:
    </p>
    <ul>
      <li><b>Conservative Nonlinear Fragmentation:</b> Derives a new conservative mass-flux formulation that captures general nonlinear fragmentation processes, including cratering and mass transfer.</li>
      <li><b>Positivity-Preserving High-Order DG Scheme:</b> Formulated on the conservative Smoluchowski equation, preserving positivity for both coagulation and fragmentation while alleviating the over-diffusion of existing discretized algorithms.</li>
      <li><b>Convergence &amp; Hydrodynamic Readiness:</b> Demonstrates high-order convergence and robustness in coupled aggregation–breakage simulations with fewer mass bins, making it well suited for integration into hydrodynamic codes.</li>
    </ul>
  </div>
</div>
