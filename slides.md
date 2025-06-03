---
addons:
- slidev-addon-citations
# You can also start simply with 'default'
theme: ../slidev-theme-uoc
# some information about your slides (markdown enabled)
title: Trixi.jl
# author field for exported PDF or PPTX
author: Benedict Geihe
# keywords field for exported PDF, comma-delimited.
keywords: Trixi.jl,Julia,CFD,DG

# enable presenter mode, can be boolean, 'dev' or 'build'
presenter: true
# enabled pdf downloading in SPA build, can also be a custom url
download: false
# filename of the export file
exportFilename: slidev-exported
# export options
# use export CLI options in camelCase format
# Learn more: https://sli.dev/guide/exporting.html
export:
  format: pdf
  timeout: 300000000
  dark: false
  withClicks: false
  withToc: false

# syntax highlighter, can be 'prism', 'shiki'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# enable twoslash, can be boolean, 'dev' or 'build'
twoslash: false
# show line numbers in code blocks
lineNumbers: false
# download remote assets in local using vite-plugin-remote-assets, can be boolean, 'dev' or 'build'
#remoteAssets: false
# controls whether texts in slides are selectable
selectable: true
# enable slide recording, can be boolean, 'dev' or 'build'
#record: false CAVE menu disappears
# enable Slidev's context menu, can be boolean, 'dev' or 'build'
contextMenu: true
# enable wake lock, can be boolean, 'dev' or 'build'
wakeLock: true
# https://sli.dev/features/drawing

# force color schema for the slides, can be 'auto', 'light', or 'dark'
colorSchema: light
# router mode for vue-router, can be "history" or "hash"
routerMode: history
# aspect ratio for the slides
aspectRatio: 16/9
# real width of the canvas, unit in px
canvasWidth: 980
# used for theme customization, will inject root styles as `--slidev-theme-x` for attribute `x`
themeConfig:
  totalSlidesDisplayed: 42
#  primary: '#005176'

# favicon, can be a local file path or URL
#favicon: 'https://cdn.jsdelivr.net/gh/slidevjs/slidev/assets/favicon.png'
# URL of PlantUML server used to render diagrams
# plantUmlServer: 'https://www.plantuml.com/plantuml'
# fonts will be auto imported from Google fonts
# Learn more: https://sli.dev/custom/fonts
fonts:
  sans: Roboto
  serif: Roboto Slab
  mono: Fira Code

# default frontmatter applies to all slides
defaults:
  layout: pageBar

# drawing options
# Learn more: https://sli.dev/guide/drawing.html
#drawings:
#  enabled: false
#  persist: false
#  presenterOnly: false
#  syncAll: true

biblio:
  filename: ../common/biblio/literature.bib
  csl_template_file: ../common/biblio/style.json # for ieee
  template: ieee
  #numerical_ref: true
  footnotes: full

# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true

# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left

# take snapshot for each slide in the overview
overviewSnapshots: true

layout: cover
---


# An Adaptive Dynamical Core<br/> For Earth System Modeling

## Benedict Geihe

<br/>

### University of Cologne, Division of Mathematics

<br/>

## Math to Product, Valencia, June 5<sup>th</sup>, 2025

<!--
- About DG and AMR
-->




---
---

# Our product: `Trixi.jl`

- Research framework for conservation laws

- Adaptive Discontinuous Galerkin spectral element method

- Various meshing backends (e.g. `p4est`, `t8code`)

<smallskip/>

- ∼20 main developers, ∼75k lines of code

- Focus on extensibility, usability, performance

<smallskip/>

- Shared memory and MPI parallelization

- GPU offloading

<smallskip/>

