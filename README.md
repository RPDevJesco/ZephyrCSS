# ZephyrCSS - An unapologetically Opinionated yet not restrictive Semantic Design Framework

A comprehensive, semantic color system that scales from 1 essential color to 10 extended colors, providing everything you need for modern web interfaces.

## ✨ What's New in v2.0

### OKLCH Color Foundation
ZephyrCSS now uses the modern OKLCH color space as its foundation, providing:
- **Perceptually uniform colors** - More natural color transitions
- **Better dark mode support** - Automatic lightness inversion
- **Enhanced color manipulation** - Precise control over hue, chroma, and lightness
- **Future-proof architecture** - Built on cutting-edge CSS standards

### Semantic Aliases
Use intent-based names alongside priority-based names:
```css
/* Both work! */
--success: var(--quinary);     /* Semantic name */
--quinary: /* ... */;          /* Priority name */
```

### Multi-Theme Support
Switch between multiple pre-built themes at runtime:
```html
<html data-theme="enchanted-forest">  <!-- Default -->
<html data-theme="ocean-breeze">      <!-- Cool blues -->
<html data-theme="sunset-warmth">     <!-- Warm sunset -->
<html data-theme="lively-spring">     <!-- Fresh greens -->
<html data-theme="monochrome-pro">    <!-- Professional grayscale -->
```

### Automatic Dark Mode
Respects system preferences with `prefers-color-scheme: dark` - no configuration needed!

## 🎨 Philosophy: Visual Harmony Over Logical Order

One of the key insights in developing this framework was discovering that **visual harmony doesn't always follow logical color order**. When building color palettes, the temptation is to arrange colors in a sequential, logical progression. However, we found that creating truly harmonious palettes requires a more thoughtful approach to color relationships.

### The "Enchanted Forest Hues" Discovery

Our current palette demonstrates this principle perfectly:

```css
/* Core Colors (1-5) */
--primary:   #264653; /* Deep teal - Background layer */
--secondary: #E9C46A; /* Warm yellow - Foreground/surface layer */
--tertiary:  #287271; /* Teal green - Borders/structure layer */
--quaternary:#EFB366; /* Soft orange - Accent layer */
--quinary:   #2A9D8F; /* Aqua green - Emphasis layer */

/* Extended Colors (6-10) */
--senary:    #F4A261; /* Coral orange - Utility overlay */
--septenary: #8AB17D; /* Sage green - Danger/warning */
--octonary:  #EE8959; /* Burnt orange - Info states */
--nonary:    #BABB74; /* Olive green - Neutral accent */
--denary:    #E76F51; /* Terra cotta - Text anchor */
```

Instead of following a strict chromatic progression, these colors were selected for their **harmonic relationships** and **practical usability** across different interface contexts. The result is a palette that feels cohesive and natural, rather than mechanical.

## 🏗️ Architecture

### Modern OKLCH Foundation

ZephyrCSS v2.0 is built on OKLCH (Oklab Lightness Chroma Hue), providing superior color manipulation:

```css
/* Instead of hex values: */
--primary: #264653;

/* We now define components: */
--primary-l: 35%;    /* Lightness */
--primary-c: 0.05;   /* Chroma (saturation) */
--primary-h: 196;    /* Hue (0-360) */
--primary: oklch(var(--primary-l) var(--primary-c) var(--primary-h));
```

**Benefits:**
- **Dark mode**: Simply invert lightness values automatically
- **Consistency**: Perceptually uniform color space
- **Control**: Adjust saturation globally by tweaking chroma
- **Predictability**: More intuitive color relationships

### Dual-Mode System

The framework operates in two modes:

- **5-Color Mode** (Default): Essential functional colors for core UI needs
- **10-Color Mode** (Extended): Full semantic palette for complex applications

Toggle between modes using the `data-palette` attribute:

```html
<!-- 5-color mode -->
<html data-palette="5">

<!-- 10-color mode -->
<html data-palette="10">
```

### Theme System

