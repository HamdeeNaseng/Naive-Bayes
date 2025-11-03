# AI Agent Instructions for Naive Bayes Learning Repository

## Project Architecture

This is an **educational repository** focused on teaching Naive Bayes algorithms through a structured, multi-level curriculum. It's NOT a production codebase—it's a learning workspace with study materials, notes, and experimental code.

### Directory Structure Philosophy

```text
notes/                          # Core learning workspace
├── section-1/                  # Introduction and course orientation
├── section-2 Naive Bayes Concept (Beginner)/  # Conceptual foundations
├── theory/                     # Mathematical foundations and formulas
├── implementations/            # Code examples and templates
├── experiments/               # Student experiment logs and tracking
├── resources/                 # Curated learning materials
└── daily-logs/                # Progress tracking and reflections

Bayes Test/                    # Jupyter notebooks demonstrating use cases
                               # Imports .py modules from machine_learning_examples-master
machine_learning_examples-master/  # Reusable Python modules (.py files)
                               # Hidden from search but imported by Bayes Test notebooks
font/                          # Thai font files (Prompt font family)
                               # Used for matplotlib Thai language rendering
.github/instructions/          # AI agent behavior rules
```

**Key Insight**: `notes/section-*` folders follow a sequential curriculum structure. Section numbers indicate learning progression, not arbitrary organization.

## Writing Style & Conventions

### Three Distinct Content Types

1. **Student-Facing Notes** (`notes/**/*.md`)
   - **Tone**: Conversational, encouraging, emoji-friendly 🎯
   - **Structure**: Intuition → Example → Math → Practice
   - **Format**: Use real-world analogies, include "Think About It" prompts
   - **Reference**: See `.github/instructions/learn.instructions.md` for full guidelines
   - Example: "Think of probability like weather forecasting! ☔"

2. **Technical Implementation** (`Bayes Test/**`)
   - **Format**: Jupyter notebooks (.ipynb) that import from `machine_learning_examples-master/`
   - **Language**: Thai and English mixed (preserve existing language)
   - **Context**: Always include file header with author, date, purpose (see `bayes algorithm.instruction.md`)
   - **Pattern**: Import Python modules → Demonstrate use case → Explain with comments
   - **Comments**: Explain WHY, not just WHAT—this is for learning
   - **Thai Font Setup**: Always configure matplotlib to use Thai fonts from `font/` directory (see Font Configuration Pattern below)

3. **Expert Guidelines** (`.github/instructions/stack.instructions.md`)
   - **Audience**: AI agents and advanced practitioners
   - **Style**: Technical, comprehensive, production-focused
   - **Coverage**: Full ML pipeline from EDA to deployment

### The "Feynman Learning Protocol"

This project follows: **Understand → Build → Apply → Teach → Optimize**

When creating content, ensure it supports this progression. Example: Don't just show sklearn code—explain the concept first, implement from scratch, THEN show sklearn.

## Development Workflows

### No Traditional Build/Test Commands

This repository has **no automated testing or build pipelines**. Instead:

- **For Notebooks**: Launch Jupyter and run cells interactively
- **For Experiments**: Track manually in `notes/experiments/experiments-log.md`
- **For Learning Validation**: Use self-check questions and manual exercises

### Working with the Curriculum

**When adding new content**:

1. Determine skill level: Beginner (Section 1-2) → Intermediate (Applications) → Advanced (Theory)
2. Place in appropriate `section-N` folder or specialized directory
3. Update parent README.md with navigation links
4. Follow the three-stage structure visible in `section-1/1-Introduction/README.md`:
   - Stage 1: Intuitive Understanding (minimal math)
   - Stage 2: Real-World Applications (5 domains: CV, NLP, Healthcare, Finance, Genomics)
   - Stage 3: Deep Mastery (mathematical rigor)

**When explaining algorithms**:

- Start with detective/real-world analogy
- Show the problem it solves BEFORE the solution
- Use tables for comparing variants (e.g., GaussianNB vs MultinomialNB)
- Include self-check questions with 🤔 emoji

## Critical Context & Patterns

### The "machine_learning_examples-master" Folder

- **Purpose**: Reference implementations from LazyProgrammer's course containing reusable Python modules
- **Usage**: Import `.py` files from here into `Bayes Test/` notebooks for demonstrations
- **VS Code Config**: Intentionally excluded from search (`.vscode/settings.json`) to reduce noise
- **Pattern**: `Bayes Test/` notebooks import functions/classes from `machine_learning_examples-master/` to show practical use cases

**Workflow Example**:
```python
# In Bayes Test/demo.ipynb
import sys
sys.path.append('../machine_learning_examples-master')
from naive_bayes.spam_detector import SpamClassifier

# Now demonstrate the use case with explanations
classifier = SpamClassifier()
# ... educational walkthrough of the implementation
```

### Three Naive Bayes Variants Matter Most

From `theory/bayes-fundamentals.md` and `stack.instructions.md`:

1. **GaussianNB**: Continuous features (normal distribution assumption)
2. **MultinomialNB**: Count data (text classification, word frequencies)
3. **BernoulliNB**: Binary features (presence/absence)

