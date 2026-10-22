# Labels, Arrangements, and the Gibbs Paradox

An interactive web page that resolves the Gibbs paradox within classical statistical mechanics, using information entropy instead of the quantum-mechanical argument for indistinguishable particles. It is based on the lecture notes by **Prof. Sunghan Ro (Harvard University)**, "Typicality and the Gibbs Paradox" (Lecture 7, Section 3.4), and on the slides of his presentation at the Korean Physical Society Fall Meeting (October 2026). It also draws on R. H. Swendsen's analysis of colloids.

The page is available in English (`index.html`) and Korean (`ko.html`), and each links to the other.

**Live page:** https://lshlj82.github.io/Gibbs-paradox-by-ProfRo/ (Korean: https://lshlj82.github.io/Gibbs-paradox-by-ProfRo/ko.html)

It is a supplement to demo 5, "Large Systems and Entropy," in the [Statistical Physics 1 interactive demos](https://lshlj82.github.io/statphys1-GNU/) ([source](https://github.com/lshlj82/statphys1-GNU)), listed there as demo 5+.

## The idea

The classical resolution of the Gibbs paradox for identical particles is not new: it is well documented in the published literature, and Swendsen's papers give a particularly clear account. This page presents the information-entropy version of that resolution, following Prof. Ro's lecture notes and talk.

Mixing two samples of the same classical gas raises the full entropy by $`2Nk_B\ln 2`$, even though the macroscopic state seems unchanged. The usual fix divides the count by $`N!`$ and appeals to quantum indistinguishability. That argument cannot explain why a molecular-dynamics simulation, in which every particle carries an index, still finds a uniform gas, or why statistical mechanics works for colloids, whose particles really are distinguishable.

The classical resolution keeps every labeled microstate and uses the chain rule for entropy, $`S(X,Y) = S(X|Y) + S(Y)`$, to split the full entropy into two parts:

```math
S_{\rm full} = \underbrace{k_B\ln N!}_{S_{\rm label}} + \underbrace{k_B\ln\!\left[\frac{\tilde V_1^{N_1}}{N_1!}\,\frac{\tilde V_2^{N_2}}{N_2!}\right]}_{S_{\rm arr}} .
```

The labeling entropy counts the ways to put identities on an unlabeled arrangement. It is constant when the total $`N`$ is fixed. The arrangement entropy carries the familiar $`1/N!`$, reduces to the Sackur–Tetrode equation for the ideal gas, and is extensive to leading order. In the mixing experiment, almost all of the $`2Nk_B\ln 2`$ is lost label information:

```math
\Delta S_{\rm label} = k_B\ln\frac{(2N)!}{(N!)^2}, \qquad \Delta S_{\rm arr} = 2Nk_B\ln 2 - \Delta S_{\rm label} \approx \tfrac12 k_B\ln(\pi N).
```

## What's on the page

- **Mixing experiment.** A live simulation of two boxes of labeled particles, taken through five stages: start, open the hole, close it, count each box, and read every label. Bars show the changes in the full, labeling, and arrangement entropies at each stage.
  - A switch treats the colors either as bookkeeping labels for one gas or as two physical species. The full entropy is the same in both cases; only its split between labels and arrangement changes. This is where the apparent discontinuity of the paradox lives.
  - Reading every label returns the full entropy to its initial value: the decrease comes from information acquired, not from inserting a wall.
- **The paradox, slide by slide.** Two tables follow the layout of Prof. Ro's slides:
  - the initial, mixing, and final states for different and for identical gases, with their entropies;
  - "Mixing entropy" is not due to mixing: one particle's probability density and entropy at each stage, and the result for $`N`$ particles. The $`k_B\ln 2`$ per particle is uncertainty about which box the particle is in, not an effect of mixing.
- **Labeling and arrangement entropy.** The derivation from conditional entropy. A plot from $`N = 1`$ to $`10^6`$ shows the labeling share of the mixing entropy approaching 1.
- **Particle exchange.** A labeled simulation with an imaginary partition builds a histogram of $`N_1`$ that matches the binomial distribution. Alongside it, the page compares two entropies:
  - $`S_{\rm specified}`$, which assumes the labels are known and has no interior maximum;
  - $`S_{\rm arr} = k_B\ln P(N_1) + {\rm const}`$, which peaks at equal densities. This is Swendsen's reading of Boltzmann's 1877 definition.
- **Colloids.** Swendsen's two homogenized-milk experiments, one of them interactive. The traditional entropy without $`1/N!`$ decreases during an irreversible partial mixing. The arrangement entropy increases and peaks at equilibrium.

## Running it

The page is a single self-contained `index.html` with no build step. Open it in a modern browser, or deploy it with GitHub Pages:

1. Put `index.html` and this `README.md` at the root of the repository.
2. In **Settings → Pages**, choose **Deploy from a branch** and select the `main` branch and the root folder.
3. The page will be served at `https://lshlj82.github.io/Gibbs-paradox-by-ProfRo/`.

## Technical notes

- Plain HTML, CSS, and JavaScript. The two gas simulations are ideal gases without particle collisions, drawn on `<canvas>`; the plots are SVG. Simulations pause while scrolled out of view.
- Exact factorials use a log-factorial table up to $`2\times10^4`$ and Stirling's series beyond.
- Equations are typeset with [MathJax 3.2.2](https://www.mathjax.org/) loaded from cdnjs. Fonts (Source Serif 4 and IBM Plex Sans) load from Google Fonts, with system fallbacks.
- Light and dark mode: the page follows the system setting, and the sun/moon button in the top-right corner switches by hand. The choice is stored as `netsci-theme` and shared with the other course demos.
- Both language versions share the same code; the script switches its labels by the page's `lang` attribute. The Korean page adds the IBM Plex Sans KR and Noto Serif KR fonts.

## Credits

- Page, explanations, numerical results, and interactive figures: **Claude Opus 5.5** (Anthropic).
- Physics content: lecture notes and presentation slides by **Prof. Sunghan Ro** (Harvard University).
- Course integration: Statistical Physics 1, Prof. Sang Hoon Lee.

## References

1. S. Ro, lecture notes, Chapter 3, "Microscopic dynamics and the foundations of statistical mechanics," Section 3.4, "Typicality and the Gibbs paradox."
2. S. Ro, presentation slides on the Gibbs paradox, Korean Physical Society Fall Meeting (October 2026).
3. R. H. Swendsen, "Statistical mechanics of colloids and Boltzmann's definition of the entropy," *American Journal of Physics* **74**, 187–190 (2006).
4. R. H. Swendsen, "Statistical mechanics of classical systems of distinguishable particles," *Journal of Statistical Physics* **107**, 1143–1165 (2002), as cited in Ref. 3.
5. L. Boltzmann, "Über die Beziehung zwischen dem zweiten Hauptsatze der mechanischen Wärmetheorie und der Wahrscheinlichkeitsrechnung respektive den Sätzen über das Wärmegleichgewicht," *Wiener Berichte* **76**, 373–435 (1877), as cited in Ref. 3.
