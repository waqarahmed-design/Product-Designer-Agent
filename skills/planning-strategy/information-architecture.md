# Information Architecture Methods

## Table of Contents
1. [Content Strategy](#1-content-strategy)
2. [Site Mapping](#2-site-mapping)
3. [Taxonomy Design](#3-taxonomy-design)
4. [Navigation Design](#4-navigation-design)
5. [Search Design](#5-search-design)
6. [Mental Model Mapping](#6-mental-model-mapping)

---

## 1. Content Strategy

**Purpose:** Plan the structure, hierarchy, and governance of content so it serves user needs and supports business goals.

**When to use:** Before building any content-heavy product, when content is inconsistent or hard to maintain, when users can't find what they need.

### Content Audit

Before strategizing, inventory what exists:

```
For each piece of content:
  URL / location
  Content type (article, FAQ, guide, legal, marketing)
  Owner / author
  Last updated
  Traffic / usage
  Quality rating (1–5)
  Action: Keep / Update / Remove / Merge
```

Categories from audit:
- **Keep** — accurate, used, well-written
- **Update** — good structure but outdated
- **Remove** — unused, redundant, or misleading
- **Merge** — overlapping topics that confuse users

### Content Hierarchy Principles

```
Primary content    — The main reason users come to this page
Supporting content — Context and detail that aids the primary goal
Related content    — What users typically want next
Secondary content  — Navigation, headers, legal — shouldn't compete
```

**Rule:** Every page should have exactly one primary content goal. If a page serves two equal goals, split it.

### Content Types and Templates

Define a template for each content type to ensure consistency:

```
Template: Help Article
  Title: [Action-oriented — "How to..." or "What is..."]
  Summary: [1–2 sentences — what will the user be able to do after reading this?]
  Prerequisites: [What users need to know/do first]
  Steps: [Numbered, one action per step]
  Expected outcome: [How users know they succeeded]
  Related: [2–3 links to adjacent help topics]
```

### Content Governance

- **Owner** — who is responsible for each content area?
- **Review cycle** — how often is content reviewed for accuracy?
- **Style guide** — voice, tone, capitalization, terminology rules
- **Archival policy** — when does outdated content get removed?

### Outputs
- Content audit spreadsheet
- Content type definitions and templates
- Content hierarchy for each section
- Governance model

---

## 2. Site Mapping

**Purpose:** Create a structural diagram of a product's navigation hierarchy to establish what exists, how it's organized, and how users navigate between sections.

**When to use:** Designing new products, restructuring navigation, onboarding onto an existing product, communicating scope to stakeholders.

### Site Map Notation

```
Rectangle  = Page / screen
Folder     = Section / category
Arrow      = Navigation path
Dashed     = Conditional / authenticated path
[#]        = Page ID for referencing in specs

Example:
[1.0] Home
  ├── [2.0] Products
  │     ├── [2.1] Category listing
  │     ├── [2.2] Product detail
  │     └── [2.3] Product comparison
  ├── [3.0] Account (authenticated)
  │     ├── [3.1] Dashboard
  │     ├── [3.2] Orders
  │     └── [3.3] Settings
  └── [4.0] Support
        ├── [4.1] Help center
        └── [4.2] Contact
```

### Flat vs. Deep Hierarchy

| Structure | Max depth | Best for | Risk |
|-----------|-----------|----------|------|
| Flat | 2 levels | Simple products, content sites | Navigation overwhelm at top level |
| Balanced | 3 levels | Most products | |
| Deep | 4+ levels | Large content sites, complex apps | Users get lost, back-button confusion |

**Rule of thumb:** Users should be able to reach any page within 3 clicks from the home screen. If not, reassess the hierarchy.

### Current vs. Future State

When restructuring:
1. Map **current state** — document reality (include broken and orphaned pages)
2. Identify **problems** — dead ends, redundant paths, buried content
3. Map **future state** — proposed new structure
4. Define **redirect plan** — old URLs → new URLs to preserve SEO and existing links

### Card Sorting (validating the sitemap)

Test your proposed structure with users:
- **Open card sort** — give users content cards, ask them to group and name the groups (reveals mental models)
- **Closed card sort** — give users your proposed categories, ask them to place cards (validates your structure)
- Recruit 15–20 participants; patterns emerge quickly

### Outputs
- Site map diagram (current and/or future state)
- Page inventory with IDs
- Redirect plan (if restructuring)

---

## 3. Taxonomy Design

**Purpose:** Design the system of categories, labels, and relationships used to organize and retrieve information within a product.

**When to use:** Building search/filter systems, content libraries, product catalogs, tag systems, or any navigable collection of items.

### Taxonomy Types

| Type | Structure | Example |
|------|-----------|---------|
| **Hierarchical** | Parent → child relationships, one parent per node | File system, product categories |
| **Faceted** | Multiple independent dimensions that filter simultaneously | E-commerce filters (color + size + price) |
| **Flat (tags)** | No hierarchy, flexible association | Blog tags, bookmark labels |
| **Polyhierarchical** | Nodes can have multiple parents | "Laptop" belongs to both "Computers" and "Work gear" |

### Naming Principles

**Use user language, not internal language:**
- Internal: "Account Management" → User language: "Your Account"
- Internal: "Knowledge Base" → User language: "Help & Support"
- Internal: "Subscription Tier" → User language: "Your Plan"

**Mutual exclusivity:** Categories shouldn't overlap. If an item could belong to two categories, the categories are too broad.

**Exhaustive coverage:** Every item should fit somewhere. "Other" or "Misc" categories signal taxonomy failure — redesign the structure.

**Label testing:**
- Show users a label, ask "What would you expect to find here?"
- Show users content, ask "Where would you look for this?"
- Mismatches reveal vocabulary problems

### Controlled Vocabulary

For tag-based systems, define rules:
```
Preferred term:  "Email marketing"
Synonyms:        "Email campaigns", "Newsletter", "EDM" → redirect to preferred term
Broader term:    "Digital marketing"
Narrower terms:  "Drip campaigns", "Transactional email"
Related terms:   "Marketing automation", "CRM"
```

### Taxonomy Maintenance
- New content should be classified within 48 hours of creation
- Review top-level categories quarterly
- Retire unused tags after 12 months of inactivity
- One person or team owns taxonomy governance

### Outputs
- Taxonomy structure with all levels and labels
- Controlled vocabulary list
- Classification guidelines for content creators
- Facet definitions (if faceted)

---

## 4. Navigation Design

**Purpose:** Design the system that allows users to move through a product efficiently and understand where they are at all times.

**When to use:** Any new product or screen architecture, when users report getting lost, when analytics show unexpected exit pages.

### Navigation Patterns by Context

| Pattern | Best for | Avoid when |
|---------|----------|------------|
| **Top navigation bar** | 4–7 primary sections, desktop | More than 7 items (overwhelm) |
| **Side navigation** | Complex apps with many sections, frequent switching | Mobile-first products |
| **Bottom tab bar** | Mobile apps, 3–5 primary sections | More than 5 tabs |
| **Hamburger menu** | Secondary/overflow navigation | Primary navigation on mobile |
| **Breadcrumbs** | Deep hierarchies, content sites | Flat products (adds noise) |
| **Mega menu** | Large e-commerce, content-rich sites | Simple products |
| **Step indicator** | Linear flows (checkout, onboarding) | Non-sequential processes |

### Navigation Design Rules

**Wayfinding — users must always know:**
1. Where am I? (active state, page title, breadcrumbs)
2. Where can I go? (visible navigation options)
3. Where have I been? (visited states, history)

**Active state design:**
- Never rely on color alone — use weight, underline, or indicator
- Active states must be immediately distinguishable from hover states
- Mobile: active tab needs both icon and label change

**Label rules:**
- Use nouns for destinations ("Dashboard", "Orders")
- Use verbs for actions ("Sign in", "Add item")
- Never mix nouns and verbs in the same nav level
- Keep labels under 3 words; 1–2 is ideal

**Depth rules:**
- Navigation deeper than 3 levels needs breadcrumbs
- Users shouldn't need to back-navigate to reach adjacent sections at the same level
- Destructive pages (delete, remove) should not appear in primary navigation

### Mobile Navigation Specifics
- Thumb zone: bottom-center is easiest to reach; top-corners are hardest
- Primary navigation in bottom tab bar, not header
- Minimum tap target: 44×44px (iOS HIG), 48×48dp (Material)
- Avoid gestures as the only navigation method

### Outputs
- Navigation structure diagram
- Active/hover/default state specs for each nav element
- Mobile-specific navigation patterns
- Labels validated against user vocabulary

---

## 5. Search Design

**Purpose:** Design a search experience that helps users find what they need quickly, even when they don't know exactly what they're looking for.

**When to use:** Products with more content than can be reasonably browsed, any catalog or library, when user research shows "I couldn't find it" as a pain point.

### Search Experience Components

```
Search entry
  └── Input field + trigger (button or Enter)
  └── Search suggestions / autocomplete
  └── Recent searches

Results page
  └── Query restatement ("Showing results for...")
  └── Result count
  └── Sort controls
  └── Filter/facet panel
  └── Result cards/rows
  └── Pagination or infinite scroll

Edge cases
  └── Zero results state
  └── Did you mean? (typo correction)
  └── Partial match state
  └── Search within results
```

### Autocomplete Design

**Triggering:** Show suggestions after 2–3 characters (not 1 — too many results)

**Suggestion types:**
- Query completions ("iphone" → "iphone 15 pro max")
- Entity suggestions (show the actual item, not just the query)
- Recent searches (personalized, dismissible)
- Trending searches (social proof)

**Keyboard navigation:** Suggestions must be navigable by arrow keys; Enter selects; Escape closes.

### Zero Results State

Never show a dead end:

```
"No results for 'bluw shirt'"
→ Did you mean: 'blue shirt'?
→ Try searching for: shirts, blue tops, casual wear
→ Browse: Men's Clothing | Women's Clothing
```

Design obligation: zero results is a design failure in disguise — treat each one as a signal to improve taxonomy, autocomplete, or inventory.

### Search Analytics to Monitor

| Metric | Signals |
|--------|---------|
| Zero-result rate | Vocabulary mismatch, missing content |
| Search abandonment rate | Results not satisfying queries |
| Top queries | What users want most (should be easiest to find) |
| Queries with no clicks | Results visible but not relevant |
| Reformulation rate | Users rephrasing same query (first results failed) |

### Filters vs. Facets

**Filters:** Sequential narrowing — "Show me only red items" (removes others)
**Facets:** Simultaneous dimensions — "Red AND size M AND under $50" (each facet is independent)

Facets are almost always preferred for catalog search. Filters work better for single-dimension narrowing (date range, status).

### Outputs
- Search component specs (input, suggestions, results, edge cases)
- Filter/facet taxonomy
- Zero-results fallback flows
- Search analytics baseline to measure against

---

## 6. Mental Model Mapping

**Purpose:** Document how users conceptualize the domain your product operates in — their vocabulary, expected behaviors, and assumed relationships — so design can align with those expectations.

**When to use:** Designing navigation and IA, when users describe the product using different words than the team uses, when features exist but users can't find or use them.

### What a Mental Model Is

A mental model is the internal representation a user builds of how a system works. It doesn't need to be accurate — it just needs to be understood by the designer.

**Example:**
Users think of email as "letters in a mailbox." This mental model explains why:
- They expect emails to stay until explicitly deleted (letters don't auto-expire)
- They get confused by "archive" (where did it go?)
- They think of labels/tags as "putting a letter in a folder"

### Eliciting Mental Models (Research Techniques)

**Vocabulary surfacing:**
- Ask users to describe the product without being shown it: "Tell me how you'd explain [product] to a friend"
- Note every noun (reveals how they categorize things) and every verb (reveals expected interactions)

**Card sorting (open sort):**
- Give users content cards with no category structure
- Ask them to group cards and name each group
- The group names are their mental model labels

**Think-aloud during navigation:**
- Ask users to find something specific while thinking aloud
- Wrong turns reveal where the product's structure diverges from their model

**The "broken" question:**
- "When [product] does something unexpected, what do you think happened?"
- Reveals their underlying causal model

### Mental Model Diagram

Map user mental model vs. product model side by side:

```
USER'S MENTAL MODEL          PRODUCT STRUCTURE
────────────────────         ──────────────────
"My stuff"                   Profile
"Projects"                   Workspaces
"Shared with me"             Collaboration inbox
"Trash"                      Archived items (no trash?)
"Settings"                   ??? (scattered across 3 menus)
```

Mismatches in this diagram are IA problems to solve.

### Bridging Model Gaps

For each mismatch:
1. **Align the product to the user model** (preferred — rename, restructure)
2. **Educate users to adopt the product model** (only if 1 is impossible — costly, risky)
3. **Hybrid** — use user language in the UI even if internal structure differs

### Outputs
- Mental model diagram with user-side and product-side vocabulary
- List of vocabulary mismatches with severity
- IA/navigation recommendations derived from alignment gaps
