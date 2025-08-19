# Web UI/Frontend Development Guidelines

Guidelines for modern web frontend development with server-side rendering focus.

## Architecture
- **Rendering**: Server-side rendering first with progressive enhancement
- **Assets**: CDN assets over local bundling
- **Standards**: Follow HTML5, CSS3, and accessibility standards

## JavaScript Preferences
- **Alpine.js**: Client-side interactivity and component behavior
- **HTMX**: Server interactions, partial updates, real-time features
- **Complementary usage**: Alpine for UI state, HTMX for server communication

## Styling
- **Framework**: Tailwind CSS utility-first
- **Theme**: Dark, professional, developer-friendly palettes
- **Responsive**: Desktop-first for developer tools
- **Custom CSS**: Minimal, leverage Tailwind utilities

## Color Palettes

### GitHub Dark
Professional theme based on GitHub's Primer design
- **Backgrounds**: Canvas (#0d1115), Secondary (#21262d), Tertiary (#161b22)
- **Text**: Primary (#f0f6fc), Secondary (#8b949e), Muted (#656d76)
- **Syntax**: Red (#f85149), Orange (#ffa657), Yellow (#d29922), Green (#3fb950), Blue (#79c0ff), Purple (#d2a8ff)
- **Semantic**: Success (#3fb950), Warning (#d29922), Danger (#f85149)
- **Accent**: Link (#58a6ff), Focus (#1f6feb)

### Everforest
Warm, eye-friendly theme with natural harmony
- **Backgrounds**: Canvas (#101115), Secondary (#21262d), Tertiary (#161b22)
- **Text**: Primary (#f0f6fc), Secondary (#8b949e), Muted (#656d76)
- **Syntax**: Red (#e67e80), Orange (#e69875), Yellow (#dbbc7f), Green (#a7c080), Blue (#79c0ff), Purple (#a173f0)
- **Semantic**: Success (#a7c080), Warning (#dbbc7f), Error (#e67e80)
- **Accent**: Link (#58a6ff), Focus (#4a90e2)

## Quality Checklist
- [ ] **Rendering**: Server-side rendering first
- [ ] **Enhancement**: Progressive enhancement with Alpine.js/HTMX
- [ ] **Styling**: Tailwind CSS utility-first styling
- [ ] **Theme**: Dark theme implemented (GitHub Dark or Everforest)
- [ ] **Assets**: CDN assets used
- [ ] **Accessibility**: Considered (keyboard nav, ARIA, screen readers)
- [ ] **Responsive**: Desktop-first responsive design