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
  totalSlidesDisplayed: 13
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
  template: apa
  #numerical_ref: true
  footnotes: false

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

- Research simulation framework for conservation laws

- Adaptive Discontinuous Galerkin spectral element method

- Various meshing backends (e.g. `p4est`, `t8code`)

<v-click>
<smallskip/>

- ∼20 main developers, ∼75k lines of code

- Focus on extensibility, usability, performance

</v-click>
<v-click>
<smallskip/>

- Shared memory and MPI parallelization

- GPU offloading

<smallskip/>

- [`github.com/trixi-framework/Trixi.jl`](https://github.com/trixi-framework/Trixi.jl)
</v-click>

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

- Make legacy Earth system modelling codes exascale-ready

<v-click>
<br/>

## `MESSy`: Modular Earth Submodel System

- Framework extending global circulation models

- ~90 chemistry and climate models

- [`messy-interface.org`](https://messy-interface.org/)

</v-click>

<img
  class="absolute -top--12% -right-2% w-60 opacity-100"
  src="/common/logos/logo_BMBF_eng.png"
  alt="Logo BMBF"
/>

<img
  v-click="1"
  class="absolute -top--48% -right--17% w-30 opacity-100"
  src="../common/logos/messy_logo.svg"
  alt="Logo MESSy"
/>

<img
  v-click="1"
  class="absolute -top--48% -right--30% w-30 opacity-100"
  src="../common/qr/qr_messy.svg"
  alt="QR-code MESSy"
/>



<!--
- e. g. ECHAM, COSMO or ICON
- idealized to fully coupled setups with full atmospheric chemistry
-->



---
---

# Glossary

- Chemistry-climate model (CCM) = AGCM + chemistry

<v-click>

- Atmospheric global circulation model (AGCM)<br/> = physical model of atmospheric flows

</v-click>

<v-click>

- Dynamical core (dycore) = flow solver

</v-click>

<v-click>

- Solves the "primitive equations"<br/> <span id="huge">&rarr;</span> compressible Euler equations

</v-click>
<v-click>

- Physics / parametrizations = additional (unresolved) models

</v-click>


<img
  class="absolute -top--10% -right--10% w-50 opacity-100"
  src="../common/results/messy/taraborrelli_2022.png"
  alt="Result taraborrelli_2022"
/>

<div class="absolute -right--9% bottom-6%" v-click="1">
<SlidevVideo autoplay loop width=220
  poster="/common/results/heldsuarez/hs_med_surfaceT.0104.png"
  printPoster="/common/results/heldsuarez/hs_med_surfaceT.0104.png"
>
  <source src="/common/results/heldsuarez/hs_med_surfaceT.mp4"
  type="video/mp4" />
</SlidevVideo>
</div>

<!--
-->


---
---
# `MESSy` cont.

- Improve chemical process representation

  - Higher spatial resolution

  - More chemical tracers (~1k)

<v-click>

- Huge computational costs

- Huge memory consumption

</v-click>
<v-click>
<smallskip/>

- AMR to the rescue!

- Needs to be supported by the dynamical core!

</v-click>

<!--
- Main issue: memory
- Chemistry up to 90% of load
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

</v-click>
<smallskip/>
<v-click>

- Integrate ODE in time

</v-click>

<img
  v-click=1
  class="absolute -top--15% -right--2% w-110 opacity-100"
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

- $\int_{V} F(u) \cdot \nabla_x v \approx \left< v, \mathrm{VOL} \right>$ with  

  $\mathrm{VOL}_i = \sum_{j} D_{i,j} f^{\mathrm{vol}}(u_i,u_j)$

<img
  class="absolute -top--20% -right--20% w-35 opacity-100"
  src="/common/tikz/DGnodessingle.svg"
  alt=""
/>

<v-click>

- Additional conservation properties: entropy, kinetic energy, ... 

- Related to split forms <span id=smaller> [@FisherCarpenter2013] [@Gassner2016] </span>

</v-click>
<br/>
<v-click>

## DG promises

- High order <span id="huge">&rarr;</span> gain in effective resolution

- Robustness without artificial stabilization  

- Works with AMR, different element shapes

- High local arithmetic intensity: good for massive parallelization

</v-click>

<!--
- Inherent local conservation properties
- Next: several aspects to highlight
-->



---
---

# Challenge: vertical direction

- Earth's circumference $\,\approx 40\,000 \text{ km}$

- Height of atmosphere $\approx 30 \text{ km}$

<smallskip/>
<v-click>

- Flat cells

</v-click>
<smallskip/>
<v-click>

- Severe time step restrictions

</v-click>

<img
  v-click=1
  class="absolute -bottom--10% -right--10% w-105 opacity-100"
  src="/common/slice_cube_sphere.png"
  alt="Sketch cubed sphere resolution"
/>

<v-click>

<br/>
Remedy: implicit or IMEX schemes

</v-click>

<!--
no issues with cell shape
-->



---
---

# Challenge: well-balancedness

- Atmosphere at rest maintains a balanced, steady state

- Hydrostatic balance: $\quad \partial_z p(z) = - \rho(z) \, g$

<smallskip/>
<v-click>

- Simulation should not divert from initial state

</v-click>

<img
  v-click=1
  class="absolute -top--25% -right--8% w-110 opacity-100"
  src="/common/results/bubble/warm_bubble_l3_p3_nopert.png"
  alt="Sketch cubed sphere resolution"
/>

<br/><br/><br/><br/><br/><br/><br/><br/>

<v-click>

- Remedy: well-balanced schemes, e.g. <span id=smaller> [@Souza2023] </span>
 
</v-click>

<!--
- column of air
- gradient of pressure equals gravity on acting on volume

- well-balanced in shallow water: lake at rest
-->


---
---

# Challenge: hanging nodes

- Hanging nodes due to refinement

- Mortar method

<img
  class="absolute -top--15% -right--5% w-70 opacity-100"
  src="/common/tikz/DGnodeshanging1.svg"
  alt=""
/>

<v-click>

<img
  class="absolute -top--15% -right--5% w-70 opacity-100"
  src="/common/tikz/DGnodeshanging.svg"
  alt=""
/>

</v-click>

<v-click>

- Hydrostatic balance: $\quad \partial_z p(z) = - \rho(z) \, g$  

  $\Rightarrow p(z) \approx p_0 \, e^{\,c g z}$

<img
  class="absolute -bottom--40% -right--30% w-70 opacity-100"
  src="/common/tikz/hydrostatic.svg"
  alt=""
/>

</v-click>

<v-click>

- Different interpolation errors at mortar sides

<img
  class="absolute -bottom--24% -left--8% w-90 opacity-100"
  src="/common/hanging_node_issue.png"
  alt=""
/>

</v-click>

<v-click>

<br/><br/><br/><br/><br/><br/>

- Remedy: split $u = \bar{u} + u'$, solve for perturbations

</v-click>


<!--
- virtual element, share resolution with finer element
-->


---
---

# Baroclinic instability

- Classical test case <span id=smaller> [@JablonowskWilliamson2006] </span>

- Cubed sphere mesh

- 1536 cells initially

- $p = 5$

- Refinement based on velocity

<div class="absolute right-0% top-11%">
<SlidevVideo controls loop width=450
  poster="/common/results/baroclinic/vel_1km_grid.0041.png"
  printPoster="/common/results/baroclinic/vel_1km_grid.0041.png"
  timestamp=4
>
  <source 
  src="/common/results/baroclinic/baro_amr_l01_shima_vel1km_grid.mp4"
  type="video/mp4" />
</SlidevVideo>
</div>

<v-click>
<br/>

## Interim conclusion

- DG works!

- Allows for (locally) increased resolution


</v-click>

<!--
ICON: 120 Schichten
Oberrand in 75 km
Zahl der Dreiecke bei 13 km Maschenweite 2.949.120

Final time step:
DOFs: 2 081 160
 #elements:                9635
 ├── level 1:              9256
 └── level 0:               379
-->


---
---
# Further aspects

- AMR criteria

<v-click>

<smallskip/>

- Real data, validation

</v-click>

<v-click>

<smallskip/>

- Fortan-Julia interface: `libtrixi`

- Fully coupled simulations

</v-click>

<v-click>

<smallskip/>

- Parallel performance, GPU porting

</v-click>

<!--
- objective and automatic adaptation criteria as provided by Multiwave
- Moist equations
- AMR and performance

- DG not worth the effort
- "AMR not plannable, too risky"
- chained intertwinned simulation rus
- schedule, lock-step
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

# Have: high effective resolution

<br/>
<div class="row">
  <div class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>

$\;p=3, \; 32\,768 \text{ DOFs}$

  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l4_p1.png"
  alt=""
/>

$\;p=1, \; 32\,768 \text{ DOFs}$
  </div>
</div>
 


---
---

# Have: high effective resolution cont.

<br/>
<div class="row">
  <div class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>

$\;p=3, \; 32\,768 \text{ DOFs}$
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l5_p1_cfl1.png"
  alt=""
/>

$\;p=1, \; 131\,072 \text{ DOFs}$
  </div>
</div>



---
---

# Have: high effective resolution cont.

<br/>
<div class="row">
  <div  class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>

$\;p=3, \; 32\,768 \text{ DOFs}$
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l6_p1_cfl1.png"
  alt=""
/>

$\;p=1, \; 524\,288 \text{ DOFs}$
  </div>
</div>


---
---

# Have: entropy conservation

<br/>
<div class="row">
  <div class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>

Flux differencing, Ranocha flux <span id=smaller>[@Ranocha2018Thesis]</span>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3_weak.png"
  alt=""
/>

Classical weak form
  </div>
</div>

<!--
-->

---
---

# Have: AMR

<br/>
<div class="row">
  <div class="column" style="text-align: center">
<img
  class="relative opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_l3_p3.png"
  alt=""
/>
<div style="margin-top: -0.6rem">

uniform, $\;p=3, \; 32\,768 \text{ DOFs}$
</div>
  </div>
  <div class="column" style="text-align: center">
  <img
  class="absolute -top--27 -right--16.2  w-105.8 opacity-100"
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_amr.png"
  alt=""
/>
<div style="margin-top: 14rem">

AMR, $\;p=3, \; 6176 \text{ DOFs}$
</div>
  </div>
</div>

<img
  class="absolute -top--27 -right--16.2  w-105.8 opacity-100"
  v-click=1
  style="margin:auto" 
  src="/common/results/bubble/warm_bubble_amr_mesh.png"
  alt=""
  />

<!--
-->


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