Switch between pre-built themes or create your own:

```html
<!-- Use a pre-built theme -->
<html data-theme="ocean-breeze" data-palette="10">

<!-- Or use default theme -->
<html data-palette="10">
```

**Available Themes:**
- `enchanted-forest` (default) - Earthy teal and warm accents
- `ocean-breeze` - Cool blues with aqua accents
- `sunset-warmth` - Warm sunset purples and oranges
- `lively-spring` - Fresh spring greens
- `monochrome-pro` - Professional grayscale with subtle blue undertones

### Color Hierarchy & Semantic Roles

ZephyrCSS uses **priority-based naming** (Primary → Denary) where colors are ordered by visual prominence, not chromatic sequence. This represents "most visible → least visible" in typical UI layouts.

#### Core Colors (1-5)
1. **Primary** - Main background layer, foundational UI elements
2. **Secondary** - Foreground/surface accent, elevated content
3. **Tertiary** - Borders/structure, form elements, dividers
4. **Quaternary** - Calm accent, secondary actions, info states
5. **Quinary** - Emphasis/positive tone, CTAs, success states

#### Extended Colors (6-10)
6. **Senary** - Utility overlay, tooltips, helper content
7. **Septenary** - Danger/warning states, destructive actions
8. **Octonary** - Info states, notifications, guidance
9. **Nonary** - Neutral accent, pending states, subtle emphasis
10. **Denary** - Text anchor, readable text on light backgrounds

### Semantic Aliases (New in v2.0!)

Use intent-based names for better code readability:

```css
/* Priority-based (original) */
--quinary: oklch(60% 0.10 175);
--septenary: oklch(65% 0.09 130);
--octonary: oklch(68% 0.16 40);
--nonary: oklch(70% 0.08 95);

/* Semantic aliases (new) */
--success: var(--quinary);
--danger: var(--septenary);
--info: var(--octonary);
--warning: var(--nonary);
--neutral: var(--tertiary);
--accent: var(--quaternary);
```

**Use whichever naming makes sense for your context:**
```css
/* Both are valid! */
.alert-success { background: var(--bg-success-base); }
.alert-success { background: var(--bg-quinary-base); }
```

#### Using a 1 to 3 color palette

Since each core color from primary to denary have a designated role, the hard requirement colors are primary through tertiary.
```css
/* Core Colors (1-3) */
--primary:    #264653; /* Deep teal - Background layer */
--secondary:  #E9C46A; /* Warm yellow - Foreground/surface layer */
--tertiary:   #287271; /* Teal green - Borders/structure layer */
--quaternary: transparent; /* Accent layer */
--quinary:    transparent; /* Emphasis layer */

/* Extended Colors (6-10) */
--senary:    transparent /* Utility overlay */
--septenary: transparent; /* Danger/warning */
--octonary:  transparent; /* Info states */
--nonary:    transparent; /* Neutral accent */
--denary:    transparent; /* Text anchor */
```

## 🎯 Color Variations System

Each color automatically generates a complete set of variations using CSS `color-mix()`:

### Tints (Lighter variations)
- `--{color}-tint` - 12% white mix
- `--{color}-tint-light` - 25% white mix
- `--{color}-highlight` - 44% white mix
- `--{color}-subtle` - 60% white mix

### Shades (Darker variations)
- `--{color}-shade` - 20% black mix
- `--{color}-shade-deep` - 35% black mix
- `--{color}-depth` - 50% black mix
- `--{color}-shadow-tint` - 70% black mix

Example usage:
```css
.card {
    background: var(--bg-primary-subtle);
    border: 1px solid var(--border-primary-subtle);
    box-shadow: var(--elevation-primary-sm);
}

.card:hover {
    background: var(--bg-primary-hover);
    border-color: var(--border-primary-light);
    box-shadow: var(--elevation-primary-md);
}
```

## 🛠️ Component Integration

