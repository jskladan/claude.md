# Core Development Guidelines

Guidelines for AI-assisted development ensuring consistent, maintainable, and high-quality code.

## Target Audience & Communication Style

**Target audience**: Experienced software engineers and technical leads

**Communication style**:
- Technical precision with concise explanations
- Professional tone between technical peers
- Assume competence, no hand-holding
- Offer feedback and challenge assumptions when appropriate

**Solution preferences**:
- Favor standard library and widely adopted third-party libraries
- Leverage third-party libraries before creating a custom solution. Always provide a quick summary of the benefits.
- Progressive refinement: start simple, refactor to establish the final solution

## Core Workflow

1. **Plan first**: Describe changes, approach, and architectural decisions before coding
2. **Clarify requirements** when unclear
3. **Wait for approval** before making any code changes
4. **Build minimal viable solutions first**
5. **Reflect post-implementation**: Analyze readability/maintainability
6. **Recommend improvements** when code becomes unwieldy

## Instruction Priority Hierarchy

When conflicting guidance exists, follow this precedence order:

1. **Explicit user instruction** - Direct commands override all guidelines
2. **Context-specific triggers** - User language like "final", "ready", "WIP" indicates intent
3. **Domain guidelines** - Language/tool-specific best practices
4. **Core principles** - General development and communication guidelines
5. **Default assumptions** - Fall back to framework defaults when uncertain

### Examples
- User says "create final commit" → Use concise style (overrides development phase defaults)
- User requests `/commit dev` → Use verbose style (explicit instruction takes precedence)
- User mentions "WIP changes" → Use verbose style (context trigger detected)

## Code Standards

### Comments
- Explain why, not what
- Do not add, and feel free to remove, basic explanations of what code does
- Focus on context: non-obvious decisions, architectural reasoning, gotchas

### Development Principles
- Prefer streamlined code over complex interconnected classes
- Use composition over inheritance
- Single-purpose functions that are clear and composable
- Consistent naming conventions following language standards
- Readable code structure with logical organization

## Testing & Verification

- **Verification**: Always verify behavior before completion
- **Simple changes**: Interactive testing for simple changes
- **Complex problems**: Temporary test files (delete after use)
- **Coverage**: Test edge cases and boundary conditions

## Refactoring

### Trigger Patterns
- **Excessive nesting**: Extract functions
- **Large functions**: Break down functions >30-40 lines
- **Global state overuse**: Convert to class attributes
- **Complex conditionals**: Use polymorphism/strategy patterns
- **Deep inheritance**: Apply mixins/composition

### Process
1. **Preserve functionality**: Maintain all functionality unless explicitly instructed otherwise
2. **Plan first**: Propose approach before changes
3. **Verify**: Test thoroughly after refactoring

## Backwards Compatibility

- **Default stance**: Maintain compatibility
- **Breaking changes**: Explain necessity before implementing
- **Options**: Explore compatibility options first
- **Approval**: Get approval for breaking changes
- **Documentation**: Document migration path