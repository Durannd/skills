---
name: deep-issue-creation
description: >
  Agnostic methodology for creating deep and well-structured sprint issues.
  Codebase analysis, understanding existing patterns, and generating issues
  with business rules, acceptance criteria, and detailed technical notes.
  Works on any tech stack (Backend, Frontend, Mobile, etc).
allowed-tools: View, Grep, Glob, PowerShell, GitHub CLI
---

# Deep Issue Creation

> Skill for creating sprint issues that go beyond the shallow. Works on any codebase (backend, frontend, mobile, fullstack).

## Philosophy

**Don't:** Create issues with vague titles and generic descriptions.
**Do:** Create issues that reflect the technical reality with:
- ✅ Codebase analysis before creating
- ✅ Understanding of existing architectural patterns
- ✅ Well-defined business rules
- ✅ Verifiable acceptance criteria
- ✅ Technical notes with context
- ✅ Explicit dependencies between issues
- ✅ Schema/structure in tables (not floating code)

---

## 5-Phase Workflow

### Phase 1: Technical Exploration

**Before creating any issue**, explore the project:

#### 1. Understand the Architecture
- What is the architectural pattern? (MVC, service-oriented, event-driven, component-based)
- How do data flow?
- What are the layers? (controllers, services, models, components, store)
- Are there established patterns?

**Examples by type:**
- **Backend:** Models → Services → Controllers, or Queue Workers → Adapters
- **Frontend:** Components → Pages → State → Services, or Hooks → Context
- **Mobile:** Screens → Providers → Services → Models
- **Full-stack:** All of the above

#### 2. Review Existing Patterns
```bash
# Backend
grep -r "class.*Service" services/
grep -r "Model" models/ | head -20
ls migrations/ | tail -10

# Frontend
grep -r "export.*function.*\(" src/components/
grep -r "useContext\|useState" src/ | head -20
grep -r "interface.*{" src/ | head -10

# General - find structure
find . -name "*.js" -o -name "*.ts" | head -30
```

#### 3. Look for Existing Documentation
- Are there ADRs (Architecture Decision Records)?
- Are there README or docs/ with patterns?
- Are there technical comments in critical files?
- Are there examples of previous features?

#### 4. Identify External Dependencies
- APIs? What is the integration pattern?
- Database? What is the approach (SQL, NoSQL)?
- Key libraries? How are they used?
- Tests? Which framework?

**Time:** 15-30 minutes of exploration

---

### Phase 2: Requirements Decomposition

Based on exploration, break down into components:

#### A. Identify Independent Components
```
Example Backend (REST API):
- Issue 1: Models + Migrations (base)
- Issue 2: API Endpoints (depends on #1)
- Issue 3: Authentication (independent)
- Issue 4: Validations/Middleware (depends on #3)

Example Frontend (React):
- Issue 1: Design System / Base components
- Issue 2: Page X with components (depends on #1)
- Issue 3: State/Context (independent)
- Issue 4: API integration (depends on #2, #3)

Example Mobile:
- Issue 1: Models/Data structures
- Issue 2: Screens (depends on #1)
- Issue 3: Navigation setup (depends on #2)
- Issue 4: API integration (depends on #1)
```

#### B. Map Dependencies
- What is the **base**? (usually models/data/design)
- What **depends on** what?
- What can run **in parallel**?

```
#1 (base)
  ↓
#2, #3 (parallel)
  ↓
#4 (depends on #2 + #3)
```

#### C. Consider Project Patterns
- If using queues (BullMQ, Celery), respect the sequence
- If using components (React, Vue, Flutter), define base component dependencies
- If using state (Redux, Context, Riverpod), model data flow

**Output:** 5-10 issues with clear dependency graph

---

### Phase 3: Content Structuring

**For each issue**, use this structure:

#### A. Objective (1 clear phrase)
```markdown
## Objective
[Clearly what will be implemented]

Examples:
- Backend: "Create User model with migrations and validations"
- Frontend: "Implement reusable Card component with Storybook"
- Mobile: "Setup authentication with local storage"
```