### Background System
- `--bg-{color}-base` - Base background color
- `--bg-{color}-hover` - Hover state background
- `--bg-{color}-active` - Active state background
- `--bg-{color}-subtle` - Subtle background variant
- `--bg-{color}-disabled` - Disabled state background

### Border System
- `--border-{color}-base` - Standard border
- `--border-{color}-light` - Light border variant
- `--border-{color}-subtle` - Subtle border
- `--border-{color}-strong` - Strong border emphasis

### Text System
- `--text-on-{color}` - High contrast text on colored backgrounds
- `--text-on-{color}-muted` - Muted text on colored backgrounds

### Interactive States
- `--focus-ring-{color}` - Focus ring for accessibility
- `--hover-overlay-{color}` - Hover overlay effects
- `--elevation-{color}-{size}` - Colored shadow variations

## 📁 File Structure

```
ZephyrCSS/
├── css/
│   ├── token_oklch.css        # OKLCH color foundation (NEW)
│   ├── themes.css             # Pre-built theme system (NEW)
│   ├── semantic_aliases.css   # Intent-based color names (NEW)
│   ├── token.css              # Legacy hex color definitions (maintained)
│   ├── color_token.css        # Color overrides & mode switching
│   ├── color_tints_shades.css # Automatic color variations
│   ├── colors.css             # Complete component color system
│   ├── layout.css             # Layout utilities & grid system
│   └── site.css               # Main import file with layer architecture
└── index.html                 # Complete showcase & documentation
```

### Import Order & Layers

The framework uses CSS `@layer` for organized customization:

```css
@layer themes, semantic-aliases, override, dual;

1. token_oklch.css     → OKLCH foundation
2. themes.css          → Named theme variants
3. semantic_aliases.css → Intent-based names
4. token.css           → Legacy compatibility (layer: dual)
5. color_token.css     → Color overrides
6. color_tints_shades.css → Variations
7. colors.css          → Component tokens
8. layout.css          → Layout system
```

## 🚀 Quick Start

1. **Include the framework:**
```html
<link rel="stylesheet" href="css/site.css">
```

2. **Set your preferred mode and theme:**
```html
<html data-palette="10" data-theme="enchanted-forest">
<!-- Palette: "5" or "10" -->
<!-- Theme: "enchanted-forest", "ocean-breeze", "sunset-warmth", etc. -->
```

3. **Use semantic color classes (now with aliases!):**
```html
<!-- Cards with priority-based names -->
<div class="card card-primary p-6">
    <h3>Primary Content</h3>
    <button class="btn btn-emphasis">Action</button>
</div>

<!-- Status alerts with semantic names -->
<div style="background: var(--bg-success-base)">Success message</div>
<div style="background: var(--bg-danger-base)">Error message</div>
<div style="background: var(--bg-warning-base)">Warning message</div>
<div style="background: var(--bg-info-base)">Info message</div>

<!-- Both naming conventions work -->
<button style="background: var(--quinary)">Success Button</button>
<button style="background: var(--success)">Success Button (same!)</button>
```

4. **Dark mode works automatically:**
```css
/* No configuration needed! */
/* Framework respects prefers-color-scheme: dark */
```

## 🎨 Real-World Usage Examples

### Card Components
```css
.feature-card {
    background: var(--bg-secondary-subtle);
    border: 1px solid var(--border-secondary-subtle);
    border-radius: var(--x-radius);
    padding: 1.5rem;
    transition: var(--x-transition);
}

.feature-card:hover {
    background: var(--bg-secondary-hover);
    transform: var(--motion-hover);
    box-shadow: var(--elevation-secondary-md);
}
```

### Interactive Buttons
```css
.cta-button {
    background: var(--bg-quinary-base);
    color: var(--text-on-quinary);
    border: 1px solid var(--border-quinary-base);
    padding: 0.75rem 1.5rem;
    border-radius: var(--x-radius);
}

.cta-button:hover {
    background: var(--bg-quinary-hover);
    transform: var(--motion-hover);
}

.cta-button:focus {
    outline: none;
    box-shadow: var(--focus-ring-quinary);
}
```