Also mention ComplementNB (imbalanced text) and CategoricalNB (categorical features) for completeness.

**Algorithm Selection Pattern**: Always ask about data type first → suggest appropriate variant → explain why.

### Progress Tracking Convention

Students track learning through:
- `daily-logs/daily-log.md`: Daily reflections with ⭐ ratings
- `experiments/experiments-log.md`: Structured experiment templates with results tables
- Checklists in various README files (use `- [ ]` format)

**When creating exercises**: Provide both the template AND a sample completed entry.

## Code Examples Standards

### Standard Import Block (from `implementations/README.md`)

```python
import numpy as np
import pandas as pd
from sklearn.naive_bayes import GaussianNB, MultinomialNB, BernoulliNB
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import classification_report, confusion_matrix
import matplotlib.pyplot as plt
import seaborn as sns
```

### Font Configuration Pattern (for Thai Language Support)

**CRITICAL**: All notebooks with matplotlib visualizations containing Thai text MUST configure fonts properly to avoid displaying squares instead of Thai characters.

**Standard font setup for `Bayes Test/` notebooks**:

```python
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm

# Load and register Thai font from font/ directory
font_path = '../../font/Prompt/Prompt-Regular.ttf'  # Adjust path based on notebook location
font_prop = fm.FontProperties(fname=font_path)

# Register font with matplotlib
fm.fontManager.addfont(font_path)
font_name = font_prop.get_name()

# Configure matplotlib to use the Thai font
plt.rcParams['font.family'] = font_name
plt.rcParams['axes.unicode_minus'] = False  # Fix minus sign display issue

print(f"✅ ตั้งค่า Font ภาษาไทยเป็น '{font_name}' เรียบร้อย")
```

**Path adjustments by notebook location**:
- `Bayes Test/ab_testing/*.ipynb` → use `'../../font/Prompt/Prompt-Regular.ttf'`
- `Bayes Test/*.ipynb` → use `'../font/Prompt/Prompt-Regular.ttf'`

**Key points**:
- Use `fm.fontManager.addfont()` to register the font file - this is essential
- Use `Prompt-Regular.ttf` for readability in graphs (not Bold or Black variants)
- Always include this setup BEFORE any plotting code
- Place in the imports cell at the beginning of the notebook

### Code Comment Philosophy

NOT like this:
```python
model = GaussianNB()  # Create model
```

INSTEAD:
```python
# We use GaussianNB because our features (height, weight) are continuous
# and roughly follow normal distributions. This is like assuming each
# feature's values form a bell curve for each class.
model = GaussianNB()
```

### Real-World Examples Priority

Preferred domains (from curriculum):
1. Email spam detection (classic beginner example)
2. Sentiment analysis (text classification)
3. Medical diagnosis (healthcare domain)
4. Iris dataset (only for quick demos)

Avoid: Synthetic/toy data without clear real-world connection.

## Mathematical Content Guidelines

### Formula Presentation Pattern

1. Show intuitive explanation first
2. Present formula in LaTeX: `$$P(A|B) = \frac{P(B|A) \times P(A)}{P(B)}$$`
3. Define each symbol with plain English
4. Provide numeric example with actual values
5. Connect to real-world interpretation

Example from `theory/bayes-fundamentals.md` shows proper structure:
- Bayes' Theorem → Components → Laplace Smoothing → Log Probabilities
- Each includes "Where:" definitions and practical notes

### Avoid Math Dumping

DON'T start with derivations. START with "What problem does this solve?" and "Why do we need this?"

## Integration Points

### External Resources

Main trusted sources (from `section-1/2-Where to get the code`):
- GitHub: lazyprogrammer/machine_learning_examples
- Google Colab: deeplearningcourses.com/notebooks
- Scikit-learn docs (official reference)

**Pattern**: Always cite source and explain WHY it's trustworthy, not just link dump.

### Cross-References

When mentioning concepts, link to relevant notes:
- Theory? → `notes/theory/bayes-fundamentals.md`
- Implementation? → `notes/implementations/README.md`
- Practice ideas? → `notes/resources/study-resources.md`

## Key Success Metrics

Student success indicators (from curriculum):
- **Beginner**: Can explain NB to non-technical person, built 3 classifiers
- **Intermediate**: Implemented across 3+ domains, knows when to use each variant
- **Advanced**: Built from scratch without sklearn, understands proofs

**When creating content**: Always tie back to one of these milestones.

## Common Pitfalls to Avoid

1. **Over-relying on sklearn**: Show concept first, sklearn second
2. **Math without intuition**: Always analogy → math → example
3. **Missing the "why"**: Explain independence assumption implications
4. **Ignoring learning levels**: Don't put derivations in beginner sections
5. **Generic advice**: "Write tests" doesn't help—show THEIR testing approach (manual experiments)

## Quick Reference: File Type Handlers

- `section-*/README.md`: Follow learn.instructions.md (friendly tone)
- `theory/*.md`: Technical but clear, math-heavy, include examples
- `implementations/*.md`: Heavy comments, beginner-friendly code
- `experiments/*.md`: Structured templates with example entries
- `Bayes Test/**`: Preserve Thai/English mix, add context headers
- `.github/instructions/**`: Technical reference for AI agents
