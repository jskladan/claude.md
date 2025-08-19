---
description: "Smart commit message rewording with style transformation"
args: "[sha] [style_or_message]"
---

# Smart Reword Command

Intelligently rewrites commit messages with style transformation and tone adjustment capabilities.

## Usage
- `/reword SHA "New message"` - Reword with specific message
- `/reword SHA` - AI-assisted reword with auto-style detection
- `/reword SHA dev` - Transform to verbose development style
- `/reword SHA final` - Transform to concise final style

## Style Transformation

### Tone Keywords
- **Verbose triggers**: `dev`, `wip`, `verbose`, `detailed`
- **Concise triggers**: `final`, `concise`, `clean`, `prod`

### Smart Detection
When no style specified, AI analyzes:
- **Current message style**: Detect existing verbose vs concise pattern
- **Commit content**: Scope and complexity of changes
- **Position in history**: Recent vs older commits
- **Context clues**: File types and change patterns

## Process

### 1. Validate Commit
```bash
# Verify SHA exists and is reachable
git rev-parse --verify <sha>
git merge-base --is-ancestor <sha> HEAD
```

### 2. Analyze Current Message
Extract and analyze:
- **Current style**: Verbose development vs concise final
- **Content elements**: What information is present
- **Context quality**: How much detail exists
- **Transformation needs**: What style should result be

### 3. Message Transformation

#### To Verbose Style (dev/wip)
```
Original: "Fix authentication bug"

Transformed: "Fix authentication token validation bug

Detailed context:
- Token expiration validation was missing null checks
- Added proper error handling for expired tokens
- Updated authentication middleware to handle edge cases
- Fixed session cleanup on token invalidation

Co-authored-by: Claude <noreply@anthropic.com>"
```

#### To Concise Style (final/clean)
```
Original: "WIP: implement OAuth flow - token handling complete, session management in progress, need to debug refresh logic"

Transformed: "Implement OAuth authentication flow

- Add token handling and validation
- Implement session management
- Fix token refresh logic

Co-authored-by: Claude <noreply@anthropic.com>"
```

### 4. Execute Reword

#### Using Git Alias (Preferred)
```bash
git reword <sha> "New message here"
```

#### Fallback Method
```bash
GIT_SEQUENCE_EDITOR="sed -i '' 1s/^pick/reword/" \
GIT_EDITOR="printf \"%s\n\" \"new message here\" >" \
git rebase -i <commit-hash>^
```

## Style Transformation Logic

### Content Analysis
The AI examines the commit to understand:
- **File changes**: What was actually modified
- **Change scope**: Small fix vs large feature
- **Technical complexity**: Simple update vs architectural change
- **Context availability**: How much can be inferred vs needs detail

### Message Enhancement Patterns

#### Verbose Enhancement
- **Expand reasoning**: Why changes were made
- **Add context**: Blockers encountered and solutions
- **Detail approach**: Technical decisions and alternatives
- **Include next steps**: Follow-up work or considerations

#### Concise Enhancement  
- **Distill essence**: Core functionality delivered
- **Bullet key changes**: Most important modifications
- **Remove verbosity**: Strip implementation details
- **Focus on value**: What the commit accomplishes

## Integration Examples

### Development Cleanup
```bash
# Convert old verbose commits to clean final style
/reword abc1234 final
/reword def5678 final
/reword ghi9012 final
```

### Adding Context
```bash
# Add detail to cryptic commit messages
/reword abc1234 dev
# "." becomes detailed explanation of changes
```

### Batch Style Conversion
```bash
# Multiple commits can be reworded with consistent style
git log --oneline -5  # Review recent commits
/reword <sha1> final
/reword <sha2> final  
/reword <sha3> final
```

## Safety Features
- **Validation**: Confirms SHA exists and is reachable before reword
- **Non-interactive**: Uses reliable non-interactive rebase methods
- **Backup suggestion**: Recommends creating backup branch for complex operations
- **Style preservation**: When no style specified, preserves original intent

## Git Alias Integration
Automatically detects and uses `git reword` alias when available:
```bash
reword = "!f() {\n  GIT_SEQUENCE_EDITOR=\"sed -i '' 1s/^pick/reword/\" GIT_EDITOR=\"printf \\\"%s\\n\\\" \\\"$2\\\" >\" git rebase -i \"$1^\";\n}; f"
```

Falls back to manual method when alias not configured.