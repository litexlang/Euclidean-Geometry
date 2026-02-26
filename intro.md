Introduction to Euclidean Geometry Concepts

This document introduces the basic concepts of Euclidean geometry defined in the `new_version.lit` file and their interrelationships.

## Table of Contents

1. [Basic Geometric Objects](#basic-geometric-objects)
2. [Basic Relations](#basic-relations)
3. [Composite Geometric Figures](#composite-geometric-figures)
4. [Geometric Quantities](#geometric-quantities)
5. [Special Points and Lines](#special-points-and-lines)

---

## Basic Geometric Objects

### 1. Point

**Definition**: A point is the most fundamental concept in geometry, a non-empty set.

**Properties**:
- Points are the foundation of all other geometric objects
- Lines and planes can be viewed as sets of points

### 2. Line

**Definition**: A line is a set of points, uniquely determined by two distinct points.

**Main Properties**:
- For any two distinct points A and B, there exists a unique line containing them, denoted as `line_of(A, B)` or `AB`
- Every line contains at least two points
- A line is a set of points: `l $in power_set(point)`

**Key Functions**:
- `line_of(A, B)`: The line through points A and B (requires A ≠ B)

### 3. Plane

**Definition**: A plane is a set of points, uniquely determined by three non-collinear points.

**Main Properties**:
- For any three non-collinear points A, B, C, there exists a unique plane containing them, denoted as `plane_of(A, B, C)`
- Every plane contains at least one point
- A plane is a set of points: `pl $in power_set(point)`
- If two points on a line are in a plane, then the entire line is in that plane

**Key Functions**:
- `plane_of(A, B, C)`: The plane through three non-collinear points A, B, C
- `plane_of_point_and_line(A, l)`: The plane through point A and line l (requires A not on l)

### 4. Ray

**Definition**: A ray is a set of points extending infinitely from an endpoint in a given direction.

**Main Properties**:
- A ray is a set of points: `r $in power_set(point)`
- Every ray has a unique endpoint (starting point)
- A ray is uniquely determined by its endpoint and a direction point

**Key Functions**:
- `ray_with_end_point_and_direction(A, B)`: The ray with endpoint A passing through B
- `end_point_of(r)`: The endpoint of ray r
- `converse_extension_ray_of(r)`: The opposite extension ray of r

**Relations**:
- If point C is on the ray `ray_with_end_point_and_direction(A, B)`, then C is on line AB
- Point C is on the ray if and only if C is between A and B, or B is between A and C

### 5. Finite Line (Segment)

**Definition**: A finite line (segment) is the set of all points between two endpoints on a line.

**Main Properties**:
- A finite line is a set of points: `fl $in power_set(point)`
- A finite line is uniquely determined by its two endpoints
- `finite_line_of(A, B)` and `finite_line_of(B, A)` are the same segment
- If point C is on segment AB and C ≠ A, B, then C is between A and B

**Key Functions**:
- `finite_line_of(A, B)`: The segment with endpoints A and B
- `length_of_finite_line(fl)`: The length of segment fl (a real number)

### 6. Angle

**Definition**: An angle is a figure formed by two rays with a common endpoint.

**Main Properties**:
- An angle is a set of points: `a $in power_set(point)`
- An angle is uniquely determined by its two sides (rays)
- Every angle has a degree measure: `deg_of_angle(a)` returns the angle's degree measure (a real number)

**Key Functions**:
- `angle_of_two_rays(r1, r2)`: The angle formed by rays r1 and r2 (requires the two rays to have a common endpoint)
- `sides_of(a)`: The two sides of angle a
- `start_point_of(a)`: The vertex of angle a

**Special Angles**:
- Right angle: `is_right_angle(a)` indicates that angle a is a right angle (90 degrees)

### 7. Circle

**Definition**: A circle is the set of all points in a plane that are at a fixed distance (radius) from a fixed point (center).

**Main Properties**:
- A circle is a set of points: `c $in power_set(point)`
- A circle is uniquely determined by its center and radius
- Point P is on the circle `circle_of_center_with_radius(O, r)` if and only if `length_of_finite_line(finite_line_of(O, P)) = r`

**Key Functions**:
- `circle_of_center_with_radius(O, r)`: The circle with center O and radius r
- `center_of_circle(c)`: The center of circle c
- `radius_of_circle(c)`: The radius of circle c
- `circle_of_triangle(A, B, C)`: The circumcircle of triangle ABC

---

## Basic Relations

### 1. Incidence Relation

The incidence relation describes the containment relationships between points, lines, and planes.

**Main Properties**:
- **I1**: Any two distinct points determine a unique line
- **I2**: Every line contains at least two points
- **I3**: There exist three non-collinear points
- **I4**: Any three non-collinear points determine a unique plane
- **I5**: Every plane contains at least three non-collinear points
- **I6**: If two points on a line are in a plane, then the entire line is in that plane
- **I7**: If two planes have a common point, then they have at least one more common point
- **I8**: There exist four non-coplanar points

**Key Predicates**:
- `A $in l`: Point A is on line l
- `A $in pl`: Point A is on plane pl
- `line_on_plane(l, pl)`: Line l is on plane pl
- `three_points_collinear(A, B, C)`: Points A, B, C are collinear

### 2. Betweenness Relation

The betweenness relation describes the ordering of three collinear points.

**Main Properties**:
- **B1**: If point B is between A and C, then B is also between C and A
- **B2**: For any two points A and C, there exists a point B such that C is between A and B
- **B3**: For any three collinear points, at most one point lies between the other two

**Key Predicates**:
- `point_between(B, A, C)`: Point B is between points A and C (requires A, B, C to be collinear and distinct)

**Pasch's Axiom**: If a line intersects one side of a triangle, then it must intersect another side.

### 3. Congruence Relation

The congruence relation describes the equality of segments and angles.

#### Segment Congruence

**Main Properties**:
- **C1**: For any segment AB and point A', we can find a point B' on the line through A' such that AB ≅ A'B'
- **C2**: Segment congruence is reflexive, symmetric, and transitive
- **C3**: If AB ≅ A'B' and BC ≅ B'C', then AC ≅ A'C' (segment additivity)

**Key Predicates**:
- `finite_line_congruence(fl1, fl2)`: Segments fl1 and fl2 are congruent

#### Angle Congruence

**Main Properties**:
- **C4**: For any angle and a given ray, we can construct a congruent angle on a specified side
- **C5**: Angle congruence is reflexive, symmetric, and transitive
- **C6**: SAS (Side-Angle-Side) criterion for triangle congruence

**Key Predicates**:
- `angle_congruence(a1, a2)`: Angles a1 and a2 are congruent

### 4. Parallel Relation

**Definition**: Two lines are parallel if and only if they are coplanar and do not intersect.

**Main Properties**:
- **P1 (Playfair's Axiom)**: Through a point not on a line, there is exactly one line parallel to the given line
- If two lines both pass through the same point and are parallel, then they are the same line

**Key Predicates**:
- `parallel_line(l1, l2)`: Lines l1 and l2 are parallel
- `line_coplanar(l1, l2)`: Lines l1 and l2 are coplanar
- `intersect_of_two_lines(l1, l2)`: Lines l1 and l2 intersect

**Key Functions**:
- `intersection_point(l1, l2)`: The intersection point of two intersecting lines

### 5. Perpendicular Relation

**Definition**: Two lines are perpendicular if and only if they intersect and form a right angle.

**Key Predicates**:
- `perp(l1, l2)`: Lines l1 and l2 are perpendicular

**Related Concepts**:
- `foot(A, l)`: The foot of the perpendicular from point A to line l
- `distance_of_point_to_line(A, l)`: The distance from point A to line l

### 6. Same-Side / Opposite-Side (Relative to a Line)

These relations describe whether two points lie on the same side of a given line (in the plane determined by the points and the line).

**Key Predicates**:
- `sameside_points(A, C, l)`: Points A and C are on the **same side** of line `l`
- `not_sameside_points(A, C, l)`: Points A and C are on **opposite sides** of line `l`

**How it is encoded in `new_version.lit` (high level)**:
- Both points are required to lie in the plane `plane_of_point_and_line(C, l)`, and neither point lies on `l`.
- Let `X = intersection_point(l, line_of(A, C))` (so `AC` is not parallel to `l`).
  - Same-side: `X` is **not** on the segment `finite_line_of(A, C)` (i.e., the line `l` does not cut the segment between A and C).
  - Opposite-side: `X` **is** on the segment `finite_line_of(A, C)` (i.e., the line `l` cuts the segment between A and C).

---

## Composite Geometric Figures

### 1. Triangle

**Definition**: A figure determined by three non-collinear points.

**Main Properties**:
- A triangle is a set of points: `T $in power_set(point)`
- Point P is on triangle ABC if and only if P is on side AB, BC, or CA

**Key Functions**:
- `triangle_of(A, B, C)`: The triangle with vertices A, B, C (requires three non-collinear points)

**Special Triangles**:
- `is_iso_triangle(A, B, C)`: Isosceles triangle (AB = AC)
- `is_r_triangle(A, B, C)`: Right triangle (AB ⟂ AC)
- `is_ieq_triangle(A, B, C)`: Equilateral triangle (all sides equal, all angles equal)
- `is_risos(A, B, C)`: Right isosceles triangle

**Triangle Congruence**:
- `triangle_congruence(A, B, C, A', B', C')`: Triangle ABC is congruent to triangle A'B'C'

### 2. Quadrangle

**Definition**: A quadrilateral determined by four points.

**Key Predicates**:
- `is_quadrangle(A, B, C, D)`: Points A, B, C, D form a quadrangle
- `is_eq_quadrangle(A, B, C, D)`: Equilateral quadrangle (opposite sides equal)

**Special Quadrangles**:
- `is_trapezoid(A, B, C, D)`: Trapezoid (AB ∥ CD)
- `is_eq_trapezoid(A, B, C, D)`: Isosceles trapezoid
- `is_parallelogram(A, B, C, D)`: Parallelogram
- `is_rectangle(A, B, C, D)`: Rectangle
- `is_square(A, B, X, Y)`: Square

### 3. Pentagon

**Definition**: A pentagon determined by five non-collinear points.

**Key Predicates**:
- `is_pentagon(A, B, C, D, E)`: Points A, B, C, D, E form a pentagon

---

## Geometric Quantities

### 1. Length

**Functions**:
- `length_of_finite_line(fl)`: The length of segment fl (a real number)

**Properties**:
- Congruent segments have equal lengths

### 2. Angle Measure

**Functions**:
- `deg_of_angle(a)`: The degree measure of angle a (a real number)

**Properties**:
- Congruent angles have equal measures

### 3. Distance

**Functions**:
- `distance_of_point_to_line(A, l)`: The distance from point A to line l (a positive real number)

---

## Special Points and Lines

### 1. Midpoint

**Definition**: The point on a segment that is equidistant from both endpoints.

**Key Functions**:
- `mid_point_of(A, B)`: The midpoint of segment AB

**Key Predicates**:
- `is_mid_point(M, A, B)`: M is the midpoint of segment AB

### 2. Angle Bisector

**Definition**: A ray that divides an angle into two equal parts.

**Key Functions**:
- `angle_bisector_of(r1, r2)`: The angle bisector of the angle formed by rays r1 and r2

### 3. Foot

**Definition**: The intersection point of the perpendicular from a point to a line with that line.

**Key Functions**:
- `foot(A, l)`: The foot of the perpendicular from point A to line l

### 4. Centroid

**Definition**: The intersection point of the three medians of a triangle.

**Key Functions**:
- `centroid_of(A, B, C)`: The centroid of triangle ABC

### 5. Incenter

**Definition**: The intersection point of the three angle bisectors of a triangle.

**Key Functions**:
- `incenter_of(A, B, C)`: The incenter of triangle ABC

### 6. Circumcenter

**Definition**: The center of the circumcircle of a triangle.

**Key Predicates**:
- `center_of_circle_of_triangle(O, A, B, C)`: O is the circumcenter of triangle ABC

### 7. Orthocenter

**Definition**: The intersection point of the three altitudes of a triangle.

**Key Functions**:
- `orthocenter_of(A, B, C)`: The orthocenter of triangle ABC

### 8. Perpendicular Bisector

**Definition**: A line that passes through the midpoint of a segment and is perpendicular to it.

**Related Concepts**:
- `is_on_bline(X, A, B)`: Point X is on the perpendicular bisector of AB

---

## Circle-Related Concepts

### 1. Relations Between Points and Circles

- `intersect_of_line_and_circle(l, c)`: A line intersects a circle
- `line_is_tangent_to_circle(l, c)`: A line is tangent to a circle
- `line_and_circle_disjiont(l, c)`: A line and a circle are disjoint

### 2. Relations Between Circles

- `two_circles_intersect(c1, c2)`: Two circles intersect
- `two_tangent_circles(c1, c2)`: Two circles are tangent
- `two_disjiont_circles(c1, c2)`: Two circles are disjoint

### 3. Points of Tangency

- `tangency_point_of_line_and_circle(l, c)`: The point of tangency between a line and a circle
- `tangency_point_of_circles(c1, c2)`: The point of tangency between two circles
- `tangent_points(A, O, B)`: The points of tangency of the two tangents from point A to the circle (with center O, passing through B)

### 4. Common Tangents of Two Circles (Internal / External)

The file `new_version.lit` distinguishes **external common tangents** and **internal common tangents** of two circles using a same-side test on the circle centers relative to the tangent line.

**Key Predicates (classifying a tangent line)**:
- `is_cc_external_tangent_line(c1, c2, l)`: Line `l` is an **external** common tangent of circles `c1` and `c2`
  - Encoded as: `l` is tangent to both circles (distance from each center to `l` equals its radius) and the two centers are on **opposite sides** of `l` (`not_sameside_points(center_of_circle(c1), center_of_circle(c2), l)`).
- `is_cc_internal_tangent_line(c1, c2, l)`: Line `l` is an **internal** common tangent of circles `c1` and `c2`
  - Encoded as: `l` is tangent to both circles and the two centers are on the **same side** of `l` (`sameside_points(center_of_circle(c1), center_of_circle(c2), l)`).

**Key Construction Predicates (tangency points)**:
- `is_cc_tangent0(X, Y, O, A, W, B)`: Constructs **one** common tangent via its two tangency points `X` (on the circle centered at `O` through `A`) and `Y` (on the circle centered at `W` through `B`), with perpendicularity constraints indicating tangency.
- `is_cc_tangent(X, Y, z, I, O, A, W, B)`: Constructs **two** common tangents (four tangency points), giving tangency points `(X, Y)` and `(z, I)` for the two tangent lines.

---

## Continuity Axiom

### Archimedes' Axiom

For any two segments AB and CD, there exists a positive integer n such that n segments of length CD, placed consecutively from A along the direction of AB, will extend beyond point B.

**Key Predicates**:
- `archimedes_number(A, B, C, D, n)`: n is a positive integer satisfying Archimedes' Axiom

---