- [`github.com/trixi-framework/Trixi.jl`](https://github.com/trixi-framework/Trixi.jl)

<img
  class="absolute -top--5% -right--3% w-40 opacity-100"
  src="../common/logos/logo_Trixi.svg"
  alt=""
/>
<img
  class="absolute -top--5% -right--20% w-40 opacity-100"
  src="../common/qr/qr_trixi.svg"
  alt=""
/>
<div class="absolute right-3% bottom-8%">
  <img
    class="w-110"
    src="../common/results/trixi/cylinder_flow_sinusoidal_walls.png"
    alt=""
  />
</div>

<!--
- Single-command reproducibility
<Youtube height=300 width=430 id="Q3Pi41gbOkI"/>
<Arrow x1="10" y1="20" x2="100" y2="200" width="10" />
-->



---
---

# Our customer: `MESSy`

## Project ADAPTEX

- <em>Adaptive Earth system modelling with strongly reduced computation time <br/> for exascale-supercomputers</em>

- Make legacy ESM codes exascale-ready

<v-click>

## `MESSy`: Modular Earth Submodel System

- Framework extending global circulation models

- ~90 chemistry and climate models

- [`messy-interface.org`](https://messy-interface.org/)

</v-click>
<v-click>

## Requirements:

- Chemical process representation benefits from high resolution

- ~1k chemical tracers <span id="huge">&rarr;</span> huge computational costs

- AMR to the rescue!

- Needs to be supported by the dynamical core!

</v-click>

<img
  class="absolute -top--10% -right-2% w-60 opacity-100"
  src="/common/logos/logo_BMBF_eng.png"
  alt="Logo BMBF"
/>

<img
  v-click="1"
  class="absolute -top--38% -right--25% w-30 opacity-100"
  src="../common/logos/messy_logo.svg"
  alt="Logo MESSy"
/>

<img
  v-click="1"
  class="absolute -top--38% -right--38% w-30 opacity-100"
  src="../common/qr/qr_messy.svg"
  alt="QR-code MESSy"
/>



<!--
- Main issue: memory
- Chemistry up to 90% of load

- e. g. ECHAM, COSMO or ICON
- idealized to fully coupled setups with full atmospheric chemistry
-->



---
---

# Glossary

- Chemistry-climate model (CCM) = AGCM + chemistry <smallskip/>

  - Atmospheric global circulation model (AGCM)<br/> = physical model of atmospheric flows <smallskip/>

    - Dynamical core (dycore) = flow solver <smallskip/>

      - Solves the "primitive equations"<br/> <span id="huge">&rarr;</span> compressible Euler equations

    - Physics / parametrizations = additional (unresolved) models


<img
  class="absolute -top--10% -right--10% w-50 opacity-100"
  src="../common/results/messy/taraborrelli_2022.png"
  alt="Result taraborrelli_2022"
/>

<div class="absolute -right--9% bottom-6%" v-click="1">
<SlidevVideo autoplay loop width=220 poster="image/baroclinic_vel_mag_237871.png">
  <source src="/common/results/heldsuarez/hs_med_surfaceT.mp4" type="video/mp4" />
</SlidevVideo>
</div>

<!--
-->



---
---

# DG

- Prototypic hyperbolic conservation law   

  $\partial_t u + \mathrm{div} F(u) = 0$

- Weak form  

  $\int_{V} \partial_t u \, v + \int_{V} F(u) \cdot \nabla v + \int_{\partial V} F(u) \cdot v \cdot n = 0$

<smallskip/>
<v-click>

- Discretization in space: cells $V_l$

- Lagrange basis, defined on $p\!+\!1$ Gauss-Lobatto nodes  

  $u(x,t) \approx u^{(l)}(x,t) = \sum_{j=0}^p U^{(l)}_j(t) \, \ell_j(x)$

</v-click>
<smallskip/>
<v-click>

- Resolve discontinuities at $\partial V$ by Riemann solvers

- Integrate ODE in time

</v-click>

<img
  v-click=1
  class="absolute -top--15% -right--3% w-110 opacity-100"
  src="/common/dg.png"
  alt=""
/>

<img
  v-click=2
  class="absolute -bottom--10% -right--20% w-60 opacity-100"
  src="/common/tikz/DGnodes.svg"
  alt=""
/>

<!--
- Riemann solver like FV
-->


---
---

# DG cont.

## Flux-differencing

- $\int_{V} F(u) \cdot \nabla_x v \approx$

- Related to split forms [@FisherCarpenter2013] [@Gassner2016]

- Additional conservation properties: entropy, kinetic energy, ... 


## Promises

- High order: gain in effective resolution

- High local arithmetic intensity

- Robustness without artificial stabilization  

- Works for different element shapes

- high local arithmetic intensity: ideal for massive parallelization


<!--
- Telescoping sum?

- Inherent local conservation properties


- Next: several aspects to highlight
- TODO: explain flux diff
-->



---
---

# Have: high effective resolution

<div class="row">
  <div id=largenumber class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>
<div style="margin-top: -3rem">

$p=3, \; 32\,768 \text{ DOFs}$
</div>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l4_p1.png"
  alt=""
/>
<div style="margin-top: -3rem">

$p=1, \; 32\,768 \text{ DOFs}$
</div>
  </div>
</div>
 


---
---

# Have: high effective resolution cont.

<div class="row">
  <div id=largenumber class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>
<div style="margin-top: -3rem">

$p=3, \; 32\,768 \text{ DOFs}$
</div>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l5_p1_cfl1.png"
  alt=""
/>
<div style="margin-top: -3rem">

$p=1, \; 131\,072 \text{ DOFs}$
</div>
  </div>
</div>



---
---

# Have: high effective resolution cont.

<div class="row">
  <div id=largenumber class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>
<div style="margin-top: -3rem">

$p=3, \; 32\,768 \text{ DOFs}$
</div>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l6_p1_cfl1.png"
  alt=""
/>
<div style="margin-top: -3rem">

$p=1, \; 524\,288 \text{ DOFs}$
</div>
  </div>
</div>


---
---

# Have: entropy conservation

<div class="row">
  <div id=largenumber class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>
<div style="margin-top: -1.2rem">

Flux differencing, Ranocha flux <Cite bref="Ranocha2018Thesis"/>
</div>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3_weak.png"
  alt=""
/>
<div style="margin-top: -1.2rem">

Classical weak form
</div>
  </div>
</div>

<!--
-->

---
---

# Have: AMR

<div class="row">
  <div id=largenumber class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>
<div style="margin-top: -3rem">

uniform, $p=3, \; 32\,768 \text{ DOFs}$
</div>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_amr.png"
  alt=""
  />
  <img
  class="relative opacity-100"
  v-click=2
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_amr.png"
  alt=""
  />
<div style="margin-top: -3rem">

AMR, $p=3, \; 6176 \text{ DOFs}$
</div>
  </div>
</div>

<!--
TODO
-->


---
---

# Challenge: vertical direction

- $U \approx 40\,000 \text{ km}$ 
- $H \approx 30 \text{ km}

<smallskip/>

- Severe time step restrictions

<img
  class="absolute -bottom--10% -right--20% w-100 opacity-100"
  src="/common/results/bubble/warm_bubble_l3_p3_nopert.png"
  alt="Sketch cubed sphere resolution"
/>



---
---

# Challenge: well-balancedness

- Atmosphere at rest maintains a balanced steady state

- $\partial_z p = - \rho g$

- Simulation should not divert from initial state

<smallskip/>

- Remedy: well-balanced schemes, e.g. [@Souza2023]

<img
  class="absolute -bottom--10% -right--20% w-100 opacity-100"
  src="/common/slice_cube_sphere.png"
  alt="Sketch cubed sphere resolution"
/>

<!---
-->


---
---

# Challenge: Hanging nodes

$$
\begin{aligned}
&\partial_z p = - \rho g \\
&\Rightarrow p(z) \approx p_0 e^{c \, g \, z}
\end{aligned}
$$


<smallskip/>

Remedy: split $q = \bar{q} + q'$, solve for perturbations


<img
  class="absolute -bottom--10% -right--20% w-60 opacity-100"
  src="/common/tikz/DGnodes.svg"
  alt=""
/>

<img
  class="absolute -bottom--40% -right--20% w-60 opacity-100"
  src="/common/tikz/hydrostatic.svg"
  alt=""
/>


<img
  class="absolute -bottom--10% -right--20% w-60 opacity-100"
  src="/common/hanging_node_issue.png"
  alt=""
/>


<!--
- hydrostatic equation Wikipedia
TODO: hanging DG node
TODO: Souza
-->


---
---

# Baroclinic instability

- Classical test case [@JablonowskWilliamson2006]

- Cubed sphere mesh

- $p = 3, \; 98\, 304 \text{ cells}$

- Refinement base on velocity

<smallskip/>

<v-click>

## Preliminary assessment

- DG works!

- Allows to (locally) increase resolution

<div class="absolute right-0% top-10%">
<SlidevVideo autoplay loop width=400>
  <source 
  src="/common/results/baroclinic/baro_amr_l01_shima_vel1km_grid.mp4"
  poster="/common/results/baroclinic/vel_1km_grid.0041.png"
  type="video/mp4" />
</SlidevVideo>
</div>

</v-click>

<!--
ICON: 120 Schichten
Oberrand in 75 km
Zahl der Dreiecke bei 13 km Maschenweite 2.949.120

benefits in (locally increased) resolution
-->


---
---
# Further aspects

- Fortan-Julia interface: `libtrixi`

- Parallel performance

- GPU porting

- Moist equations

- AMR criteria

- Validation

- Real data, required tools

- Fully couples simulations

- AMR and performance

<!--
TODO: QR Juliacon talk?

- DG not worth the effort
- "AMR not plannable, too risky"
- chained intertwinned simulation rus
- schedule, lock-step

- objective and automatic adaptation criteria as provided by Multiwave
--> 


---
layout: biblio
biblio:
  item_per_page: 5
---



---
layout: end
---



---
---

# libtrixi

Reversed workflow:
Fortran calls Julia!
Negligible overhead
See our JuliaCon talk
& reproducibility repository


Make `Trixi.jl` available for legacy codes
- Application: `MESSy` framework
- Common `t8code` meshing backend
- Bidirectional data exchange

<img
  class="absolute w-85% bottom-15%"
  src="/common/libtrixi-overview.svg"
  alt=""
/>

<!--
- cloud microphysics in \texttt{MESSy}\\[3pt]
- transfer between DG nodes and FV elements via nested grids\\[3pt]
- Test case: tracer transport with Radon decay chain (\texttt{MESSy} \texttt{DRADON} 
-->




---
---

# More results / AMR 

- Geostrophic balance
- Barotropic, baroclinic instability
- Held-Suarez
- Rossby-Haurwitz wave
- Schär mountain gravity waves
- Dry / moist warm rising bubble
- Raining bubble
- Rainy mountain
- Tracer advection

<img
  class="absolute w-15% left-38% bottom-55%"
  src="/common/results/bubble/moist_bubble_dgsem_lmars_chandra_256_p6.png"
  alt=""
/>

<img
  class="absolute w-15% left-38% bottom-15%"
  src="/common/results/bubble/rainy_bubble_64x64_poly3_diffusion05_lax_friedrichs_ec_rain_300s_simple_slip_wall.png"
  alt=""
/>

<div class="absolute right-22% bottom-6%">
<SlidevVideo autoplay loop width=220 poster="image/baroclinic_vel_mag_237871.png">
  <source src="/common/results/tracer/tracer.mp4" type="video/mp4" />
</SlidevVideo>
</div>



---
---

# Lessons learned so far

- Well balancedness
- Non conforming elments vs. hydrostic balance
- Need for regridding tools


<img
  class="absolute w-70 right-35% bottom-15%"
  src="/common/results/heldsuarez/hs_velmag.png"
  alt=""
/>
<img
  class="absolute w-70 right-5% bottom-15%"
  src="/common/results/heldsuarez/hs_fail.png"
  alt=""
/>










---
---

# CPU performance

- Performance of `Trixi.jl` on par with classical codes
  <p style="font-size:14pt; color:#888888; line-height: 1.5rem; margin-top: -6pt">H. Ranocha et al. "Efficient Implementation of Modern Entropy Stable and Kinetic Energy Preserving Discontinuous Galerkin Methods for Conservation Laws". ACM Trans. Math. Softw. (2023).</p> <br/>

- Parallel scaling using `MPI.jl`  
  Baroclinic instability, <span id="longnumber">98 304</span> cells, <span id="longnumber">21 233 664</span> DOFs

<img
  class="absolute w-40% opacity-100"
  src="/common/performance/baroclinic-juwels-cpu-rhs.svg"
  alt=""
/>

<img
  class="absolute right-5% bottom-20% w-40% opacity-100"
  src="/common/performance/trixi-strong-scaling-jureca-dups-juliacon.svg"
  alt=""
/>



---
---

# `Trixi.jl` cont.

Configure simulations through code (*elixir*) <br/>

```julia
using Trixi
using OrdinaryDiffEq

equations = CompressibleEulerEquations2D(gamma = 1.4)
solver = DGSEM(polydeg = 3, surface_flux = flux_lax_friedrichs)
mesh = T8codeMesh((8, 8), (-1.0, -1.0), (1.0, 1.0), polydeg = 3)
my_init(x, t, equations) = ...
semi = SemidiscretizationHyperbolic(mesh, equations, my_init, solver)
tspan = (0.0, 1.0)
ode = semidiscretize(semi, tspan)
# OrdinaryDiffEq.jl
sol = solve(ode, ...)
```

<!--
Trixi as a library
-->


---
---

# Rapid prototyping

Why Julia

modern high-level programming language
solves two-language problem: easy and fast

rapid prototyping capability
lots of ready-to-use packages

performance of Trixi.jl on par with classical codes!
performance portability (GPUs)




Example: Held Suarez forcing
An alternative DSL? 




---
---

# `TrixiAtmo.jl`

Subpackage focused on atmospheric modeling
<br/><br/>


1. General concepts
    - Seperation of horizonal and vertical discretization
    - HEVI
    - Prism elements

2. PDEs on surfaces
    - Covariant advection / shallow water solver

3. Moist Euler equations
    - Cloud microphysics
    - Rain

<!--
(simplified) ICON
Perturbation approach
Total energy including geopotential \\[3pt]
-->



---

# GPU offloading

- Prototype based on `KernelAbstractions.jl`, `Adapt.jl`, CUDA-aware MPI 

- Easy backend switching:

  - ```julia
    ode = semidiscretize(semi, tspan)                     # Vanilla
    ```

  - ```julia
    ode = semidiscretize(semi, tspan; adapt_to=Array)     # CPU
    ```

  - ```julia
    ode = semidiscretize(semi, tspan; adapt_to=CuArray)   # NVIDIA
    ```

  - ```julia
    ode = semidiscretize(semi, tspan; adapt_to=ROCArray)  # AMD
    ```


---

# `KernelAbstractions.jl`
<br>

```julia
function calc_volume_integral!(du, u,..., solver, cache)
    backend = backend_or_nothing(cache.elements)
    _calc_volume_integral!(backend, du, u,..., solver, cache)
end

function _calc_volume_integral!(backend::Nothing, du, u,..., solver, cache)   # Vanilla
    @threaded for element in eachelement(solver, cache)
        weak_form_kernel_element!(du, u, element,..., solver, cache)
    end
end

function _calc_volume_integral!(backend::Backend, du, u,..., solver, cache)   # KernelAbstractions.jl
    kernel! = _weak_form_kernel!(backend)
    kernel!(du, u,..., ndrange = nelements(solver, cache))
end

@kernel function _weak_form_kernel!(du, u,...)
    element = @index(Global)
    weak_form_kernel_element!(du, u, element,..., solver, cache)
end
```


---
---

# Evaluating GPU performance

- ESiWACE3 service

- JUREAP (JUPITER Research and Early Access Program)


---
---

# Project *ADAPTEX*



- Exascale ready framework for CFD

- With AMR, on CPUs and GPUs

- Make legacy ESM codes exascale-ready

- Keep original code

- Add new features written in a high-level language

- Do not sacrifice performance

- Support heterogeneous HPC environments

<img
  class="absolute -bottom--8% -right--1% w-80 opacity-100"
  src="/common/logos/logo_EU.png"
  alt="Logo EU"
/>
<img
  class="absolute -bottom--20% -right-5% w-80 opacity-100"
  src="/common/logos/logo_BMBF_eng.png"
  alt="Logo BMBF"
/>

<!--
- performance portability
- heterogenous compute environments
- `Trixi.jl` as an alternative dynamical core
-->


