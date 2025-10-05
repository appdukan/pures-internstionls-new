# Pures International Website - AI Coding Instructions

## Project Overview
This is a vanilla HTML/CSS/JavaScript website for Pures International, an agricultural export company. The site showcases products like spices, fruits, vegetables, and dehydrated foods with a focus on premium quality and global reach.

## Architecture & Tech Stack
- **Pure Vanilla Stack**: No frameworks - HTML5, CSS3, vanilla JavaScript only
- **Single-file Structure**: Each page is a standalone HTML file with shared CSS/JS assets
- **Component-based CSS**: Modular styles with CSS variables for design system consistency
- **Animation Framework**: Custom animation system in `css/animations.css` with intersection observers

## Key Files & Structure
```
├── index.html              # Homepage with hero slider and stats
├── [about|products|services|contact|blog].html
├── css/
│   ├── style.css          # Main styles with CSS variables design system
│   └── animations.css     # Custom animation framework
├── js/
│   ├── main.js           # All functionality in single file (~2800 lines)
│   └── product-enhancements.js  # Product card animations
├── images/               # Organized by functionality (hero/, product_type_*, etc.)
├── schema.json          # Structured data for SEO
└── manifest.json        # PWA configuration
```

## Design System & Conventions

### CSS Variables (`:root` in style.css)
- **Colors**: Light cool palette with `--primary-green: #86efac`, `--primary-blue: #7dd3fc`
- **Typography**: Poppins font with weight variables (`--font-weight-*`)
- **Spacing**: Consistent scale (`--spacing-xs` to `--spacing-4xl`)
- **Shadows**: Predefined levels (`--shadow-sm` to `--shadow-2xl`)

### Animation Classes
- `.animate-fade-in-up`, `.animate-fade-in-left` for scroll animations
- `.delay-*` classes for staggered animations (200ms increments)
- Custom keyframes in `animations.css` with intersection observer triggers

### Product Categories
Products use `data-category` attributes with predefined icons in `product-enhancements.js`:
```javascript
const categoryIcons = {
    'spices': 'fas fa-pepper-hot',
    'fruits': 'fas fa-apple-alt',
    'vegetables': 'fas fa-carrot',
    // ... etc
};
```

## JavaScript Architecture

### Main.js Structure
- **Initialization**: `DOMContentLoaded` event initializes ~15 component functions
- **Component Pattern**: Each feature has its own `init*()` function (e.g., `initHeroSlider()`, `initProductFilters()`)
- **Performance**: Debounced scroll events, lazy loading, `will-change` optimizations
- **Animation System**: Intersection observers for scroll animations with cleanup

### Key Functions to Understand
- `initScrollAnimations()`: Handles `.animate-*` class triggers
- `initHeroSlider()`: Auto-advancing image slider with navigation
- `initProductFilters()`: Category filtering with search functionality
- `enhanceProductCards()`: Adds icons and scroll animations to product cards

## Critical Development Patterns

### Adding New Pages
1. Copy existing HTML structure (navigation, page-header, footer)
2. Update active nav link: `<a href="page.html" class="nav-link active">`
3. Add page-specific initialization in `main.js`
4. Update meta tags and OpenGraph data

### Animation Implementation
```javascript
// Standard pattern for scroll animations
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('is-visible');
            observer.unobserve(entry.target);
        }
    });
}, { threshold: 0.1 });
```

### CSS Component Structure
```css
/* Component block */
.component-name {
    /* base styles */
}

/* Element */
.component-name__element {
    /* element styles */
}

/* Modifier */
.component-name--modifier {
    /* variant styles */
}
```

## Image Organization
- `images/hero_section_images/`: Hero slider backgrounds (612x612px format)
- `images/product_type_*/`: Product images organized by category
- `images/all_certificats/`: Company certification badges
- Each folder includes `image_summary.txt` documenting contents

## SEO & Performance
- **Structured Data**: Complete schema.org markup in `schema.json`
- **Lazy Loading**: Intersection observer-based image loading
- **PWA Ready**: `manifest.json` configured for standalone app experience
- **Meta Tags**: Each page has complete OpenGraph and SEO meta data

## Common Gotchas
- All animations require both CSS class AND intersection observer setup
- Product cards need `data-category` attribute for proper icon assignment
- Hero slider images should be 612x612px for consistency
- Font Awesome 6.5.0 is used - verify icon availability before use
- CSS variables must be defined in `:root` to work across components

## Testing & Debugging
- Use browser dev tools' Animation panel for performance debugging
- Check intersection observer behavior with `console.log` in observer callbacks
- Validate responsive design at breakpoints: 768px (tablet), 1024px (desktop)
- Test hero slider auto-advance (5-second intervals) and manual navigation