# Migration Workflow: Bootstrap 3 to Bootstrap 5.3 (Twig Environment)
Enforces a clean backend-friendly stack while meeting Taste Skill premium aesthetic standards.

## Stack Rules
- Template Engine: Twig (`.html.twig`) - Variables and tags must remain untouched.
- CSS Framework: Bootstrap 5.3+ (No Tailwind, No jQuery).
- Theme Customization: Exclusively via Bootstrap 5 CSS Variables (`:root { --bs-primary: ... }`).

## Migration Pipeline

1. TWIG & STRUCTURAL MAP (Authority: Bencium UX)
   - Action: Read the legacy BS3 template. Document the variables and loops.
   - Output: An unchanged template skeleton ready for class replacement.

2. CLASS DICTIONARY & DESIGN SYSTEM (Authority: UI/UX Pro Max)
   - Action: Map BS3 component classes to their modern BS5 equivalents (e.g., Panels to Cards).
   - Theme: Define premium tokens using BS5 utility variables (e.g., `rounded-3`, `shadow-sm`, custom root colors).

3. TEMPLATE REFACTORING (Authority: Anthropic Frontend)
   - Action: Rewrite the Twig code using strict Bootstrap 5 syntax.
   - Rule: Leverage BS5 utility classes for spacing (`ms-auto`, `pe-3`, `gap-3`) to satisfy Taste's alignment constraints without custom CSS.

4. BROWSER VALIDATION (Authority: Taste Skill)
   - Action: Run headless browser tests (`node scripts/consistency.mjs`).
   - Guardrail: Instantly fail the build if any legacy BS3 classes remain or if layout alignment breaks on mobile viewport (390px).