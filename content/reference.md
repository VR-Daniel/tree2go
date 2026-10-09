# tree2go options reference guide

Every option of the left panel, section by section, in the same order as in the app. Many options only appear once something they depend on is turned on: the column **Appears when** says what. Options can also be set for single elements from their `Right-click` menu (see [Right-click menus](#right-click-menus)).

## Contents

- [Tree](#tree)
- [Layout](#layout)
- [Branches](#branches)
- [Branch values](#branch-values)
- [Nodes](#nodes)
- [Node values](#node-values)
- [Tip labels](#tip-labels)
- [Clades](#clades)
- [Fossils](#fossils)
- [Phylogenetic networks](#phylogenetic-networks)
- [Scale bar](#scale-bar)
- [Time axis](#time-axis)
- [Ancestral reconstructions](#ancestral-reconstructions)
- [Attachments](#attachments)
- [Side plots](#side-plots)
- [Legends](#legends)
- [Split into pages](#split-into-pages)
- [Images and visual elements](#images-and-visual-elements)
- [Page settings](#page-settings)
- [Export](#export)
- [Right-click menus](#right-click-menus)
- [On the canvas](#on-the-canvas)

## Tree

Load or paste a tree (Newick and NEXUS are recognized from their content, whatever the file extension). A file with many trees (for example a BEAST or MrBayes posterior) opens as a tree set.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Burn-in` | Share of the first trees of the chain left out of every summary. | 0 to 99% | 0% | A file with several trees is open |
| `Show tree number` | Shows one sampled tree of the file, by its position. | Number | 1 | A file with several trees is open |
| `Summary tree` | How the trees of the file are summarized into one. | Majority rule¹<br>Strict consensus²<br>Maximum compatible³<br>Maximum clade credibility (MCC)⁴<br>Maximum a posteriori (MAP)⁵ | Majority rule | A file with several trees is open, **MAP** needs the posterior of each tree in the file (as a `.p` or `. log` file in Attachments) |
| `Clades in more than` | Clades must be found in more than this share of the trees to be kept. | 50 to 100% | 50% | `Summary tree` is **Majority rule** |
| `Node ages` | How the MCC tree gets its node ages from all the trees. | Median<br>Mean | Median | `Summary tree` is **MCC** |
| `Build summary tree` | Builds and shows the chosen summary tree. |  |  | A file with several trees is open |

¹ Majority rule: keeps every clade found in more than the chosen share of the trees (more than half by default), and gives each one that share as its support.  
² Strict consensus: keeps only the clades found in every tree. Where the trees disagree, the branches join in a polytomy.  
³ Maximum compatible: the majority-rule tree plus the less frequent clades that do not conflict with it, added from the most to the least frequent (allcompat in MrBayes).  
⁴ MCC (maximum clade credibility): the sampled tree whose clades have the highest product of their frequencies, as in TreeAnnotator. Each node gets the median or mean age of its clade in all the trees.  
⁵ MAP (maximum a posteriori): the sampled tree with the highest posterior probability, read from the trees file (BEAST) or from the attached log (`.log` of BEAST2, `.p` of MrBayes).  

With unrooted trees (no clock), the branch lengths of the majority-rule, strict and maximum compatible trees are the mean length of each branch over the trees that contain it, as in MrBayes.  

## Layout

The shape of the tree and its overall size.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Shape`¹ | Overall form of the tree. | Rectangular<br>Circular<br>Fan<br>Unrooted | Rectangular |  |
| `Orientation` | Horizontal, with the tips on the right, or vertical, with the tips on top and the root at the bottom. The time axis, the scale bar and the clade names turn with the tree, legends and the title do not. Split into pages works on horizontal trees only. | Horizontal<br>Vertical | Horizontal | `Shape` is **Rectangular** |
| `Scale bar on a vertical tree` | Turns with the tree, vertical like the branches it measures, or stays horizontal under the root. Both measure the same, since the figure keeps one scale in both directions. The time axis always turns with the tree. | Turns with the tree<br>Horizontal | Turns with the tree | `Shape` is **Rectangular**, `Orientation` is **Vertical**, `Show scale bar` is **On**, `Show time axis (dated trees)` is **Off** |
| `Text on a vertical tree` | Vertical: every text reads from bottom to top. Horizontal: the tip names read at 45 degrees and the values of nodes and branches across, beside their branch. The number of the scale bar always follows its bar, and the texts of the side plots (category names, heatmap titles, bar values and bar scale) always stay upright. | Vertical<br>Horizontal | Vertical | `Shape` is **Rectangular**, `Orientation` is **Vertical** |
| `Use branch lengths` | Draws branches proportional to their lengths, when **Off** the tree is a cladogram. | On<br>Off | On |  |
| `Order nodes`² | Sorts every node by clade size, once, for the whole tree. | Increasing<br>Decreasing |  |  |
| `Rename tips from a file…` | Renames many tips at once from a file with two columns: the current name, then the new name. Column headers are optional. | File |  |  |
| `Width` | Horizontal size of the tree, without labels. | 80 to 4000 px | 700 px | **Rectangular** layout |
| `Height` | Vertical distance between neighboring tips. | 3 to 80 px | 18 px | **Rectangular** layout |
| `Radius` |  | 40 to 3000 px | 320 px | **Circular**, **Fan** or **Unrooted** layout |
| `Inner radius (center gap)` | Empty circle left at the center. | 0 to 1500 px | 0 px | `Shape` is **Circular** or **Fan** |
| `Total angle` | How much of the circle the tree fills. | 20 to 360° | 360° | `Shape` is **Circular** |
| `Fan opening` | Angle covered by a fan tree. | 20 to 359° | 180° | `Shape` is **Fan** |
| `Rotation` | Turns the whole circular, fan or unrooted tree. | −180 to 180° | 0° | **Circular**, **Fan** or **Unrooted** layout |
| `Root branch` | Short branch drawn before the root, which can hold its values. | 0 to 80 px | 0 px | `Shape` is not **Unrooted** |

¹ Locked while the page has images.<br>
² Affects the whole tree.

## Branches

Width, color and line style of every branch (a value given to a branch from its `Right-click` menu always wins over the general panel).

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Line width` |  | 1 to 20 px | 1 px |  |
| `Branch color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F |  |
| `Line ends` | Shape of the ends of every line. | Round<br>Square | Round |  |
| `Branch angle` | Angle at which branches leave their node: 90° is the classic square tree, lower values slant them. | 45 to 90° | 90° | **Rectangular** layout |
| `Rounded corners` | Rounds the bend where a branch turns toward its child. | 0 to 30 px | 0 px | **Rectangular** layout |
| `Line style` |  | Solid<br>Dashed<br>Dotted | Solid |  |
| `Dash length (also fossils)` | Used by dashed branches and by grafted fossils. | 1 to 30 px | 5 px |  |
| `Gap between dashes or dots` |  | 1 to 30 px | 3 px |  |

### › Color by data

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Value`¹ | The annotation of the tree or the column of a table that sets the colors. One list: the branch length (raw) first, then every annotation of the tree and every column of the tables (with the table name). | List | None |  |
| `Palette` | The colors of the scale: your own, or a standard palette such as Viridis or Inferno. Those marked ✓ stay distinguishable with the common forms of color blindness. | Custom colors<br>tree2go<br>Okabe-Ito ✓<br>Paul Tol bright ✓<br>Viridis ✓<br>Inferno ✓<br>Magma ✓<br>Plasma ✓<br>Cividis ✓<br>Turbo<br>Spectral<br>Blue to red ✓ | Custom colors | `Value` is set |
| `Reverse the colors` | Runs the palette the other way, low values taking the colors of the high ones. | On<br>Off | Off | `Value` is set |
| `Hue shift` | Turns the hue of every color of the palette. | −180 to 180° | 0° | `Value` is set |
| `Low values` |  | Color | <img src="img/colors/2C7BB6.svg" alt="#2C7BB6" align="absmiddle"> #2C7BB6 | `Value` is set, `Palette` is **Custom colors** |
| `Use a middle color` | Adds a third color for values in the middle of the range. | On<br>Off | On | `Value` is set, `Palette` is **Custom colors** |
| `Middle values` |  | Color | <img src="img/colors/FFFFBF.svg" alt="#FFFFBF" align="absmiddle"> #FFFFBF | `Value` is set, `Use a middle color` is **On**, `Palette` is **Custom colors** |
| `High values` |  | Color | <img src="img/colors/D7191C.svg" alt="#D7191C" align="absmiddle"> #D7191C | `Value` is set, `Palette` is **Custom colors** |
| `Logarithmic scale (log₁₀)` | Uses the base-10 logarithm of the values for the colors, so each tenfold step gets the same share. The legend shows the values themselves. | On<br>Off | Off | `Value` is set |
| `Lowest value of the scale` | Fixes the start of the scale, empty uses the lowest value found. | −10¹² to 10¹² |  | `Value` is set |
| `Highest value of the scale` | Fixes the end of the scale, empty uses the highest value found. | −10¹² to 10¹² |  | `Value` is set |
| `Show a color legend` |  | On<br>Off | On | `Value` is set |

¹ Color the branches by a value read from the tree, such as a rate or a posterior annotation, or from a table in Attachments with tips and internal nodes named as in the tree.  

### › Width by data

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Value`¹ | The annotation of the tree or the column of a table that sets the widths. One list: the branch length (raw) first, then every annotation of the tree and every column of the tables (with the table name). | List | None |  |
| `Thinnest` | Width of the branch with the lowest value. | 0.1 to 10 px | 0.5 px | `Value` is set |
| `Thickest` | Width of the branch with the highest value. | 0.5 to 20 px | 5 px | `Value` is set |
| `Logarithmic scale (log₁₀)` | Uses the base-10 logarithm of the values for the widths, so each tenfold step gets the same share. The legend shows the values themselves. | On<br>Off | Off | `Value` is set |
| `Show legend` |  | On<br>Off | On | `Value` is set |

¹ Make the branches thicker where a value is higher, for example a rate or a posterior probability, read from the tree or from an attached table.  

## Branch values

Labels with the length or annotations for each branch.

### › Values on the branches

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show a value on each branch` | Writes a number on every branch. | On<br>Off | Off |  |
| `Value` | One list: the branch length (raw) first, then every annotation of the tree and every column of the tables (with the table name). | List | Branch length | `Show a value on each branch` is **On** |
| `Decimals` |  | 0, 1, 2, 3, 4, 5, 6 | 3 | `Show a value on each branch` is **On** |
| `Text size` |  | 1 to 100 px | 8 px | `Show a value on each branch` is **On** |
| `Color of the values` | One color for all, or the color of each branch: its color by data, a clade color or the line color, or a color from a parameter of its own, whatever the color of the branches. | One color<br>Like their branch<br>By data | One color | `Show a value on each branch` is **On** |
| `Colored by` | The parameter that gives the colors: branch length (raw), an annotation of the tree or a column of a table. | List | Branch length (raw) | `Show a value on each branch` is **On**, `Color of the values` is **By data** |
| `Palette` | Colors of the scale. Those marked ✓ stay distinguishable with the common forms of color blindness. | tree2go<br>Okabe-Ito ✓<br>Paul Tol bright ✓<br>Viridis ✓<br>Inferno ✓<br>Magma ✓<br>Plasma ✓<br>Cividis ✓<br>Turbo<br>Spectral<br>Blue to red ✓ | Viridis | `Show a value on each branch` is **On**, `Color of the values` is **By data** |
| `Reverse the colors` |  | On<br>Off | Off | `Show a value on each branch` is **On**, `Color of the values` is **By data** |
| `Color` |  | Color | <img src="img/colors/666666.svg" alt="#666666" align="absmiddle"> #666666 | `Show a value on each branch` is **On**, `Color of the values` is **One color** |
| `Position on branch` | Where along the branch the value is written. | Left<br>Center<br>Right | Center | `Show a value on each branch` is **On** |
| `Margin from branch end` | Distance from the end of the branch, for left and right positions. | −2000 to 2000 px | 0 px | `Show a value on each branch` is **On**, `Position on branch` is not **Center** |
| `Vertical offset` | Moves the value up (positive) or down (negative). | −500 to 500 px | 2 px | `Show a value on each branch` is **On** |

## Nodes

Dots on tips and internal nodes.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Dots on tips` |  | On<br>Off | Off |  |
| `Tip dot shape` | Shape of the dots on the tips. Any dot can take its own shape from its right-click menu. | Circle<br>Square<br>Triangle<br>Diamond<br>Star | Circle | `Dots on tips` is **On** |
| `Tip dot size` |  | 0.5 to 12 px | 3 px | `Dots on tips` is **On** |
| `Dots on internal nodes` |  | On<br>Off | Off |  |
| `Node dot shape` | Shape of the dots on the internal nodes. | Circle<br>Square<br>Triangle<br>Diamond<br>Star | Circle | `Dots on internal nodes` is **On** |
| `Node dot size` |  | 0.5 to 12 px | 3 px | `Dots on internal nodes` is **On** |
| `Dot opacity` |  | 5 to 100% | 100% | `Dots on tips` is **On**, `Dots on internal nodes` is **On** |
| `Fill dots` |  | On<br>Off | On | `Dots on tips` is **On**, `Dots on internal nodes` is **On** |
| `Dot color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | `Dots on tips` is **On**, `Dots on internal nodes` is **On**, `Fill dots` is **On** |
| `Dot border` |  | Solid<br>Dashed<br>Dotted<br>None | None | `Dots on tips` is **On**, `Dots on internal nodes` is **On** |
| `Border color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | `Dots on tips` is **On**, `Dots on internal nodes` is **On**, `Dot border` is not **None** |
| `Border width` |  | 0.05 to 50 px | 1 px | `Dots on tips` is **On**, `Dots on internal nodes` is **On**, `Dot border` is not **None** |
| `Number of dashes or dots` | For dashed or dotted borders, how many go around the dot. | 1 to 60 | 12 | `Dots on tips` is **On**, `Dots on internal nodes` is **On**, `Dot border` is **Dashed** or **Dotted** |

### › Dots by data

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Value`¹ | The annotation of the tree or the column of a table that sets the dots. One list: the branch length (raw) first, then every annotation of the tree and every column of the tables (with the table name). | List | None |  |
| `Palette` | The colors of the scale: your own, or a standard palette such as Viridis or Inferno. Those marked ✓ stay distinguishable with the common forms of color blindness. | Custom colors<br>tree2go<br>Okabe-Ito ✓<br>Paul Tol bright ✓<br>Viridis ✓<br>Inferno ✓<br>Magma ✓<br>Plasma ✓<br>Cividis ✓<br>Turbo<br>Spectral<br>Blue to red ✓ | Custom colors | `Value` is set, `Color by the value` is **On** |
| `Reverse the colors` | Runs the palette the other way, low values taking the colors of the high ones. | On<br>Off | Off | `Value` is set, `Color by the value` is **On** |
| `Hue shift` | Turns the hue of every color of the palette. | −180 to 180° | 0° | `Value` is set, `Color by the value` is **On** |
| `Color by the value` | Colors each dot along a scale from its value. | On<br>Off | On | `Value` is set |
| `Low values` |  | Color | <img src="img/colors/2C7BB6.svg" alt="#2C7BB6" align="absmiddle"> #2C7BB6 | `Value` is set, `Color by the value` is **On**, `Palette` is **Custom colors** |
| `High values` |  | Color | <img src="img/colors/D7191C.svg" alt="#D7191C" align="absmiddle"> #D7191C | `Value` is set, `Color by the value` is **On**, `Palette` is **Custom colors** |
| `Size by the value` | Makes each dot bigger as its value grows. | On<br>Off | Off | `Value` is set |
| `Smallest` | Size of the dot with the lowest value. | 0.5 to 10 px | 2 px | `Value` is set, `Size by the value` is **On** |
| `Largest` | Size of the dot with the highest value. | 1 to 20 px | 7 px | `Value` is set, `Size by the value` is **On** |
| `Show legend` |  | On<br>Off | On | `Value` is set |

¹ Give the dots a color or a size from a value, for example the posterior or a rate read from the tree, or a column of a table (nodes with a value always get a dot).  

## Node values

Support values, other values read from the tree (such as ages or probabilities), and bars on the nodes (HPD intervals or age densities from a tree set).

### › Support values

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show as` | How support values are shown on the nodes. | Hidden<br>Number<br>Circles | Hidden |  |
| `Values from`¹ | Where support values come from. | Input tree<br>SIMMAP<br>Trees file | Input tree | `Show as` is not **Hidden** |
| `Decimals` | Decimals of the numbers written, or as they are written in the file. | As written<br>0, 1, 2, 3 | As written | `Show as` is **Number** |
| `Size` |  | 1 to 100 px | 9 px | `Show as` is **Number** or **Circles**, `Which values` is **Above a threshold** |
| `Color of the values` | One color for all, or the color of the branch leading to each node, or a color from a parameter of its own, whatever the color of the branches. | One color<br>Like their branch<br>By data | One color | `Show as` is **Number** |
| `Colored by` | The parameter that gives the colors: branch length (raw), an annotation of the tree or a column of a table. | List | Branch length (raw) | `Show as` is **Number**, `Color of the values` is **By data** |
| `Palette` | Colors of the scale. Those marked ✓ stay distinguishable with the common forms of color blindness. | tree2go<br>Okabe-Ito ✓<br>Paul Tol bright ✓<br>Viridis ✓<br>Inferno ✓<br>Magma ✓<br>Plasma ✓<br>Cividis ✓<br>Turbo<br>Spectral<br>Blue to red ✓ | Viridis | `Show as` is **Number**, `Color of the values` is **By data** |
| `Reverse the colors` |  | On<br>Off | Off | `Show as` is **Number**, `Color of the values` is **By data** |
| `Color` |  | Color | <img src="img/colors/6A6A6A.svg" alt="#6A6A6A" align="absmiddle"> #6A6A6A | `Show as` is not **Hidden**, `Which values` is **Above a threshold**, `Color of the values` is **One color** |
| `Bigger circles for higher values` | Circle size grows with the support. | On<br>Off | Off | `Show as` is **Circles**, `Which values` is **Above a threshold** |
| `Which values` | Show the values above a threshold, or style them by ranges. | Above a threshold<br>By categories | Above a threshold | `Show as` is not **Hidden** |
| `Only when support ≥` | Values below this are not shown. | 0 to 100 | 0 | `Show as` is not **Hidden**, `Which values` is **Above a threshold** |
| `Ranges` | Each range of support gets its own look. | One card per range<br>(from, to, fill, size, border) |  | `Show as` is not **Hidden**, `Which values` is **By categories** |
| `Show category legend` |  | On<br>Off | On | `Show as` is not **Hidden**, `Which values` is **By categories** |
| `Position` | Side of the node, or the middle of its branch. | Left<br>Centered on the branch<br>Right | Left | `Show as` is **Number** |
| `Distance from the node` | Space between the node and the value. | −2000 to 2000 px | 3 px | `Show as` is **Number**, `Position` is not **Centered on the branch** |
| `Vertical offset` | Moves the value up (positive) or down (negative). | −500 to 500 px | 2 px | `Show as` is **Number** |

¹ Input tree: the labels of its internal nodes. Trees file: the percentage of trees that contain the same clade, as in bootstrap or posterior support.  

### › Other node labels

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show`¹ | Value written next to each node: names, annotations or summaries of the trees. | List |  |  |
| `Show as` | Writes each value, or draws a circle whose color and size can follow it. | Number<br>Circles | Number | `Show` is set |
| `Color by the value` | Colors each circle along a scale from its value. | On<br>Off | On | `Show` is set, `Show as` is **Circles** |
| `Low values` |  | Color | <img src="img/colors/2C7BB6.svg" alt="#2C7BB6" align="absmiddle"> #2C7BB6 | `Show` is set, `Show as` is **Circles**, `Color by the value` is **On** |
| `High values` |  | Color | <img src="img/colors/D7191C.svg" alt="#D7191C" align="absmiddle"> #D7191C | `Show` is set, `Show as` is **Circles**, `Color by the value` is **On** |
| `Size by the value` | Makes each circle bigger as its value grows. | On<br>Off | Off | `Show` is set, `Show as` is **Circles** |
| `Circle size` |  | 0.5 to 15 px | 3.5 px | `Show` is set, `Show as` is **Circles**, `Size by the value` is **Off** |
| `Smallest` | Size of the circle with the lowest value. | 0.5 to 10 px | 2 px | `Show` is set, `Show as` is **Circles**, `Size by the value` is **On** |
| `Largest` | Size of the circle with the highest value. | 1 to 20 px | 7 px | `Show` is set, `Show as` is **Circles**, `Size by the value` is **On** |
| `Show legend` |  | On<br>Off | On | `Show` is set, `Show as` is **Circles** |
| `Decimals` |  | 0, 1, 2, 3, 4, 5, 6 | 2 | `Show` is set, `Show as` is **Number** |
| `Text size` |  | 1 to 100 px | 9 px | `Show` is set, `Stack with the support values` is not **After the support (a / b)**, `Show as` is **Number** |
| `Color of the values` | One color for all, or the color of the branch leading to each node, or a color from a parameter of its own, whatever the color of the branches. | One color<br>Like their branch<br>By data | One color | `Show` is set, `Show as` is **Number** |
| `Colored by` | The parameter that gives the colors: branch length (raw), an annotation of the tree or a column of a table. | List | Branch length (raw) | `Show` is set, `Show as` is **Number**, `Color of the values` is **By data** |
| `Palette` | Colors of the scale. Those marked ✓ stay distinguishable with the common forms of color blindness. | tree2go<br>Okabe-Ito ✓<br>Paul Tol bright ✓<br>Viridis ✓<br>Inferno ✓<br>Magma ✓<br>Plasma ✓<br>Cividis ✓<br>Turbo<br>Spectral<br>Blue to red ✓ | Viridis | `Show` is set, `Show as` is **Number**, `Color of the values` is **By data** |
| `Reverse the colors` |  | On<br>Off | Off | `Show` is set, `Show as` is **Number**, `Color of the values` is **By data** |
| `Color` |  | Color | <img src="img/colors/6A6A6A.svg" alt="#6A6A6A" align="absmiddle"> #6A6A6A | `Show` is set, `Stack with the support values` is not **After the support (a / b)**, `Show as` is **Number** or `Color by the value` is **Off**, `Color of the values` is **One color** |
| `Position` | Side of the node, or the middle of its branch. | Left<br>Centered on the branch<br>Right | Left | `Show` is set, `Stack with the support values` is not **After the support (a / b)**, `Show as` is **Number** |
| `Distance from the node` | Space between the node and the label. | −2000 to 2000 px | 3 px | `Show` is set, `Position` is not **Centered on the branch**, `Stack with the support values` is not **After the support (a / b)**, `Show as` is **Number** |
| `Vertical offset` | Moves the label up (positive) or down (negative). | −500 to 500 px | 2 px | `Show` is set, `Stack with the support values` is not **After the support (a / b)**, `Show as` is **Number** |
| `Stack with the support values` | Writes these labels together with the support values. | No<br>Below the branch<br>After the support (a / b) | No | `Show` is set, `Show as` is **Number** |

¹ Load a SIMMAP or a tree with annotations to write values next to the nodes. 

### › Node bars

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Draw`¹ | Uncertainty drawn on each node: an interval from the tree or the ages from a trees file. | List |  |  |
| `Show the ages as` | Full distribution of the ages, or only its HPD interval. | Violin<br>HPD bar | Violin | `Draw` is set |
| `Height` | Thickness of the bar, or height of the violin on each side. | 1 to 40 px | 6 px | `Draw` is set |
| `Color` |  | Color | <img src="img/colors/5B8DEF.svg" alt="#5B8DEF" align="absmiddle"> #5B8DEF | `Draw` is set |
| `Opacity` |  | 5 to 100% | 45% | `Draw` is set |
| `Border` |  | Solid<br>Dashed<br>Dotted<br>None | None | `Draw` is set |
| `Border color` |  | Color | <img src="img/colors/2F5D8C.svg" alt="#2F5D8C" align="absmiddle"> #2F5D8C | `Draw` is set, `Border` is not **None** |
| `Border width` |  | 0.05 to 50 px | 0.8 px | `Draw` is set, `Border` is not **None** |
| `Mirror the density on both sides of the branch` | Draws the violin above and below the branch. | On<br>Off | On | `Draw` is set, `Show the ages as` is not **HPD bar** |
| `Smoothing` | Bandwidth of the density: lower keeps more detail, higher gives a smoother curve. | 0.2 to 3× | 1× | `Draw` is set, `Show the ages as` is not **HPD bar** |
| `Show the HPD inside the violin` | Draws the HPD interval as a thin bar over the violin. | On<br>Off | Off | `Draw` is set, `Show the ages as` is not **HPD bar** |
| `HPD interval` | Share of the ages the interval holds. | 90%, 95%, 99% | 95% | `Draw` is set, `Show the ages as` is **HPD bar**, `Show the HPD inside the violin` is **On** |
| `HPD thickness` |  | 0.5 to 20 px | 3 px | `Draw` is set, `Show the ages as` is not **HPD bar**, `Show the HPD inside the violin` is **On** |
| `HPD color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | `Draw` is set, `Show the ages as` is not **HPD bar**, `Show the HPD inside the violin` is **On** |
| `Mark the median` | A short line at the median age. | On<br>Off | Off | `Draw` is set |
| `Median line width` |  | 0.1 to 20 px | 1.5 px | `Draw` is set, `Mark the median` is **On** |
| `Median line` |  | Solid<br>Dashed<br>Dotted | Solid | `Draw` is set, `Mark the median` is **On** |
| `Median color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | `Draw` is set, `Mark the median` is **On** |
| `Mark the mean` | A short line at the mean age, next to or instead of the median. | On<br>Off | Off | `Draw` is set |
| `Mean line width` |  | 0.1 to 20 px | 1.2 px | `Draw` is set, `Mark the mean` is **On** |
| `Mean line` |  | Solid<br>Dashed<br>Dotted | Dashed | `Draw` is set, `Mark the mean` is **On** |
| `Mean color` |  | Color | <img src="img/colors/C8553D.svg" alt="#C8553D" align="absmiddle"> #C8553D | `Draw` is set, `Mark the mean` is **On** |

¹ Ranges from the tree annotations, such as height_95%_HPD, or age densities from a file with several dated trees.  

## Tip labels

The names at the tips: font, size, style, color, and where the names come from.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show tip names` |  | On<br>Off | On |  |
| `Show` | What the tips show: their names, or any value in one list (branch length, age, the annotations of the tips such as height or rate, and the columns of the tables). | List | The names in the tree | `Show tip names` is **On** |
| `Keep the name, with the value after it` |  | On<br>Off | Off | `Show` is not **The names in the tree** |
| `Decimals` |  | 0 to 4 | 2 | `Show` is not **The names in the tree** |
| `Font size` |  | 1 to 200 px | 12 px |  |
| `Typeface` |  | Helvetica / Arial<br>Verdana<br>Trebuchet<br>Georgia<br>Times<br>Courier | Helvetica / Arial |  |
| `Italic` |  | On<br>Off | On |  |
| `Bold` |  | On<br>Off | Off |  |
| `Keep taxonomic qualifiers upright (cf. / aff. / gr. / sp.)` | Writes qualifiers upright inside italic names, as the codes of nomenclature ask. | On<br>Off | On | `Italic` is **On** |
| `Label color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F |  |
| `Labels take their clade color`¹ | Tip names follow the color of their clade. | On<br>Off | On |  |
| `Distance from branch` |  | 0 to 60 px | 5 px |  |
| `Show underscores as spaces` | Shows *Homo_sapiens* as *Homo sapiens*. | On<br>Off | On |  |
| `Label direction on circular, fan and unrooted trees` | Easy to read flips the labels on the left half, all outward keeps them pointing away from the center. | Easy to read<br>All outward | Easy to read | **Circular**, **Fan** or **Unrooted** layout |
| `Align labels to the right` | Lines up every name in one column, with guides back to the tips. | On<br>Off | Off | `Shape` is not **Unrooted** |
| `Alignment guide` | Line from each tip to its aligned name. | Dotted<br>Solid<br>None | Dotted | `Shape` is not **Unrooted**, `Align labels to the right` is **On** |

¹ Tip names use the color given to the branches of their clade.  

## Clades

Highlights behind clades, collapsed clades and clade name bars.

### › Highlights

Add a highlight from the `Right-click` menu of a branch or a clade (these options set how every highlight looks).

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Highlight opacity` |  | 0.05 to 1 | 0.55 |  |
| `Starts at`¹ | Where the colored background of a clade begins. | Root<br>Stem<br>Node<br>Crown | Node |  |
| `Ends at` | Where the colored background of a clade ends. | The tree edge<br>The clade labels | The tree edge |  |
| `Gradient` | Fades the background toward one end. | None<br>Fade out<br>Fade in | None |  |
| `Corner rounding` |  | 0 to 20 px | 0 px | **Rectangular** layout |

¹ The whole clade, from its own node.  

### › Collapsed clades

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Triangle height` | Rows a collapsed clade takes. | 1 to 10 rows | 2 rows |  |
| `Fill collapsed triangles` |  | On<br>Off | On |  |
| `Show tip count on collapsed clades` | Writes how many tips each collapsed clade holds. | On<br>Off | On |  |

### › Clade name bars

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Name clades from a file…` | Adds many clade name bars at once from a file with one group per line, like *Primates={Homo sapiens, Pan troglodytes}*. One name marks that tip, two or more names their most recent common ancestor. | File |  |  |
| `Show the names next to the bars` | Off, only the bars are drawn. | On<br>Off | On |  |
| `Names on circular and fan trees` | Names pointing outward, or written along the arc. | Radial<br>Curved along the arc | Radial | **Circular** or **Fan** layout, `Show the names next to the bars` is **On** |
| `Position along the arc` | Where a curved name sits along its bar. | Start<br>Center<br>End | Center | **Circular** or **Fan** layout, `Show the names next to the bars` is **On**, `Names on circular and fan trees` is **Curved along the arc** |
| `Clade bar width` |  | 1 to 12 px | 3 px |  |
| `Line up the clade bars in one column`¹ | Puts every bar at the same distance | On<br>Off | On |  |
| `Clade bar distance from labels` |  | −200 to 200 px | 6 px |  |
| `Clade name distance from bar` |  | 0 to 60 px | 6 px |  |
| `Clade name size` |  | 1 to 200 px | 13 px |  |
| `Clade names in bold` |  | On<br>Off | On |  |
| `Clade names in italic` |  | On<br>Off | On |  |

¹ When off, each bar sits right after the labels of its own clade.  

## Fossils

Extinct tips and grafted fossils (fossils can be added from the `Right-click` menu of a branch). Mark a tip as extinct, or add a fossil lineage to a branch, from the `Right-click` menu.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Tips that end before the present are extinct`¹ | In dated trees, marks tips that do not reach the present as fossils. | On<br>Off | On |  |
| `Tolerance` | Tips this close to the present still count as living. | 0 to 5 % of the height | 0.5 % of the height | `Tips that end before the present are extinct` is **On** |
| `Add † after the names of extinct tips and fossils` |  | On<br>Off | On |  |

¹ For dated trees: when the youngest tip is above 0, as in a fossil-only tree, every tip is extinct (`Right-click` a tip to change it by hand).  

### › Sampled ancestors

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show tips on zero-length branches as sampled ancestors`¹ | Draws sampled ancestors of fossilized birth-death trees as dots on their branch. | On<br>Off | On |  |
| `Dot size` |  | 0.5 to 10 px | 3 px | `Show tips on zero-length branches as sampled ancestors` is **On** |
| `Dot color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | `Show tips on zero-length branches as sampled ancestors` is **On** |
| `Names` | Side of the branch where their names go. | Above the branch<br>Below the branch | Above the branch | `Show tips on zero-length branches as sampled ancestors` is **On** |
| `Align the names with their dot` |  | Left<br>Center<br>Right | Right | `Show tips on zero-length branches as sampled ancestors` is **On** |
| `Distance from the branch`² | Space between the branch and the names. | −50 to 200 px | 0 px | `Show tips on zero-length branches as sampled ancestors` is **On** |
| `Branches of extinct tips`³ | Line style of extinct lineages. | Same<br>Dashed<br>Dotted | Dashed |  |

¹ Fossilized birth-death analyses write sampled ancestors as tips on branches of length zero. Each one is drawn as a dot on the branch of its descendants, with its name next to it.  
² `Right-click` the name of one sampled ancestor to move only that one, for example when it overlaps another name.  
³ Grafted fossil lineages are always drawn dashed, using the dash length and gap from Branches.  

## Phylogenetic networks

Networks written in extended Newick (eNewick), as PhyloNet, SNaQ or Dendroscope write them. A node with two parents appears twice with the same label: `#H` (hybridization), `#LGT` (lateral gene transfer) or `#R` (recombination). The occurrence with a subtree, like `(6)#H7`, is the hybrid node, the one that receives, and the bare `#H7` hangs from the donor lineage. A hybrid node has two parents: the major edge brings most of its genome (γ above 0.5), the minor edge the rest, as in introgression. Without the minor edges, what remains is the major tree, drawn with solid lines. A network cannot be rerooted on or below a hybrid node, since both of its parents must stay above it. Gamma (γ), the last field of `name:length:support:γ`, is the share of the genome inherited through each line. Click a line or its value to select it, and right-click it to change only that one. Save Newick writes the network back in eNewick.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show network number` | Shows one of the networks of a file by its number, such as the runs listed by SNaQ, in the order of their score. | Number | 1 | The file holds several networks |
| `Show the reticulations` | Draws each reticulation as a dashed line from the donor lineage to the hybrid node. | On<br>Off | On | A network is open |
| `Hybridization (#H)` | Color of the #H reticulations. | Color | <img src="img/colors/C8553D.svg" alt="#C8553D" align="absmiddle"> #C8553D | `Show the reticulations` is **On**, the network has #H reticulations |
| `Lateral gene transfer (#LGT)` | Color of the #LGT reticulations. | Color | <img src="img/colors/2F5D8C.svg" alt="#2F5D8C" align="absmiddle"> #2F5D8C | `Show the reticulations` is **On**, the network has #LGT reticulations |
| `Recombination (#R)` | Color of the #R reticulations. | Color | <img src="img/colors/7A4E9A.svg" alt="#7A4E9A" align="absmiddle"> #7A4E9A | `Show the reticulations` is **On**, the network has #R reticulations |
| `Width from γ` | Thicker lines for a larger share of the genome inherited through them. | On<br>Off | On | `Show the reticulations` is **On**, the network has γ values |
| `Width` |  | 0.1 to 20 px | 1.5 px | `Show the reticulations` is **On**, `Width from γ` is **Off** |
| `Thinnest (γ = 0)` | Width of a line with γ = 0. Each line takes a width between this and the thickest, in proportion to its γ. | 0.1 to 20 px | 0.6 px | `Show the reticulations` is **On**, `Width from γ` is **On** |
| `Thickest (γ = 1)` | Width of a line with γ = 1. With γ = 0.3, a line sits 30% of the way from the thinnest to the thickest. | 0.1 to 30 px | 4 px | `Show the reticulations` is **On**, `Width from γ` is **On** |
| `Dash length` |  | 0.5 to 50 px | 4 px | `Show the reticulations` is **On** |
| `Gap between dashes` |  | 0.5 to 50 px | 3 px | `Show the reticulations` is **On** |
| `Style` | Major tree: the tree of the major edges, with each minor edge drawn from the donor to the hybrid node. Full network: each hybrid node is a point of its own, where the major edge (from its parent, in the color of its type) and the minor edge (from the donor, in a lighter shade) arrive as curves, and one branch goes on from there. | Major tree<br>Full network | Major tree | `Show the reticulations` is **On** |
| `Arrows` | Arrow heads toward the hybrid (the receiver), toward the donor, at both ends or none. | None<br>To hybrid<br>To donor<br>Both | To hybrid | `Show the reticulations` is **On** |
| `Arrow head size` | Length of each arrow head. It is always a little wider than the line. | 1 to 80 px | 8 px | `Show the reticulations` is **On**, `Arrows` is not **None** |
| `Line` |  | Straight<br>Curved | Curved | `Show the reticulations` is **On**, `Style` is **Major tree** |
| `Curvature` | How far the curve bends toward the root. | 5 to 100% | 40% | `Show the reticulations` is **On**, `Style` is **Major tree**, `Line` is **Curved** |
| `Where on the branches` | Point of each branch where the lines start and end.¹ | Centered<br>Lengths<br>Custom | Centered | `Show the reticulations` is **On** |
| `Position along the branch` | 0% is the parent end of each branch, 100% its node. | 0 to 100% | 50% | `Show the reticulations` is **On**, `Where on the branches` is **Custom** |
| `Show a value on each line` | Writes a value of each reticulation next to its line. | On<br>Off | Off | `Show the reticulations` is **On**, the reticulations carry values |
| `Value` | γ, the length or the support of each reticulation, or any [&…] annotation of its two ends, as written in the file. The minor value goes on the minor edge (the reticulation line). | List | γ (inheritance) | `Show the reticulations` is **On**, `Show a value on each line` is **On** |
| `Decimals` |  | 0 to 4 | 2 | `Show the reticulations` is **On**, `Show a value on each line` is **On** |
| `Color the values like their line` | The major value takes the color of its reticulation type (#H, #LGT or #R), the minor value a lighter shade of it. | On<br>Off | On | `Show the reticulations` is **On**, `Show a value on each line` is **On** |
| `Minor value: text size` |  | 1 to 100 px | 9 px | `Show the reticulations` is **On**, `Show a value on each line` is **On** |
| `Minor value: color` |  | Color | <img src="img/colors/6A6A6A.svg" alt="#6A6A6A" align="absmiddle"> #6A6A6A | `Show the reticulations` is **On**, `Show a value on each line` is **On**, `Color the values like their line` is **Off** |
| `Minor value: horizontal offset` | Moves the minor value sideways. | −500 to 500 px | 4 px | `Show the reticulations` is **On**, `Show a value on each line` is **On** |
| `Minor value: vertical offset` | Moves the minor value up (positive) or down (negative). | −500 to 500 px | 3 px | `Show the reticulations` is **On**, `Show a value on each line` is **On** |
| `Also show the γ of the major edge` | Writes the γ of the main parent too: under the hybrid node's branch, or just before the hybrid node in a full network. | On<br>Off | Off | `Show the reticulations` is **On**, `Show a value on each line` is **On**, `Value` is **γ (inheritance)** |
| `Major value: text size` |  | 1 to 100 px | 9 px | `Show the reticulations` is **On**, `Show a value on each line` is **On**, `Also show the γ of the major edge` is **On** |
| `Major value: color` |  | Color | <img src="img/colors/6A6A6A.svg" alt="#6A6A6A" align="absmiddle"> #6A6A6A | `Show the reticulations` is **On**, `Show a value on each line` is **On**, `Also show the γ of the major edge` is **On**, `Color the values like their line` is **Off** |
| `Major value: horizontal offset` | Moves the major value sideways. | −500 to 500 px | 0 px | `Show the reticulations` is **On**, `Show a value on each line` is **On**, `Also show the γ of the major edge` is **On** |
| `Major value: vertical offset` | Moves the major value up (positive) or down (negative). | −500 to 500 px | 0 px | `Show the reticulations` is **On**, `Show a value on each line` is **On**, `Also show the γ of the major edge` is **On** |

¹ Centered: the middle of each branch. Lengths: where the network places each end, from the branch lengths of the file (without lengths, the middle). Custom: the point chosen with `Position along the branch`.  

## Scale bar

The bar that gives the scale of the branch lengths, for trees without a time axis.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show scale bar`¹ | A bar showing a length in branch units. | On<br>Off | On |  |
| `Length` | Automatic picks a round length, custom uses your own. | Automatic<br>Custom | Automatic | `Show scale bar` is **On** |
| `Bar length` |  | 10⁻⁹ to 10⁹ | 0.1 | `Show scale bar` is **On**, `Length` is **Custom** |
| `Unit` | Written after the number, centred with it on the bar: Ma, subs./site or any text. | Text |  | `Show scale bar` is **On** |
| `Decimals` |  | Auto, 0, 1, 2, 3, 4 | Automatic | `Show scale bar` is **On** |
| `Vertical position` |  | Top<br>Bottom | Bottom | `Show scale bar` is **On**, the bar is locked on the canvas |
| `Horizontal position` |  | Left<br>Center<br>Right | Left | `Show scale bar` is **On**, the bar is locked on the canvas |
| `Move sideways` |  | −400 to 400 px | 0 px | `Show scale bar` is **On**, the bar is locked on the canvas |
| `Move up or down` |  | −400 to 400 px | 0 px | `Show scale bar` is **On**, the bar is locked on the canvas |
| `Line width` |  | 0.1 to 20 px | 1.2 px | `Show scale bar` is **On** |
| `End tick height` | Height of the small marks at both ends. | 0 to 20 px | 4 px | `Show scale bar` is **On** |
| `Text size` |  | 1 to 100 px | 10 px | `Show scale bar` is **On** |
| `Text distance from bar` |  | −40 to 40 px | 4 px | `Show scale bar` is **On** |
| `Color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 | `Show scale bar` is **On** |

¹ Measured in branch length units.  

## Time axis

An axis of ages for dated trees, with the geologic time scale, guide lines and shaded intervals.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show time axis (dated trees)`¹ | Adds an axis of ages under the tree. | On<br>Off | Off | `Use branch lengths` turned **On** |

¹ Needs branch lengths in time units.  

### › Ages

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Age of the youngest tip`¹ | Age where the axis starts. | −10⁶ to 10⁶ | 0 | `Show time axis (dated trees)` is **On** |
| `Time units per branch length unit`² | Factor that turns branch lengths into ages. | 10⁻⁹ to 10⁹ | 1 | `Show time axis (dated trees)` is **On** |
| `Axis title` |  | Text | Ma | `Show time axis (dated trees)` is **On** |
| `Show units next to the youngest value` | Writes the units after the first number of the axis. | On<br>Off | Off | `Show time axis (dated trees)` is **On** |
| `Units` |  | Text | Ma | `Show time axis (dated trees)` is **On**, `Show units next to the youngest value` is **On** |

¹ Change it when the youngest tip is not from the present, as in a fossil-only tree. All tips then count as extinct.  
² Multiplies the branch lengths to get ages. Leave it at 1 when the lengths are already in the units of the axis.  

### › Ticks

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Place ticks` | How the ages on the axis are chosen. | Automatic<br>Every…<br>Geologic<br>Custom | Automatic | `Show time axis (dated trees)` is **On** |
| `Ages` | Your own list of ages to mark, separated by commas. To show a name instead of the number, add it after an equals sign, for example 66=K–Pg. | Text |  | `Place ticks` is **Custom**, `Show time axis (dated trees)` is **On** |
| `Interval` | Distance between ticks, in the units of the axis. | 10⁻⁹ to 10⁹ | 10 | `Show time axis (dated trees)` is **On**, `Place ticks` is **Every…** |
| `Boundaries of` | Geologic units whose boundaries become ticks. | Era<br>Period<br>Epoch<br>Age | Period | `Show time axis (dated trees)` is **On**, `Place ticks` is **Geologic** |
| `Minor ticks between labels` | Small unlabeled ticks between the numbered ones. | 0 to 9 | 1 | `Show time axis (dated trees)` is **On**, `Place ticks` is not **Custom** |
| `Decimals` |  | Auto, 0, 1, 2, 3 | Automatic | `Show time axis (dated trees)` is **On** |

### › Axis look

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Line width` |  | 1 to 6 px | 1 px | `Show time axis (dated trees)` is **On** |
| `Tick length` |  | 0 to 20 px | 5 px | `Show time axis (dated trees)` is **On** |
| `Show the ages on the circles` | Writes the ages on the rings of circular trees. | On<br>Off | On | **Circular**, **Fan** or **Unrooted** layout, `Show time axis (dated trees)` is **On** |
| `Number size` |  | 1 to 100 px | 10 px | **Rectangular** layout, **Circular** or **Fan** layout, `Show time axis (dated trees)` is **On**, `Show the ages on the circles` is **On** |
| `Space between numbers and axis` |  | 0 to 30 px | 3 px | `Show time axis (dated trees)` is **On** |
| `Title size` |  | 1 to 100 px | 11 px | `Show time axis (dated trees)` is **On** |
| `Distance from the tree` | Space between the tree and the axis. | 0 to 60 px | 8 px | `Show time axis (dated trees)` is **On** |
| `Axis color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 | `Show time axis (dated trees)` is **On** |
| `Guide lines at each label` | Lines across the tree at every labeled age. | On<br>Off | Off | `Show time axis (dated trees)` is **On** |
| `Guide line color` |  | Color | <img src="img/colors/9A9A9A.svg" alt="#9A9A9A" align="absmiddle"> #9A9A9A | `Show time axis (dated trees)` is **On**, `Guide lines at each label` is **On** |
| `Guide line style` |  | Solid<br>Dashed<br>Dotted | Dashed | `Show time axis (dated trees)` is **On**, `Guide lines at each label` is **On** |
| `Guide line width` |  | 0.05 to 20 px | 0.6 px | `Show time axis (dated trees)` is **On**, `Guide lines at each label` is **On** |
| `Guide dash length` |  | 1 to 20 px | 3 px | `Show time axis (dated trees)` is **On**, `Guide lines at each label` is **On**, `Guide line style` is **Dashed** |
| `Guide gap between dashes or dots` |  | 1 to 20 px | 3 px | `Show time axis (dated trees)` is **On**, `Guide lines at each label` is **On**, `Guide line style` is not **Solid** |

### › Geologic time scale

Boundaries follow the GSA Geologic Time Scale v. 6.0.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show geologic boxes with official colors` | Adds the geologic time scale under the axis, with the colors of the International Commission on Stratigraphy. | On<br>Off | Off | `Show time axis (dated trees)` is **On** |
| `Eras`<br>`Periods`<br>`Epochs`<br>`Ages (stages)` | Rows of the time scale to show. | On<br>Off | Off | `Show time axis (dated trees)` is **On**, `Show geologic boxes with official colors` is **On** |
| `Row height` |  | 4 to 40 px | 14 px | `Show time axis (dated trees)` is **On**, `Show geologic boxes with official colors` is **On** |
| `Show names that fit` | Writes the name of each unit when there is room. | On<br>Off | On | `Show time axis (dated trees)` is **On**, `Show geologic boxes with official colors` is **On** |
| `Name size` |  | 1 to 60 px | 8 px | `Show time axis (dated trees)` is **On**, `Show geologic boxes with official colors` is **On**, `Show names that fit` is **On** |
| `Box border width` |  | 0 to 10 px | 0.5 px | `Show time axis (dated trees)` is **On**, `Show geologic boxes with official colors` is **On** |
| `Box border color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 | `Show time axis (dated trees)` is **On**, `Show geologic boxes with official colors` is **On**, `Box border width` is **On** |
| `Tree background`¹ | Shades the area behind the tree by geologic interval. | None<br>Colors<br>Stripes | None | `Show time axis (dated trees)` is **On** |
| `Background intervals` | Intervals used to shade the background. | Era<br>Period<br>Epoch<br>Age<br>Ticks | Period | `Show time axis (dated trees)` is **On**, `Tree background` is not **None** |
| `Background opacity` |  | 0.05 to 1 | 0.25 | `Show time axis (dated trees)` is **On**, `Tree background` is not **None** |
| `Extend the background and guide lines down to the axis` | The shading and guides reach the axis instead of stopping at the tree. | On<br>Off | Off | **Rectangular** layout, `Show time axis (dated trees)` is **On**, `Tree background` is not **None**, `Guide lines at each label` is **On** |

¹ **Colors** uses the official colors of the intervals, while **Stripes** alternates light gray bands.  

## Ancestral reconstructions

Ancestral states from a SIMMAP file: pie charts on the nodes and colored branches.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `States` | Colors of the states found in the SIMMAP maps. | One color per state found in the maps |  | A SIMMAP file is attached |
| `Show pies on the nodes` | Pie charts with the probability of each state. | On<br>Off | On |  |
| `Show on`¹ | Which nodes get pies. | All nodes<br>Internal<br>Tips | Internal | `Show pies on the nodes` is **On** |
| `Group the small slices` | Joins the least probable states into one slice. | On<br>Off | Off |  |
| `Group the slices below` | States under this probability are grouped. | 1 to 50% | 10% | `Group the small slices` is **On** |
| `Color of the group`² |  | Color | <img src="img/colors/D9D9D9.svg" alt="#D9D9D9" align="absmiddle"> #D9D9D9 | `Group the small slices` is **On** |

¹ Size, border and opacity of the pies are set in Nodes. A pie replaces any dot or support circle on its node.  
² The slices below the threshold are joined into one slice of this color, in the pies and on the branches, the legend calls it "Other".  

### › Branches

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Color the branches` | Paints the states along each branch, from the SIMMAP maps. | No<br>Maximum a posteriori<br>Most probable states<br>Probability gradient | No |  |
| `Ignore changes shorter than` | Short changes of state are merged into their neighbors. | 1 to 50% | 10% | `Color the branches` is **Maximum a posteriori** |
| `Dominance threshold`¹ | Probability a state needs to be drawn alone. | 1 to 100% | 50% | `Color the branches` is **Most probable states** |
| `Exclusion threshold`² | Probability a state needs to appear when none dominates. | 0 to 100% | 25% | `Color the branches` is **Most probable states** |
| `Stripe length` | Length of the stripes when several states share a stretch. | 1 to 20 px | 3 px | `Color the branches` is **Most probable states** |
| `Show a legend` |  | On<br>Off | On |  |

¹ Each branch is split into short stretches, and each stretch is drawn with the states whose posterior probability there reaches this threshold. With 50%, a state present in at least half of the maps is drawn alone.  
² Used only where no state reaches the dominance threshold: every state at or above this threshold is drawn, alternating as stripes, and the less probable ones are left out. When no state reaches it either, the most probable state is drawn. 

## Attachments

Tables (CSV or TSV) and other files that add data to the tree. Rows are matched to tips and internal nodes by name.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Add table` | Adds data tables to the tree: CSV, TSV or text files whose first column holds the names. | File |  |  |
| `Table list` | The attached tables, with how many names of each one match the tree and a button to remove it. | List |  | A table is added |
| `MCMC log` | Posterior of each sampled tree, needed for the MAP tree: the `.log` of BEAST2 or the `.p` file of MrBayes. | File |  | A trees file is open |

## Side plots

Bars, categories and a heatmap drawn next to the tips, from the attached tables. Their options appear once a table that matches the tree is chosen.

### › Bars

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Table (bars)` | Table with the values to draw as bars. | A table that matches the tree | None | A table is attached |
| `Columns (bars)` | Numeric columns drawn as bars, each with its color. | List |  | A table is chosen for the bars |
| `Width of the bar area` | Room for the longest bar. | 20 to 600 px | 150 px | A table is chosen for the bars |
| `Distance from the previous element` | Space between the labels (or the previous plot) and the bars. | 0 to 200 px | 12 px | A table is chosen for the bars |
| `Bar thickness` | Share of the row each bar takes. | 10 to 100% | 70% | A table is chosen for the bars |
| `Bar opacity` |  | 5 to 100% | 100% | A table is chosen for the bars |
| `Color the bars by named clade` | Each bar takes the color of its clade name bar. | On<br>Off | Off | A table is chosen for the bars |
| `Show as proportions` | Stacks the columns as parts of a whole. | On<br>Off | Off | A table is chosen for the bars |
| `Show them as` | Writes the parts as proportions or percentages. | Proportion<br>Percentage | Proportion | A table is chosen for the bars, `Show as proportions` is **On** |
| `Show the values next to the bars` |  | On<br>Off | Off | A table is chosen for the bars, `Show as proportions` is **On** |
| `Value size` |  | 1 to 100 px | 9 px | A table is chosen for the bars, `Show the values next to the bars` is **On**, `Show as proportions` is **On** |
| `Upper limit of the bars` | Value at the end of the bar area, empty uses the highest value. | 0 to 10¹² |  | A table is chosen for the bars |
| `Show a legend` |  | On<br>Off | On | A table is chosen for the bars |

### › Bar scale

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show a scale under the bars` | Adds an axis with the values of the bars. | On<br>Off | On | A table is chosen for the bars, **Rectangular** layout |
| `Distance from the bars` |  | 0 to 60 px | 4 px | A table is chosen for the bars, **Rectangular** layout, `Show a scale under the bars` is **On** |
| `Line width` |  | 0.2 to 4 px | 0.8 px | A table is chosen for the bars, **Rectangular** layout, `Show a scale under the bars` is **On** |
| `Number distance from the line` |  | 0 to 30 px | 2 px | A table is chosen for the bars, rectangular layout, `Show a scale under the bars` is **On** |
| `Tick length` |  | 0 to 12 px | 4 px | A table is chosen for the bars, **Rectangular** layout, `Show a scale under the bars` is **On** |
| `Number size` |  | 1 to 100 px | 9 px | A table is chosen for the bars, **Rectangular** layout, `Show a scale under the bars` is **On** |
| `Color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 | A table is chosen for the bars, rectangular layout, `Show a scale under the bars` is **On** |

### › Categories

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Table (categories)` | Table with the categories to draw as shapes. | A table that matches the tree | None | A table is attached |
| `Columns (categories)` | Columns drawn as shapes, filled where present. | List |  | A table is chosen for the categories |
| `Shape` |  | Squares<br>Circles | Squares | A table is chosen for the categories |
| `Size` |  | 4 to 40 px | 10 px | A table is chosen for the categories |
| `Space between columns` |  | 0 to 40 px | 3 px | A table is chosen for the categories |
| `Distance from the previous element` |  | 0 to 200 px | 12 px | A table is chosen for the categories |
| `Place them` | Order of the categories and the bars. | After the bars<br>Before the bars | After the bars | A table is chosen for the categories |
| `Absent shapes` | How absent values are drawn. | Filled<br>Outline only | Filled | A table is chosen for the categories |
| `Absent color` |  | Color | <img src="img/colors/E2E2E2.svg" alt="#E2E2E2" align="absmiddle"> #E2E2E2 | A table is chosen for the categories |
| `Shape border` |  | Solid<br>Dashed<br>Dotted<br>None | None | A table is chosen for the categories |
| `Border color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | A table is chosen for the categories, `Shape border` is not **None** |
| `Border width` |  | 0.05 to 50 px | 1 px | A table is chosen for the categories, `Shape border` is not **None** |
| `Number of dashes or dots` |  | 1 to 60 | 12 | A table is chosen for the categories, `Shape border` is **Dashed** or **Dotted** |
| `Turn circular and fan trees inside out` | Puts the tree outside and the categories inside the circle. | On<br>Off | Off | A table is chosen for the categories, **Circular** or **Fan** layout |
| `Show the column titles` |  | On<br>Off | On | A table is chosen for the categories, **Rectangular** layout |
| `Title angle` |  | 45°<br>Vertical | 45° | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On**, `Orientation` is not **Vertical** |
| `Title typeface` |  | Same as the labels |  | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On** |
| `Titles in bold` |  | On<br>Off | Off | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On** |
| `Titles in italic` |  | On<br>Off | Off | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On** |
| `Title size` |  | 1 to 100 px | 10 px | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On** |
| `Title distance` |  | 0 to 40 px | 6 px | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On** |
| `Title color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 | A table is chosen for the categories, **Rectangular** layout, `Show the column titles` is **On** |

### › Heatmap

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Table (heatmap)` | Table with the values of the heatmap. | A table that matches the tree | None | A table is attached |
| `Columns (heatmap)` | Numeric columns, one column of colored cells each. | List |  | A table is chosen for the heatmap |
| `Colour scale` | One color scale per column, or one for all columns. | Each column<br>All columns | Each column | A table is chosen for the heatmap |
| `Low values` |  | Color | <img src="img/colors/2C7BB6.svg" alt="#2C7BB6" align="absmiddle"> #2C7BB6 | A table is chosen for the heatmap |
| `Use a middle color` | Adds a third color for values in the middle of the range. | On<br>Off | On | A table is chosen for the heatmap |
| `Middle values` |  | Color | <img src="img/colors/FFFFBF.svg" alt="#FFFFBF" align="absmiddle"> #FFFFBF | A table is chosen for the heatmap, `Use a middle color` is **On** |
| `High values` |  | Color | <img src="img/colors/D7191C.svg" alt="#D7191C" align="absmiddle"> #D7191C | A table is chosen for the heatmap |
| `Leave missing values empty` | Missing values get their own color. | On<br>Off | Off | A table is chosen for the heatmap |
| `Missing values` |  | Color | <img src="img/colors/E5E5E5.svg" alt="#E5E5E5" align="absmiddle"> #E5E5E5 | A table is chosen for the heatmap, `Leave missing values empty` is **Off** |
| `Cell width` |  | 2 to 60 px | 14 px | A table is chosen for the heatmap |
| `Cell height` | Share of the row each cell takes. | 0.1 to 1 × row | 0.9 × row | A table is chosen for the heatmap |
| `Space between columns` |  | 0 to 20 px | 1 px | A table is chosen for the heatmap |
| `Distance from the labels` | Space between the labels (or the previous plot) and the heatmap. | 0 to 100 px | 10 px | A table is chosen for the heatmap |
| `Column titles` |  | On<br>Off | On | A table is chosen for the heatmap |
| `Title angle` |  | 0 to 90° | 60° | A table is chosen for the heatmap, `Column titles` is **On**, `Orientation` is not **Vertical** |
| `Title size` |  | 1 to 100 px | 9 px | A table is chosen for the heatmap, `Column titles` is **On** |
| `Title color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 | A table is chosen for the heatmap, `Column titles` is **On** |
| `Show legend` |  | On<br>Off | On | A table is chosen for the heatmap |

## Legends

Placement and look of every legend or scale bar. Hover an element on the canvas and click its lock to move it by hand. `Right-click` it to rewrite its texts.

### › Place

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Vertical position` | Where the legends sit when they are not placed by hand. | Top<br>Bottom | Bottom |  |
| `Horizontal position` | Where the legends sit when they are not placed by hand. | Left<br>Center<br>Right | Left |  |
| `Move sideways` |  | −400 to 400 px | 0 px |  |
| `Move up or down` |  | −400 to 400 px | 0 px |  |

### › Look

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Text size` |  | 1 to 100 px | 10 px |  |
| `Title size` |  | 1 to 100 px | 10 px |  |
| `Bold titles` |  | On<br>Off | On |  |
| `Symbol size` | Size of the symbols relative to the text. | 0.5 to 3× | 1× |  |
| `Space between symbol and text` |  | 0 to 40 px | 8 px |  |
| `Space between rows` |  | 0 to 30 px | 4 px |  |
| `Space between legends` | Space between legends stacked together. | 0 to 60 px | 14 px |  |
| `Text color` |  | Color | <img src="img/colors/333333.svg" alt="#333333" align="absmiddle"> #333333 |  |

## Split into pages

Split a long rectangular tree into pages of the same width, each with a small map of the whole tree.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Pages` | The pages made so far, from top to bottom. | List |  | The tree has pages |
| `Split the rest into pages` | Makes pages for every row that has none. |  |  |  |
| `Split the tree into … pages` | Splits the whole tree into this number of pages. | Number | 2 |  |
| `Save pages as PDF` | One PDF with a page per section. |  |  | The tree has pages |
| `PNG (.zip)`<br>`SVG (.zip)` | One image per page, in a .zip. |  |  | The tree has pages |

### › Look

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Page box on the canvas` | Color of the page frames on screen (for visualization only, they are not exported). | Color | <img src="img/colors/27408B.svg" alt="#27408B" align="absmiddle"> #27408B | **Rectangular** layout, the tree has pages |
| `Repeat the time axis under each page` | Each page gets its own copy of the axis. | On<br>Off | On | **Rectangular** layout, the tree has pages, `Show time axis (dated trees)` is **On** |
| `Include the title, legends and scale bar` | The first page gets the title and the last one the legends and scale bar. | On<br>Off | Off | **Rectangular** layout, the tree has pages |
| `Extra width on the left` | Widens every page to the left, the same for all. | −200 to 600 px | 0 px | **Rectangular** layout, the tree has pages |
| `Extra width on the right` | Widens every page to the right, the same for all. | −200 to 600 px | 0 px | **Rectangular** layout, the tree has pages |

### › Tree map

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Show a map of the whole tree on each page` | A small tree with the rows of the page highlighted. | On<br>Off | On | **Rectangular** layout, the tree has pages |
| `Map width` |  | 20 to 300 px | 60 px | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |
| `Map height` |  | 20 to 600 px | 120 px | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |
| `Space to the tree` | Space between the map and the tree. | 0 to 200 px | 24 px | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |
| `Line width` |  | 0.1 to 10 px | 0.8 px | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |
| `Tree color` |  | Color | <img src="img/colors/BDBDBD.svg" alt="#BDBDBD" align="absmiddle"> #BDBDBD | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |
| `Color of the rows on the page` |  | Color | <img src="img/colors/C8553D.svg" alt="#C8553D" align="absmiddle"> #C8553D | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |
| `Mark the rows on the page with` | How the rows of the page stand out on the map. | Branch color<br>Color and background | `Color of the rows on the page` | **Rectangular** layout, the tree has pages, `Show a map of the whole tree on each page` is **On** |

## Images and visual elements

Pictures (PNG or JPG) placed on the page¹.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Add image` | Places a PNG or JPG on the page, for example a silhouette. |  |  |  |
| `Add label` | A text you can place anywhere, for example a name inside the tree. It moves, aligns with branches, labels and clades, shows distance guides and takes arrows like an image, and is exported as text. `Right-click` it to write it and choose its size, color, bold, italic and typeface. |  |  | A tree is loaded |
| `Add density plot` | A density plot (or histogram) of a value of the tree or of a table, drawn by the app as an image that moves, resizes and aligns like the others. `Right-click` it to choose the values and its look. `Values from` picks the origin: **From tree** (branch lengths and Support values when the nodes have them), **Tree annotations** (such as rates or HPD) or **Attached files** (a column of a table). Its fill can follow the color scale of the branches or of the dots. |  |  | A tree is loaded |
| `Draw arrow` | An arrow to point at something. Drag it by its body, or drag an end onto a node or one of the nine points of an image to anchor it there: when they move, the arrow follows. `Right-click` it for its look. |  |  | A tree is loaded |
| `Image list` | Click a row to select its image. |  |  | An image is added |
| `Replace` | Swaps the picture, keeping its place and width. |  |  | An image is added |
| `Remove` |  |  |  | An image is added |

¹ Drag an image to move it, drag a corner to resize it (proportions are kept), or just outside a corner to rotate it. `Right-click` it for position, size, opacity, rotation, mirror, layer and alignment. On rectangular trees, dotted guides show the distance to the nearest branch, tip label or axis, click a number to type an exact distance. Arrow keys move it 1 px (10 px with Shift). To align it, select the image, `Shift-click` a branch, label or clade, and `Right-click` the image for more options. Alignment works better with rectangular views.

## Page settings

In the **Page settings** menu of the header, next to Export.

Background, palette, color vision preview and plot title.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Background color` |  | Color | <img src="img/colors/FFFFFF.svg" alt="#FFFFFF" align="absmiddle"> #FFFFFF |  |

### › Colors

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Palette`¹ | Colors offered in the menus and for new categories. | Tree2go<br>Okabe-Ito (color blind safe)<br>Paul Tol bright (color blind safe)<br>Viridis (color blind safe)<br>Inferno (color blind safe)<br>Magma (color blind safe)<br>Plasma (color blind safe)<br>Cividis (color blind safe)<br>Turbo<br>Spectral<br>Blue to red (color blind safe) | Tree2go |  |
| `Preview as seen with` | Shows the figure as seen with a color vision deficiency, on screen only. | Normal vision<br>Deuteranopia (red-green)<br>Protanopia (red-green)<br>Tritanopia (blue-yellow)<br>No color (grayscale) | Normal vision |  |

¹ The colors offered in the menus and for new categories (colors already in use do not change).  

### › Plot title

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `Text` |  | Text |  |  |
| `Size` |  | 4 to 300 px | 18 px | `Text` is set |
| `Vertical position` |  | Top<br>Bottom | Top | `Text` is set |
| `Horizontal position` |  | Left<br>Center<br>Right | Left | `Text` is set |
| `Move sideways` |  | −400 to 400 px | 0 px | `Text` is set |
| `Move up or down` |  | −400 to 400 px | 0 px | `Text` is set |
| `Bold` |  | On<br>Off | On | `Text` is set |
| `Italic` |  | On<br>Off | Off | `Text` is set |
| `Color` |  | Color | <img src="img/colors/1F1F1F.svg" alt="#1F1F1F" align="absmiddle"> #1F1F1F | `Text` is set |

## Export

In the **Export** menu of the header.

Save the figure, the tree or a style template.

| Option&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Values&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Appears&nbsp;when&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:---|:---|:---|:---|:---|
| `SVG`<br>`PDF` | Vector files that stay sharp at any size. |  |  |  |
| `PNG`<br>`TIFF` | Images at the chosen resolution. |  |  |  |
| `Resolution` |  | 36 to 2400 dpi | 300 dpi |  |
| `Units` |  | px<br>cm<br>in | px |  |
| `Width`<br>`Height` | Final size of the figure, changing one keeps the proportions. |  | Natural size |  |
| `Save Newick` | The tree as it is now: names, rooting, order. |  |  |  |
| `Save NEXUS` | Same tree, with branch colors for FigTree and its annotations. |  |  |  |
| `Save style…` | Saves the look of the figure, without its tree or data. |  |  |  |
| `Apply a style…` | Gives a saved look to the current tree. |  |  |  |
| `Reset visual settings` | Back to the default look (names, lengths, collapsed clades, clade names, fossils and tables are kept). |  |  |  |

## Right-click menus

`Right-click` any element (on a Mac: `Control-click`) to edit just that element, or everything selected. Values set here win over the panel, the small ↶ next to a field returns it to the left-panel value. The left-panel shows how many elements use their own value, with a button to undo them all.

| Element&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | What you can change&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|---|---|
| Branch | Color, width, line style, branch length label, grafting a fossil, reroot here, extract clade, make a page, copy Newick, delete |
| Clade | Clade color, highlight background (opacity, start at root, stem or crown, end, gradient, corners), collapse, rotate, ladderize, height and fill when collapsed, clade name bar |
| Tip label | Font size, color, style, weight, open nomenclature qualifiers (cf., aff., sp.), extinct tip |
| Node | Dot size, shape, fill, color and border, support label, other node labels, node bars |
| Grafted fossil | Ages, split the lineage, add fossils to a split, delete |
| Clade name bar | Name, color, sizes, on circular trees, the name along the arc |
| Legend | Title and entry texts, look of that legend, alignment with a selection |
| Scale bar | Length, unit, sizes, color, alignment |
| Page box | Rows of the page, look of its tree map, alignment |
| Image | Position, size, opacity, rotation, mirror, layer, alignment |
| Label | Text, size, color, bold, italic, typeface, opacity, rotation, mirror, layer, alignment |
| Density plot | Values from (From tree, Tree annotations or Attached files) and Value, logarithmic scale (base 10), cut below and above (where the curve stops, since a density spills past the data, density curve shown or hidden, histogram with its bin width (empty for automatic, in log₁₀ units with the logarithmic scale), color and opacity, smoothing, one color or the colors of the branches or dots (offered only when they are colored by the same values the plot shows, and also applied to the histogram), fill and opacity, line color, width and style, axis with its color, width, text size, spacing and title |
| Arrow | Color, width, opacity, line style, arrow heads and their size, curvature, space from the anchor at each end, free an anchored end, delete |
| Reticulation | Color, width, arrows and their size, straight or curved line, where it starts and ends along its branches, show its value |
| Value of a reticulation | Text size, color, horizontal and vertical offset |
| Major edge (Full network) | Color, width |
| Value of the major edge | Text size, color, horizontal and vertical offset |
| Any element | Copy style, paste style, reset style |

## On the canvas

| Action&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | How&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|---|---|
| Select | Click an element (`Shift-click` to add more) |
| Select mode | Element (single)<br>Clade (`Shift-click` extends the selection to the most recent common ancestor)<br>MRCA (pick two tips) |
| Find tips | Type a name or a pattern with * and ? (`Enter` selects the matches, `Shift+Enter` their clade) |
| Info on hover | Button at the bottom of the panel: tips, branch length and support of the branch under the mouse |
| Move a legend, the scale bar or a page tree map | Hover it and click its lock, then drag it, arrow keys move it 1 px (10 px with `Shift`) |
| Zoom and move | Mouse wheel to zoom, drag the empty canvas to move, buttons at the bottom right to fit |
| Tabs | Extract clade (`Right-click` menu of a clade) opens the clade in a new tab, with the same style. Supports, ages and frequencies come from the full tree as they were, and the clade keeps its own branch to show them. Click a tab to switch, double-click it to rename it, the × of the active tab closes it. The tab of the full tree cannot be closed |
| Undo<br>Redo | `Ctrl+Z`<br>`Ctrl+Shift+Z` (`Cmd+Shift+Z` on a Mac) |
| Clear the selection | `Esc` |
