# **GEMINI.md**

This file defines how agents should operate in this project. It blends general **AGENTS.md best practices** with our **Performance‑Idiomatic Python style**. The goal: agents generate code that is not just correct, but also **fast by default** on CPython.

---

## **Purpose**

* Provide **machine‑usable guidance** for AI agents.

* Default to **performance‑idiomatic Python** (C‑accelerated, loop‑minimal, memory‑aware).

* Ensure **maintainability \+ reproducibility**: style, structure, testing, and performance regression tracking.

---

## **Directory Structure**

* `src/` → core modules

* `tests/` → unit & performance tests

* `docs/` → human‑readable docs

* `benchmarks/` → profiling and regression benchmarks

* `AGENTS.md` → this file (agent‑facing)

* `README.md` → human‑facing intro

---

## **Build & Test Commands**

\# Run lint, type check, unit tests  
make check

\# Run performance regression suite  
make bench

\# Quick profiling for hotspots  
python \-m cProfile \-o profile.out src/main.py

---

## **Code Style**

* **Python ≥3.12 required**.

* Lint: `ruff`.

* Type hints: `mypy --strict`.

* Docstrings: Google‑style.

* Indent: 4 spaces, max 88 cols.

* Hot paths annotated with `# hot path`.

---

## **Performance‑Idiomatic Python (Agent Style)**

### **Core Traits**

* **Intent‑first abstractions**: prefer builtins / stdlib C‑paths over manual loops.

* **Loop‑minimal**: use comprehensions, `sum`, `min`, `max`, `any`, `all`, `itertools`.

* **C‑backed data structures**: `dict`, `set`, `deque`, `array`, `memoryview`.

* **Data locality**: contiguous buffers, slices, `__slots__`, `@dataclass(slots=True)`.

* **Work pushdown**: `json`, `zlib`, `hashlib`, `sqlite3`, `csv`, `struct`, `mmap`.

* **Caching**: `functools.lru_cache`, pre‑compiled regex.

* **Concurrency**:

  * I/O → `asyncio`, threads.

  * CPU‑bound pure Python → processes.

  * CPU‑bound C‑extensions → libs that release GIL.

* **Profiling**: always measure; optimize only real bottlenecks.

### **Do / Avoid Examples**

\# ✅ Do  
total \= sum(values)

\# ❌ Avoid  
for v in values:  
    total \+= v

\# ✅ Do  
processed \= \[f(x) for x in data if cond(x)\]

\# ❌ Avoid  
processed \= \[\]  
for x in data:  
    if cond(x):  
        processed.append(f(x))

---

## **Agent Instructions**

* Default to **C‑accelerated primitives** over Python loops.

* Auto‑suggest refactors when hot loops appear.

* Annotate hot paths with `# hot path`.

* Suggest profiling hooks for new code.

* Do not micro‑optimize trivial/cold paths.

---

## **Profiling & Regression**

* Use `cProfile` \+ `snakeviz` for call graphs.

* Keep performance baselines in `benchmarks/`.

* CI should reject commits slowing hot paths \>10%.

---

## **Summary**

This AGENTS.md:

1. Defines **directory structure**.

2. Provides **build & test commands**.

3. Enforces **code style & type safety**.

4. Embeds **Performance‑Idiomatic Python** as the default programming model.

Agents should follow these rules **strictly**, unless profiling shows a justified exception.