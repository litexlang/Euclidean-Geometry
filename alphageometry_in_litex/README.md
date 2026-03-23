# AlphaGeometry in Litex

This directory contains a formalisation in **Litex** of [AlphaGeometry](https://github.com/google-deepmind/alphageometry)'s geometric definitions and deductive inference rules. AlphaGeometry is DeepMind's symbolic reasoning system for Euclidean plane geometry; its `defs.txt` and `rules.txt` provide compact representations of a large body of geometric concepts and theorems. This project ports that content into Litex, combining a strict logical structure with a concise syntax.

## Conciseness of the Litex Language

Litex is designed for a balance of **declarative style**, **readability**, and **compactness**. Compared to AlphaGeometry's raw text format, it offers:

| Feature | Description | Example |
|---------|-------------|---------|
| **Unified syntax** | Definitions (`prop`), constructions (`let draw_...`), and deduction (`know`) all use the same function and predicate syntax | `prop midpoint(x,a,b): $diff(a,b), $coll(x,a,b), $cong(x,a,x,b)` |
| **Explicit types** | Declarations such as `point` and `nonempty_set` clarify types and reduce ambiguity | `have point nonempty_set` |
| **Readable formulas** | `forall` / `=>` directly correspond to first-order logic; bilingual comments support understanding | `forall a,b,c point: $ncoll(a,b,c) =>: $para(e,f,b,c)` |
| **Modularity** | Definitions and rules are separated and can be referenced or verified independently | `defs.lit` for constructions and concepts, `rules.lit` for deduction rules |

---

## File Overview

### 1. `defs.lit` — Geometric Definitions and Constructions

`defs.lit` is the Litex formalisation of AlphaGeometry's `defs.txt`. It contains:

#### 1.1 Basic Props

Primitive predicates used only by reference during problem solving (no definitions), for example:

- `ncoll2(a,b,c,d)` — Four points are not collinear  
- `eqangle(a,b,c,d,e,f,g,h)` — Equal angles  
- `cong(a,b,c,d)` — Segments have equal length  
- `para(a,b,c,d)` / `npara(a,b,c,d)` — Parallel / not parallel  
- `perp(a,b,c,d)` / `nperp(a,b,c,d)` — Perpendicular / not perpendicular  
- `coll(a,b,c)` — Collinear  
- `diff(a,b)` — Distinct points  

#### 1.2 Geometric Concept Definitions (`prop`)

Each geometric concept is given by a `prop` of the form `prop name(...): preconditions => conditions`, with the original `defs.txt` format retained as reference comments. Representative examples:

| Concept | Description |
|---------|-------------|
| `angle_bisector` | Angle bisector |
| `circle` / `circumcenter` | Circumcenter |
| `foot` | Foot of perpendicular |
| `incenter` / `excenter` | Incenter / Excenter |
| `orthocenter` | Orthocenter |
| `midpoint` | Midpoint |
| `iso_triangle` | Isosceles triangle |
| `parallelogram` | Parallelogram |
| `square` / `rectangle` | Square / Rectangle |
| `tangent` / `lc_tangent` | Tangent-related |
| `intersection_ll` / `intersection_lc` etc. | Line–line, line–circle intersections |

#### 1.3 Geometric Constructions (`let draw_...`)

For each constructible geometric object, an explicit constructor is provided in the form:

```
let draw_xxx fn(parameters: preconditions) return_type
know:
  forall parameters: preconditions =>: conclusion (satisfying the corresponding prop)
```

For example: `draw_midpoint_x(a,b)` constructs the midpoint of segment `ab`; `draw_foot_x(a,b,c)` constructs the foot from point `a` to line `bc`. These functions correspond one-to-one with `prop` definitions, ensuring correctness of constructions.

---

### 2. `rules.lit` — Geometric Deduction Rules

`rules.lit` is the Litex formalisation of AlphaGeometry's `rules.txt`. It contains **43** geometric deduction rules, covering:

- Perpendicular and parallel (Rule 1–3)  
- Concyclic points and inscribed angles (Rule 2, 4–6)  
- Midsegments and intercepts (Rule 7–8)  
- Angle and ratio relations (Rule 9–13)  
- Isosceles triangles and tangent properties (Rule 14–17)  
- Power of a point, concyclic and similarity (Rule 18–25)  
- Parallelograms and ratios (Rule 26–32)  
- Congruent and similar triangles (Rule 33–41)  
- Intercept theorem and its converse (Rule 42–43)  

#### 2.1 Rule Format

Each rule uses the following structure for easy cross-reference with the original `rules.txt` and natural-language descriptions:

```
# Rule N
### rules.txt single line: original single-line rule (AlphaGeometry format)
### Natural language: description (Chinese)
### English: description (where applicable)
know:
    forall variables point:
        premises...
        =>:
            conclusion
```

#### 2.2 Dependent Predicates

`rules.lit` declares at the top all predicates required by the rules, including:

- Basic: `ncoll`, `eqangle`, `cong`, `para`, `diff`, `perp`, `coll`  
- Composite: `midpoint`, `circle`, `cyclic`, `cyclic6`, `eqratio`, `eqratio6`, `eqratio3`  
- Triangle relations: `contri`, `contri2`, `simtri`  
- Auxiliary: `npara`, `ncoll2`, `sameside`  

These predicates are compatible with the concepts defined in `defs.lit`; some have minimal definitions in `rules.lit` for deduction purposes.

---


---

## Correspondence with AlphaGeometry

| AlphaGeometry source | Litex counterpart | Notes |
|---------------------|--------------------|-------|
| `defs.txt`          | `defs.lit`         | Geometric definitions and constructions, one-to-one |
| `rules.txt`         | `rules.lit`        | 43 deduction rules, with rules.txt single-line format in comments |


---

## Usage Suggestions

1. **Understand the definitions**: Read the `prop` and `let draw_...` entries in `defs.lit` to clarify the meaning of each geometric concept and construction.  
2. **Understand the rules**: Browse `rules.lit` by rule number and use the comments to understand each rule's premises and conclusions.  
3. **Formalise problems**: Follow the style of `imo_ag_30.txt` and use the constructions from `defs.lit` to describe new problems.  
4. **Verify and extend**: Use Litex proof/checking tools to verify the definitions and rules, and extend the theorem library as needed.