#### B. Business Rules
```markdown
## Business Rules
- [Rule 1]
- [Rule 2]
- [Condition X] → [Behavior Y]

Examples:
- Backend: "Unique email, password min 8 chars"
- Frontend: "Card must support avatar, title, description, actions"
- Mobile: "Token stored in secure storage, expires in 24h"
```

#### C. Schema/Structure (IN TABLES)
```markdown
## Schema/Structure

### Database (if applicable)
| Field | Type | Null | Default |
|-------|------|------|---------|

### Components (if frontend/mobile)
| Component | Props | Events |
|-----------|-------|--------|

### API Endpoints (if backend)
| Method | Path | Input | Output |
|--------|------|-------|--------|
```

**IMPORTANT:** Don't put code here. Use tables for spec.

#### D. Acceptance Criteria
```markdown
## Acceptance Criteria
- [ ] [Thing 1] created with exact spec
- [ ] [Thing 2] tested with [method]
- [ ] [Thing 3] integrated with [other]
- [ ] Documentation/Storybook updated
- [ ] Tests covering [scenarios]
```

**Complete Example:**
```markdown
## Objective
Implement reusable Button component with support for variants and states.

## Business Rules
- Support 4 variants: primary, secondary, danger, ghost
- States: default, hover, focus, disabled, loading
- Accessible: proper ARIA labels, keyboard support
- Mobile-friendly: min 44px tap target

## Structure

### Button Component
| Prop | Type | Default | Description |
|------|------|---------|-------------|
| variant | enum | primary | primary, secondary, danger, ghost |
| size | enum | md | sm, md, lg |
| disabled | bool | false | |
| loading | bool | false | Show spinner |
| onClick | func | - | Handler |
| children | node | - | Text/content |

### CSS States
| State | Behavior |
|-------|----------|
| :hover | Darken color, shadow |
| :focus | Focus ring |
| :disabled | Opacity 50%, cursor not-allowed |
| .loading | Spinner + disabled |

## Acceptance Criteria
- [ ] Component created with 4 variants
- [ ] Unit tests: render, onClick, disabled states
- [ ] Accessibility tests: ARIA labels, keyboard nav
- [ ] Storybook with examples of each variant
- [ ] Usage documentation (props, events)
- [ ] Visual tests (snapshot or visual regression)
```

---

### Phase 4: Cross-Cutting Considerations

For **each issue**, consider:

| Aspect | Questions |
|--------|-----------|
| **Security** | Input sanitization? Auth? Rate limiting? |
| **Performance** | Indexes? N+1 queries? Lazy loading? Bundle size? |
| **Accessibility** | ARIA labels? Keyboard nav? Color contrast? |
| **Compliance** | LGPD? GDPR? Logs/audit? |
| **Testing** | Unit? Integration? E2E? Mocks needed? |
| **Documentation** | Code comments? README? API docs? Storybook? |
| **Fallback** | If API fails, what happens? Default values? |
| **Logging** | Important context? (userId, traceId, timestamp) |

**Add a "Technical Notes" section** to the issue with these considerations:

```markdown
## Technical Notes
- **Security:** Validate email with RFC 5322 regex, hash password with bcrypt (10 rounds)
- **Performance:** Create index on email for login, cache tokens in Redis
- **Testing:** Mock API with MSW, tests with Jest + React Testing Library
- **Fallback:** If API fails, retry 3x with exponential backoff
```

---

### Phase 5: Creation

#### Option A: Manual via UI (always works)
1. Open GitHub repo → Issues → New issue
2. Copy structured content
3. Create the issue
4. Come back later to link dependencies in Projects

#### Option B: Automation with gh CLI (faster)

