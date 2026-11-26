---
title: "Planetary & Moon Formation"
summary: "How do gas giants gain their primordial heat and magnetic fields, and how do moons assemble inside circumplanetary disks? Explore our models linking accretion shocks, disk thermodynamics, and missions like JWST and Tianwen-4."
tags: []
draft: false
---

# Planetary & Moon Formation

Direct imaging of actively accreting protoplanets (such as PDS 70 b and c) and upcoming Solar System missions (*Tianwen-4*, *Europa Clipper*, *JUICE*) demand first-principles models of how gas giants and their moons assemble. My research connects **non-ideal gas thermodynamics**, **2D/3D radiation hydrodynamics (RHD) and MHD**, and **dust coagulation** to multi-wavelength observables.

---

## 1. Planetary Accretion Shocks & Primordial Thermodynamics

<div class="flex flex-col md:flex-row gap-6 items-center my-6">
  <div class="w-full md:w-2/5 max-w-sm shrink-0">
    <img src="./ps_entropy.png" alt="Post-shock specific entropy vs planet mass" class="rounded-md w-full" />
    <p class="text-xs text-muted-foreground mt-2">
      Post-shock specific entropy <i>s</i><sub>ps</sub> vs. planet mass <i>M<sub>p</sub></i> for accretion rates of 10<sup>−2</sup> (red) and 10<sup>−3</sup> <i>M</i><sub>⊕</sub> yr<sup>−1</sup> (black; Chen &amp; Bai 2022).
    </p>
  </div>
  <div class="flex-1 space-y-3 text-sm sm:text-base leading-relaxed">
    <p>
      During the runaway gas accretion phase, infalling gas approaches free-fall velocity and forms a luminous accretion shock at the planet's surface. Using 1D RHD simulations with a realistic hydrogen/helium equation of state, we showed that <b>molecular hydrogen (H<sub>2</sub>) dissociation</b> at ∼2000 K drives a sharp jump in post-shock entropy at high accretion rates, leading to <b>hot-start</b> planet formation (<a href="https://arxiv.org/abs/2201.07453" target="_blank" rel="noopener noreferrer">Chen &amp; Bai 2022</a>).
    </p>
    <p>
      Building on this, we coupled first-principles shock models to planetary interior evolution (<code>MESA</code>) via a physics-informed neural network (<a href="https://arxiv.org/abs/2611.24615" target="_blank" rel="noopener noreferrer">Zha &amp; Chen 2026</a>), predicting initial intrinsic luminosities 4–10 times higher than canonical cold-start models and linking accretion physics directly to primordial dynamo magnetic fields. Under optimistic assumptions, the maximum magnetic field strength at 2 <i>R</i><sub>J</sub> reaches a few gauss for a 0.3 <i>M</i><sub>J</sub> planet, ∼100 G for 1 <i>M</i><sub>J</sub>, and ∼500 G for 3 <i>M</i><sub>J</sub>.
    </p>
  </div>
</div>

<div class="my-6">
  <div class="flex flex-col md:flex-row items-center justify-center gap-2">
    <img src="./planetaccschematic.png" alt="Planetary accretion shock schematic" class="h-56 md:h-64 w-auto max-w-full object-contain rounded-md" />
    <img src="./planetBL.png" alt="Luminosity and magnetic field evolution with realistic EOS vs photospheric boundary conditions" class="h-56 md:h-64 w-auto max-w-full object-contain rounded-md" />
  </div>
  <p class="text-sm text-muted-foreground mt-2 text-center">
    <b>Left panel:</b> Schematic of planetary accretion shock physics: gas infalls at free-fall velocity, passes through an accretion shock at the top of the atmosphere, and settles onto deeper layers under internal (<i>L</i><sub>int</sub>) and accretion (<i>L</i><sub>acc</sub>) luminosities (Zha &amp; Chen 2026). <b>Right panel:</b> Evolution of planetary luminosity <i>L</i> (a) and primordial dynamo magnetic field strength <i>B</i><sub>2<i>R</i><sub>J</sub></sub> (b) for <i>M<sub>p</sub></i> = 0.3, 1, and 3 <i>M</i><sub>J</sub>, comparing our realistic-EOS shock boundary conditions (red) against canonical cold-start photospheric models (blue; Zha &amp; Chen 2026), with filled dots marking the end of accretion.
  </p>
</div>

---

## 2. Viscously Heated Circumplanetary Disks (CPDs) & Moon Formation

Moons assemble inside circumplanetary disks, whose temperature, ionization, and dust distribution govern satellite survival and composition. Using `Guangqi` with a realistic EOS and our passive-scalar angular momentum algorithm (PSAMA), we developed an axisymmetric viscous RHD model of CPDs ([Chen, Yang & Bai 2026](https://arxiv.org/abs/2610.21284)) that self-consistently resolves:

- The **boundary layer** connecting the disk to the planet
- The **inner dust sublimation zone** and snowline location
- **Meridional circulation** and a **high-latitude supersonic accretion stream** (2–5% of the total accretion rate) capable of powering observable Hα emission

<div class="my-6">
  <div class="flex flex-col md:flex-row items-center justify-center gap-4">
    <img src="./cpdschematic.png" alt="Circumplanetary disk schematic" class="h-64 md:h-72 w-auto max-w-full object-contain rounded-md" />
    <img src="./sumsaturn1.png" alt="Quasi-steady-state Saturnian CPD solution" class="h-64 md:h-72 w-auto max-w-full object-contain rounded-md" />
  </div>
  <p class="text-sm text-muted-foreground mt-2 text-center">
    <b>Left panel:</b> Schematic of a viscously heated CPD modeled with <code>Guangqi</code>, illustrating the boundary layer, dust sublimation zone, surface accretion shock, and meridional circulation (Chen, Yang &amp; Bai 2026). <b>Right panel:</b> Quasi-steady-state 2D RHD solution and radial midplane profiles for a Saturnian CPD model (Chen, Yang &amp; Bai 2026).
  </p>
</div>
