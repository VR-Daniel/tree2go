<div align="center">

# tree2go

**A fast and interactive browser-based tool for visualizing and editing phylogenetic trees and networks**

[![Status: beta](https://img.shields.io/badge/status-beta-F2B705)](https://github.com/VR-Daniel/tree2go)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/docs/Web/JavaScript)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/HTML)
[![No installation](https://img.shields.io/badge/installation-none-2EA44F)](#getting-started)
[![Works offline](https://img.shields.io/badge/works-offline-2EA44F)](#getting-started)
<br>
[![License: AGPL-3.0](https://img.shields.io/badge/code-AGPL--3.0-0A66C2)](https://www.gnu.org/licenses/agpl-3.0.html)
[![Docs: CC BY-NC-SA 4.0](https://img.shields.io/badge/docs-CC%20BY--NC--SA%204.0-6E7781)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Last commit](https://img.shields.io/github/last-commit/VR-Daniel/tree2go)](https://github.com/VR-Daniel/tree2go/commits)
[![Stars](https://img.shields.io/github/stars/VR-Daniel/tree2go?style=social)](https://github.com/VR-Daniel/tree2go/stargazers)

[**Open tree2go**](https://vr-daniel.github.io/tree2go/) · [Reference guide](https://vr-daniel.github.io/tree2go/#reference) · [Tutorial](https://vr-daniel.github.io/tree2go/#tutorial/en/01-basic-editing) · [How to cite](#how-to-cite)

</div>

---

## What it is

tree2go is a tool for viewing and editing phylogenetic trees and networks, and turning them into publication-ready figures. It brings together, in one place, many of the customization options that are otherwise spread across different programs or that require writing code.

It runs directly in your web browser, with or without an internet connection, and uses your computer's own resources: your trees and data never leave it. It is a single, self-contained HTML file. There is nothing to install, no registration and no subscription, and every feature is available to everyone.

## Highlights

- **Trees and networks.** Reads Newick, NEXUS and extended Newick (phylogenetic networks), with single trees or whole posterior samples from BEAST or MrBayes.
- **Summary trees.** Majority-rule, strict and maximum compatible consensus, maximum clade credibility (MCC) and maximum a posteriori (MAP) trees, with burn-in and node ages summarized from the sample.
- **Uncertainty.** Support values, node-age bars and violins, and tree clouds in the style of DensiTree.
- **Time trees and fossils.** Time axis with the geologic time scale, extinct tips and fossil lineages, and sampled ancestors from fossilized birth-death analyses.
- **Data on the tree.** Branches and nodes colored or sized by any annotation of the tree or column of an attached table, plus side plots: bars, categories, heatmaps and sequence alignments.
- **Ancestral reconstructions.** Pie charts and colored branches from stochastic character maps (SIMMAP).
- **Maps, images and legends.** Maps with records linked to the tips, images, density plots and free text, all movable with alignment guides.
- **Large figures.** Split a long tree into pages, each with a miniature of the whole tree.
- **Fine control.** The left panel changes the whole tree at once, and a right-click on any element changes only that element. Every change can be undone.
- **Accessible colors.** Color-blind-safe palettes and a preview of the figure as seen with color vision deficiencies.
- **Export.** PNG, PDF and SVG at any size and resolution, plus the edited tree as Newick or NEXUS. Projects can be saved and reopened with every change.

## Getting started

There are two ways to use tree2go:

1. **Online:** open [vr-daniel.github.io/tree2go](https://vr-daniel.github.io/tree2go/) in any modern browser (Chrome, Edge, Firefox or Safari).
2. **Offline:** download `index.html` from this repository and open it like any web page. It works without an internet connection, except for a few functions that download data, such as world maps.

Then click `Open tree` in the **Tree** section of the left panel, or drop a tree file on the window.

## Documentation

- **[Options reference guide](https://vr-daniel.github.io/tree2go/#reference):** every option of tree2go, grouped as in the app, with what it does, its values and when it appears.
- **Tutorial on the basic options:** a step-by-step walk from opening a set of trees to exporting the final figure, available in three languages:
  - 🇬🇧 [English](https://vr-daniel.github.io/tree2go/#tutorial/en/01-basic-editing)
  - 🇪🇸 [Español](https://vr-daniel.github.io/tree2go/#tutorial/es/01-basic-editing)
  - 🇧🇷 [Português](https://vr-daniel.github.io/tree2go/#tutorial/pt/01-basic-editing)

## How to cite

If you use tree2go in a publication, please cite it as:

> Vásquez-Restrepo, J. D. & Simões, T. R. (2026). *tree2go: An interactive browser-based phylogenetic tree viewer and editor* [Software]. GitHub. https://github.com/VR-Daniel/tree2go

## Feedback

tree2go is in beta. Given the number of options and how they combine, some combinations may still hide bugs. If you find one, or have a suggestion, please [open an issue](https://github.com/VR-Daniel/tree2go/issues), ideally with the file and the steps that reproduce it.

## License

The source code of tree2go is licensed under the [GNU AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html). All related documentation, assets and materials are shared under a [Creative Commons BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) international license: they can be shared and modified with credit to the authors, for non-commercial purposes only, and any modified version must be shared under the same license.
