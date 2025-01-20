## &#10162; CSS Methodology:

It describes the set of guidelines for writing a maintainable and scalable CSS code. It improves overall readability of project.

### &#9780; Overview:
1. [BEM](#-bem)
2. [SMACSS](#-smacss)

### &#10022; BEM:

BEM stands for Block, Element, Modifier. It is primarily used for creating the reusable and maintainable CSS components.

- **Naming Convention:**
	- **Block:** A standalone block or entity (e.g., `.card`).
	- **Element:** A child of a block or entity (e.g., `.card__title`, `.card__image`).
	- **Modifier:** A variation of a block or element (e.g., `.card--primary`, `.button--primary`).

### &#10022; SMACSS:

SMACSS stands for Scalable and Modular Architecture for CSS. It recommends to categorizing CSS rules into five distinct groups. Divide the style into these groups as separate SASS style. Which will be easier to maintain and improves readability. 

- **Groups:**
	- **Base:** Basic styles like resets, typography, and normalization.
  - **Layout:** Styles for sections with grids, containers, and positioning.
  - **Module:** Reusable component styles like heading, buttons and colors.
  - **State:** Styles for different states of a component like active, focus and hover.
  - **Theme:** Styles for different themes like light and dark.

---
[&#8682; To Top](#-css-methodology)

[&#10094; Previous Topic](./performance-optimization.md)

[&#8962; Goto Home Page](../README.md)