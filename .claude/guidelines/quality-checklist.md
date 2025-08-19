# Quality Checklist

Comprehensive quality assurance checklist for AI-assisted development across all technologies.

## General Code Quality
- [ ] **Functionality**: Preserved (unless intentionally changing)
- [ ] **Testing**: Behavior verified through testing
- [ ] **Breaking changes**: Documented and approved
- [ ] **Compatibility**: Backwards compatibility maintained or migration path provided
- [ ] **Structure**: Code structure readable with logical organization

## Python Development
- [ ] **Virtual environment**: Verified (`echo $VIRTUAL_ENV`)
- [ ] **Formatting**: Code formatted with `black` and `isort`
- [ ] **Naming**: PEP 8 naming standards followed
- [ ] **Error handling**: EAFP principle applied
- [ ] **Libraries**: Library choices justified
- [ ] **Functions**: Single-purpose and composable
- [ ] **Error handling**: Proper error handling implemented
- [ ] **Comments**: Explain why, not what

## Web UI/Frontend Development
- [ ] **Rendering**: Server-side rendering first
- [ ] **Enhancement**: Progressive enhancement with Alpine.js/HTMX
- [ ] **Styling**: Tailwind CSS utility-first styling
- [ ] **Theme**: Dark theme implemented (GitHub Dark or Everforest)
- [ ] **Assets**: CDN assets used
- [ ] **Accessibility**: Considered (keyboard nav, ARIA, screen readers)
- [ ] **Responsive**: Desktop-first responsive design

## Git Practices
- [ ] **Branching**: Feature branch used (never develop on main)
- [ ] **Frequency**: Appropriate commit frequency
- [ ] **Squashing**: Squash workflow followed (reset method, not interactive rebase)
- [ ] **Messages**: Adequately detailed commit messages used
- [ ] **Co-authorship**: Included `Co-authored-by: [AI Model Name] <AI Model Email>`
- [ ] **History**: Clean history maintained

## Claude Code Integration
- [ ] **Configuration**: Appropriate settings hierarchy used
- [ ] **Permissions**: Tool permissions properly configured
- [ ] **Commands**: Custom slash commands documented and functional
- [ ] **Hooks**: Automation hooks configured where beneficial
- [ ] **Status line**: Relevant project information displayed

## Security & Safety
- [ ] **Secrets**: No secrets or keys exposed in code or logs
- [ ] **Permissions**: Minimal necessary permissions granted
- [ ] **Dependencies**: Third-party libraries vetted and justified
- [ ] **Input validation**: User inputs properly validated
- [ ] **Error handling**: Sensitive information not leaked in error messages