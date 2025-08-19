# Python Development Guidelines

Language-specific guidelines for Python development with AI assistance.

## Virtual Environment Management
- **CRITICAL**: Verify virtual environment status using `echo $VIRTUAL_ENV` before python/pip commands
- **Trust user confirmation**: If user says venv is active, proceed without activation
- **Ask for location**: If `.env` not found in current directory

## Code Standards
- **Format**: Use `black` and `isort`
- **Type hints**: No type hints unless requested
- **Naming**: Follow PEP 8 naming conventions
- **Error handling**: Use EAFP principle (try/except over pre-checking conditions)
- **Philosophy**: Follow the Zen of Python (see below)

## Library Preferences
- **HTTP**: `requests`
- **Web framework**: `flask`, `jinja2`
- **CLI/output**: `argparse`, `click`, `logging`, `rich`

## The Zen of Python
```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

## Quality Checklist
- [ ] **Virtual environment**: Verified (`echo $VIRTUAL_ENV`)
- [ ] **Formatting**: Code formatted with `black` and `isort`
- [ ] **Naming**: PEP 8 naming standards followed
- [ ] **Error handling**: EAFP principle applied
- [ ] **Libraries**: Library choices justified
- [ ] **Functions**: Single-purpose and composable
- [ ] **Error handling**: Proper error handling implemented
- [ ] **Comments**: Explain why, not what