# Comigo's CSS naming guide

My naming guide for CSS.

## Goals

Keep CSS:

1. simple,
2. readable,
3. predictable,
4. easy to use and code,
5. concise and sufficient,
6. modular,
7. extendable.

## The guide

The guide is built on the idea of *semantic classes*, *containers*, *modifiers*, *junctions*, and *mimics*, and defines the relations between each other and between them and HTML tags/web components. The guide doesn't cover the use of pseudoselectors or entities outside of *semantic classes*, *containers*, *modifiers*, *junctions*, *mimics* group.

### Definitions

1. **Semantic classes** start with `a` (or `an`) and follow the `camelCase` pattern: `aButtonGroup`, `aCard`, `aFeature`, `anInfoBox`. A semantic class is applied to describe a custom block built upon existing HTML tags or custom elements (aka web components).
1. **Containers** for a collection of other entities with semantic classes follow the `PascalCase` pattern, and name items in pluralForm: `Cards`, `MenuItems`, `Features`. These classes imply that certain semantic classes exist. (`.aCard`, `aMenuItem`, `aFeature`.)
    * Some entities are… particularly amusing in English and describe a semantic class instead of a container. For example, `News` and `Docs`.
1. **Modifiers** follow the `lowercase` pattern. A modifier is a class that is applied to tweak the appearance of arbitrary tags, be they bare HTML tags or blocks with semantic classes/container classes. Examples:
    * Font size modifiers: `.small`, `.large`.
    * Generic color modifiers, plus those that add semantic meaning with color: `.red`, `.orange`, `.blue`, `.error`, `.warn`, `.info`.
    * Layout tweaks: `nomarginleft`, `nopaddingright`, `inlineblock`, `block`.
    * Visibility flags: `hide`, `show`.
    * Semantic modifiers: `.secondary`, `.primary`.
    * State descriptors: `.active`, `.selected`, `.disabled`, `.removed`.
1. **Junctions** are CSS rules that target specific elements that may exist in the described form (in its visual state and behavior) only inside specific parents.  They are written as two or more class names/web component names joined with a hyphen (`-`). A parent must be either an element with a *semantic class* or a web component. A child must be either a *container* or a *semantic class*.
    * For example, you may want to describe an icon inside `.aDownload` blocks. The style for this icon is unique and is not used elsewhere, and shouldn't be reused outside of `.aDownload` blocks. You create `.aDownload-anIcon` class.
    * You may also have controls inside custom input elements: `.curve-editor-aNode`, `.docs-panel-aSearchForm`, `texture-generator-aPreviewImage`.
1. **Mimics** are rules that target classes which names match the names of specific HTML tags to style arbitrary elements so that they match the look of real HTML tags. Examples: 
    * `.h1`, `.h2`, `.h3`, and others that make an element look like a heading.
    * `.button` that is applied to `a` elements to make them look like a button.

### Rules

1. A rule with a *junction* may have a descendant combination only if the *junction* is a parent, or if the *junction* is preceded by the parent part of this junction + a modifier. Examples of selectors:
    * `.curve-editor.compact .curve-editor-aNode`.
    * `.aModal.fullscreen .aModal-aFooter`.
    * `.texture-generator-aPreviewImage button`.
    * but not `.aModal .aModal-aFooter` (redundant) and not `.aModal .aDownload-anIcon` (not modular).
1. *Semantic classes* and *containers* may change their appearance if certain *modifiers* are applied.
    * Example: `.anInfoBox` has blue borders and pale blue background, with dark text color. `.red` and `.error` make any text red. There may exist a rule with `.anInfoBox.red, .anInfoBox.error` selector that also changes background and border color to shades of red.
    * Another example: a *container* `.Downloads` exists. There may be a rule with a selector `.Downloads.compact` that provides a denser layout.
1. *Modifiers* must not match HTML tag names.
1. *Mimics* must match HTML tag names.

### Recommendations
1. Before everything, define the look and feel of HTML elements, then switch to classes.
1. Minimize the usage of *mimics*. They pollute other classes and thus are prone to errors.
1. Avoid the usage of IDs in CSS. IDs are intended to be unique and restrict the reusability of styles.
    * If you do use them, IDs must start with `the` and follow the `camelCase`, e.g. `theHomeButton`, `theTopLeftLogo`.
1. Firstly define the effect of usage of *modifiers* on all elements (e.g. `.small`), then define their effect on semantic classes, containers, and others (e.g. `.aModal.small`, `.Downloads.small`).