```powershell
# Structure content
$body = @"
## Objective
...

## Business Rules
...

## Schema/Structure
| Field | ...

## Acceptance Criteria
- [ ] ...
"@

# Save to temporary file (avoids quoting issues)
$tempFile = New-TemporaryFile
Set-Content -Path $tempFile -Value $body -Encoding UTF8

# Create issue
& gh issue create --title "Descriptive title" --body-file $tempFile --assignee @me

# Clean up
Remove-Item $tempFile
```

**gh advantages:**
- ✅ No data loss from copy-paste
- ✅ Fast for multiple issues
- ✅ Scriptable
- ✅ Traceable

---

## Quality Checklist

Before creating, verify:

```
Exploration:
- [ ] Visit key files (models, components, services)
- [ ] Understand existing patterns
- [ ] Look for docs/ADR

Structure:
- [ ] Schema in tables (not code)
- [ ] Clear Objective (1 phrase)
- [ ] Specific business rules (not generic)
- [ ] Verifiable criteria (not "tested well")

Quality:
- [ ] Considered security/perf/accessibility?
- [ ] Dependencies mapped?
- [ ] Specific name? (not "Implement feature")
- [ ] Can a new dev start with this?
```

---

## Examples by Project Type

### Backend (Node/Python/Go)
```markdown
## Objective
Create POST /users endpoint with validation and authentication.

## Business Rules
- Unique email, password min 8 chars
- Returns valid JWT token for 24h
- Rate limit: 5 requests/min per IP

## Schema

### Endpoint
| Method | Path | Auth | Input | Output |
|--------|------|------|-------|--------|
| POST | /users | - | {email, password} | {id, token} |

### User Model
| Field | Type | Validation |
|-------|------|-----------|

## Tests
- [ ] Unit tests (model, validation)
- [ ] Integration tests (API)
- [ ] Security tests (SQL injection, XSS)
```

### Frontend (React/Vue/Svelte)
```markdown
## Objective
Implement user list page with pagination and filters.

## Business Rules
- Display 10 users per page
- Filter by name and email
- Soft deleted users not shown
- Avatar placeholder if null

## Components Needed
| Component | Responsibility |
|-----------|----------------|
| UserList | Main page |
| UserCard | User row |
| FilterBar | Filters |
| Pagination | Page nav |

## Acceptance Criteria
- [ ] Page created with components
- [ ] Tests with React Testing Library
- [ ] Storybook updated
```

### Mobile (React Native/Flutter)
```markdown
## Objective
Implement login screen with biometry support.

## Business Rules
- Support touch ID/face ID
- Fallback to PIN if biometry unavailable
- Token stored in secure storage
- Auto-login if token valid

## Tests
- [ ] Unit tests (auth logic)
- [ ] Integration tests (storage)
- [ ] E2E tests (full flow)
```

---

## Anti-patterns to Avoid

| ❌ Wrong | ✅ Right |
|---------|---------|
| "Implement feature" | "Create POST /users endpoint with JWT auth" |
| Loose JavaScript code | Schema in table |
| "Tests included" | "Tests: unit, integration, E2E with [framework]" |
| No context | Business rules + acceptance criteria |
| "As per pattern" | "Follows [X] pattern, see [file]" |
| Giant issues | 5-10 issues with clear deps |

---

## When to Use This Skill

- ✅ Sprint planning with multiple issues
- ✅ New feature (API, component, screen)
- ✅ External service integration
- ✅ Significant refactoring
- ✅ When technical traceability matters

## When Not to Use

- ❌ Trivial bugfix already well understood
- ❌ Simple documentation/typo
- ❌ Administrative tasks
- ❌ Issues that are really "bonus task"

---

## Final Tips

1. **Exploration is 50% of the work** - don't skip. Quality comes from here.

2. **Tables > Code** - schemas in tables are clearer and less error-prone.

3. **Specific names** - "POST /users endpoint" is better than "User auth".

4. **Accept that not everything is known** - use ⚠️ for "to be refined later".

5. **Test the flow** - "Can a new dev start with this issue and not get lost?"

6. **Dependency links** - GitHub Projects or `gh issue` to link.

7. **Reuse for roadmaps** - this format also works well for roadmap planning.