### Form Elements
```css
.themed-input {
    background: var(--bg-tertiary-highlight);
    border: 1px solid var(--border-tertiary-base);
    color: var(--text-on-tertiary);
    padding: 0.75rem;
    border-radius: var(--x-radius);
}

.themed-input:focus {
    border-color: var(--border-quaternary-base);
    box-shadow: var(--focus-ring-quaternary);
}
```

## 🎯 Color Selection Guidelines

### When choosing colors for your own palette:

1. **Test harmonic relationships** - Colors should feel naturally related, not just logically sequential
2. **Consider practical usage** - Each color needs to work across different UI contexts (backgrounds, text, borders)
3. **Validate accessibility** - Ensure sufficient contrast ratios for text readability
4. **Test at scale** - View colors in actual interface contexts, not just as swatches
5. **Prioritize cohesion** - A smaller palette that works harmoniously is better than a large palette that feels disjointed

### The "Coolors.co Row Method"

Our discovery process involved using tools like Coolors.co, but instead of taking colors in sequential order, we:

1. Generated multiple palette variations
2. Mixed and matched colors from different rows
3. Tested combinations in real interface contexts
4. Selected based on visual harmony rather than tool-suggested order

This approach led to the much more cohesive "Enchanted Forest Hues" palette we use today.

## 🔧 Customization

### Creating Your Own Theme

With the new theme system, creating custom themes is easier:

```css
/* In themes.css or your own override file */
@layer themes {
    :root[data-theme="my-brand"] {
        /* Define OKLCH components */
        --primary-l: 40%;
        --primary-c: 0.12;
        --primary-h: 280;
        
        --secondary-l: 75%;
        --secondary-c: 0.15;
        --secondary-h: 50;
        
        /* ... define all 10 colors */
    }
}
```

Then use your theme:
```html
<html data-theme="my-brand" data-palette="10">
```

### Creating Your Own Palette (Legacy Method)

To adapt this framework with your own colors using the legacy system:

1. **Replace the color values** in `color_token.css`
2. **Maintain the semantic structure** (don't change the variable names)
3. **Test all variations** using the included showcase page
4. **Validate accessibility** with tools like WebAIM Color Contrast Checker

### Advanced Customization with OKLCH

Fine-tune colors by adjusting individual components:

```css
/* Increase saturation across all colors */
:root {
    --primary-c: calc(var(--primary-c) * 1.2);
    --secondary-c: calc(var(--secondary-c) * 1.2);
}

/* Create custom dark mode lightness values */
@media (prefers-color-scheme: dark) {
    :root {
        --primary-l: 70%;  /* Lighter in dark mode */
        --secondary-l: 40%; /* Darker in dark mode */
    }
}
```

### Extended Customization

The framework is designed to be modular. You can:

- Create new themes in `themes.css`
- Add semantic aliases in `semantic_aliases.css`
- Modify tint/shade percentages in `color_tints_shades.css`
- Add new component variations in `colors.css`
- Extend the layout system in `layout.css`
- Override at specific layers using `@layer override`

## 🎭 Examples & Showcase

The included `index.html` file provides a comprehensive showcase of:

- All 10 colors in action
- Real-world component examples
- Interactive state demonstrations
- Form element variations
- Complete color palette visualization
- 5-color vs 10-color mode comparisons

Visit the showcase to see the framework in action and understand how each color works in context.

## 🤝 Philosophy & Best Practices

This framework embodies several key principles:

1. **Semantic over Arbitrary** - Colors have meaning and purpose, not just aesthetic value
2. **Harmony over Logic** - Visual relationships matter more than systematic ordering
3. **Scalability** - Works for simple 5-color needs and complex 10-color systems
4. **Accessibility First** - Built with contrast and usability in mind
5. **Real-World Tested** - Every color works in actual interface contexts
---

**Remember**: Great color systems aren't just about having the right colors—they're about having colors that work beautifully together in the real world. Visual harmony trumps logical order every time.
