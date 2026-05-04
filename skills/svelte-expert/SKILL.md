---
name: svelte-expert
description: Svelte 5 and SvelteKit performance optimization and best practices. Use when building Svelte components, using Runes ($state, $derived, $effect), optimizing SvelteKit load functions, or implementing performance-critical frontend logic.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Svelte 5 & SvelteKit Expert

> **High-Performance Svelte Development** - Modern patterns for Svelte 5 (Runes) and SvelteKit.
> **Philosophy:** Leverage the compiler, eliminate waterfalls, and master the reactivity model.

---

## 🎯 Selective Reading Rule (MANDATORY)

**Read ONLY sections relevant to your task!**

---

## 📑 Content Map

| Category | Impact | Focus | When to Read |
| :--- | :--- | :--- | :--- |
| **1. Runes ($state, $derived, $effect)** | 🔴 **CRITICAL** | Modern reactivity | State management, complex logic, Svelte 5 migration |
| **2. SvelteKit Load Functions** | 🔴 **CRITICAL** | Data fetching waterfalls | Slow page transitions, sequential `fetch` calls |
| **3. Performance & Compilation** | 🟠 **HIGH** | Bundle size & execution | Large apps, slow interactivity, tree-shaking |
| **4. Component Architecture** | 🟡 **MEDIUM** | Snippets & composition | Code reuse, maintainability, props management |
| **5. State Management** | 🟡 **MEDIUM** | Global vs Local state | Cross-component communication, stores vs runes |

---

## 🚀 Quick Decision Tree

**What's your issue?**

```
🐌 Slow page loads / Data lag
  → Read Section 2: SvelteKit Load Functions
  → Check: Use `Promise.all()` in load functions, avoid sequential awaits.

🔄 Reactivity confusion / Bugs
  → Read Section 1: Runes
  → Check: Are you using $state correctly? Avoid $effect for derived logic (use $derived).

📦 Large bundle size
  → Read Section 3: Performance
  → Check: Tree-shaking, component lazy loading, CSS bloat.

🎨 UI Lag / Heavy Rendering
  → Read Section 3: Performance
  → Check: Each blocks keys, avoiding expensive logic in templates.
```

---

## ✅ Svelte Performance Checklist

Before shipping:

- [ ] **No Sequential Awaits:** Load functions fetch independent data in parallel.
- [ ] **Runes Usage:** Using `$derived` instead of `$effect` for state transformations.
- [ ] **Snippets Over Components:** Using `{#snippet}` for small, internal UI logic to reduce component overhead.
- [ ] **Keyed Each Blocks:** All `{#each}` blocks have unique keys (e.g., `(item.id)`).
- [ ] **Selective Effects:** `$effect` is used only for side effects, not for syncing state.
- [ ] **Server-Side Rendering (SSR):** Critical data is fetched on the server for SEO and fast FCP.

---

## ❌ Anti-Patterns (Common Mistakes)

**DON'T:**

- ❌ Use `$effect` to update state based on other state (use `$derived`).
- ❌ Fetch data sequentially in `load` functions.
- ❌ Pass huge objects as props if only a few fields are needed (breaks granularity).
- ❌ Overuse Svelte stores in Svelte 5 (use classes with `$state` instead).
- ❌ Forget to use the `node` adapter or equivalent for production performance.

**DO:**

- ✅ Use `$state` for mutable values and `$derived` for computed values.
- ✅ Parallelize fetches: `const [a, b] = await Promise.all([fetchA(), fetchB()])`.
- ✅ Use `{#snippet}` for repeatable UI fragments within a component.
- ✅ Leverage SvelteKit's `enhance` for form actions.
- ✅ Profile with Svelte DevTools.

---

## 🎯 How to Use This Skill

1. **New Features:** Use Runes by default. Master the difference between `$state` and `$state.raw`.
2. **Performance Audits:** Check `+page.server.js` or `+page.js` for waterfalls.
3. **Architecture:** Use class-based state for complex logic (Svelte 5 "Universal Reactivity").

---

**Version:** 1.0.0 (Svelte 5 Focus)
**Date:** May 2026
