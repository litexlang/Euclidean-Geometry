 欧几里得几何概念介绍

本文档介绍 `new_version.lit` 文件中定义的欧几里得几何基本概念及其相互关系。

## 目录

1. [基本几何对象](#基本几何对象)
2. [基本关系](#基本关系)
3. [复合几何图形](#复合几何图形)
4. [几何量](#几何量)
5. [特殊点和线](#特殊点和线)

---

## 基本几何对象

### 1. 点 (Point)

**定义**：点是几何学中最基本的概念，是一个非空集合。
*性质**：
- 点是所有其他几何对象的基础
- 直线和平面都可以看作是点的集合

### 2. 直线 (Line)

**定义**：直线是点的集合，由两个不同的点唯一确定。

**主要性质**：
- 对于任意两个不同的点 A 和 B，存在唯一一条直线包含它们，记作 `line_of(A, B)` 或 `AB`
- 每条直线上至少存在两个点
- 直线是点的集合：`l $in power_set(point)`

**关键函数**：
- `line_of(A, B)`：通过点 A 和 B 的直线（要求 A ≠ B）

### 3. 平面 (Plane)

**定义**：平面是点的集合，由三个不共线的点唯一确定。

**主要性质**：
- 对于任意三个不共线的点 A、B、C，存在唯一一个平面包含它们，记作 `plane_of(A, B, C)`
- 每个平面上至少存在一个点
- 平面是点的集合：`pl $in power_set(point)`
- 如果一条直线上的两个点都在平面上，则整条直线都在该平面上

**关键函数**：
- `plane_of(A, B, C)`：通过不共线三点 A、B、C 的平面
- `plane_of_point_and_line(A, l)`：通过点 A 和直线 l 的平面（要求 A 不在 l 上）

### 4. 射线 (Ray)

**定义**：射线是从一个端点出发，沿某个方向无限延伸的点的集合。

**主要性质**：
- 射线是点的集合：`r $in power_set(point)`
- 每条射线有唯一的端点（起点）
- 射线由其端点和方向点唯一确定

**关键函数**：
- `ray_with_end_point_and_direction(A, B)`：以 A 为端点，通过 B 的射线
- `end_point_of(r)`：射线 r 的端点
- `converse_extension_ray_of(r)`：射线 r 的反向延长线
**关系**：
- 如果点 C 在射线 `ray_with_end_point_and_direction(A, B)` 上，则 C 在直线 AB 上
- 点 C 在射线上当且仅当 C 在 A 和 B 之间，或 B 在 A 和 C 之间

### 5. 线段 (Finite Line)

**定义**：线段是直线上两个端点之间的所有点的集合。

**主要性质**：
- 线段是点的集合：`fl $in power_set(point)`
- 线段由其两个端点唯一确定
- 线段 `finite_line_of(A, B)` 和 `finite_line_of(B, A)` 是同一个线段
- 如果点 C 在线段 AB 上且 C ≠ A, B，则 C 在 A 和 B 之间

**关键函数**：
- `finite_line_of(A, B)`：以 A 和 B 为端点的线段
- `length_of_finite_line(fl)`：线段 fl 的长度（实数）

### 6. 角 (Angle)

**定义**：角是由两条具有公共端点的射线形成的图形。

**主要性质**：
- 角是点的集合：`a $in power_set(point)`
- 角由其两条边（射线）唯一确定
- 每个角都有度数：`deg_of_angle(a)` 返回角的度数（实数）

**关键函数**：
- `angle_of_two_rays(r1, r2)`：由射线 r1 和 r2 形成的角（要求两条射线有公共端点）
- `sides_of(a)`：角 a 的两条边
- `start_point_of(a)`：角的顶点
**特殊角**：
- 直角：`is_right_angle(a)` 表示角 a 是直角（90度）

### 7. 圆 (Circle)

**定义**：圆是平面上到定点（圆心）距离等于定长（半径）的所有点的集合。

**主要性质**：
- 圆是点的集合：`c $In power_set(point)`
- 圆由其圆心和半径唯一确定
- 点 P 在圆 `circle_of_center_with_radius(O, r)` 上当且仅当 `length_of_finite_line(finite_line_of(O, P)) = r`

**关键函数**：
- `circle_of_center_with_radius(O, r)`：以 O 为圆心、r 为半径的圆
- `center_of_circle(c)`：圆 c 的圆心
- `radius_of_circle(c)`：圆 c 的半径
- `circle_of_triangle(A, B, C)`：三角形 ABC 的外接圆

---
## 基本关系

### 1. 关联关系 (Incidence)

关联关系描述点、直线、平面之间的包含关系。

**主要性质**：
- **I1**：任意两个不同的点确定唯一一条直线
- **I2**：每条直线上至少有两个点
- **I3**：存在三个不共线的点
- **I4**：任意三个不共线的点确定唯一一个平面
- **I5**：每个平面至少包含三个不共线的点
- **I6**：如果一条直线上的两个点都在平面上，则整条直线在平面上
- **I7**：如果两个平面有公共点，则它们至少还有另一个公共点
- **I8**：存在四个不共面的点

**关键谓词**：
- `A $in l`：点 A 在直线 l 上
- `A $in pl`：点 A 在平面 pl 上
- `line_on_plane(l, pl)`：直线 l 在平面 pl 上
- `three_points_collinear(A, B, C)`：三点 A、B、C 共线
### 2. 介于关系 (Betweenness)

介于关系描述三个共线点的顺序关系。

**主要性质**：
- **B1**：如果点 B 在 A 和 C 之间，则 B 也在 C 和 A 之间
- **B2**：对于任意两点 A 和 C，存在点 B 使得 C 在 A 和 B 之间
- **B3**：对于任意三个共线的点，最多有一个点在另外两个点之间

**关键谓词**：
- `point_between(B, A, C)`：点 B 在点 A 和 C 之间（要求 A、B、C 共线且互不相同）

**Pasch 公理**：如果一条直线与三角形的一条边相交，则它必与另一条边相交。

### 3. 全等关系 (Congruence)

全等关系描述线段和角的相等关系。

#### 线段全等
**主要性质**：
- **C1**：对于任意线段 AB 和点 A'，可以在 A' 所在直线上找到点 B'，使得 AB ≅ A'B'
- **C2**：线段全等具有自反性、对称性和传递性
- **C3**：如果 AB ≅ A'B' 且 BC ≅ B'C'，则 AC ≅ A'C'（线段可加性）

**关键谓词**：
- `finite_line_congruence(fl1, fl2)`：线段 fl1 和 fl2 全等

#### 角全等

**主要性质**：
- **C4**：对于任意角和给定射线，可以在指定一侧构造全等的角
- **C5**：角全等具有自反性、对称性和传递性
- **C6**：三角形全等的 SAS 判定法则

**关键谓词**：
- `angle_congruence(a1, a2)`：角 a1 和 a2 全等

### 4. 平行关系 (Parallel)

**定义**：两条直线平行当且仅当它们共面且不相交。

**主要性质**：
- **P1（Playfair 公理）**：过直线外一点，有且仅有一条直线与已知直线平行
- 如果两条直线都经过同一点且平行，则它们是同一条直线
**关键谓词**：
- `parallel_line(l1, l2)`：直线 l1 和 l2 平行
- `line_coplanar(l1, l2)`：直线 l1 和 l2 共面
- `intersect_of_two_lines(l1, l2)`：直线 l1 和 l2 相交

**关键函数**：
- `intersection_point(l1, l2)`：两条相交直线的交点

### 5. 垂直关系 (Perpendicular)

**定义**：两条直线垂直当且仅当它们相交且形成的角是直角。

**关键谓词**：
- `perp(l1, l2)`：直线 l1 和 l2 垂直

**相关概念**：
- `foot(A, l)`：点 A 到直线 l 的垂足
- `distance_of_point_to_line(A, l)`：点 A 到直线 l 的距离

---
## 复合几何图形

### 1. 三角形 (Triangle)

**定义**：由三个不共线的点确定的图形。

**主要性质**：
- 三角形是点的集合：`T $in power_set(point)`
- 点 P 在三角形 ABC 上当且仅当 P 在边 AB、BC 或 CA 上

**关键函数**：
- `triangle_of(A, B, C)`：以 A、B、C 为顶点的三角形（要求三点不共线）

**特殊三角形**：
- `is_iso_triangle(A, B, C)`：等腰三角形（AB = AC）
- `is_r_triangle(A, B, C)`：直角三角形（AB ⟂ AC）
- `is_ieq_triangle(A, B, C)`：等边三角形（三边相等，三角相等）
- `is_risos(A, B, C)`：等腰直角三角形

**三角形全等**：
- `triangle_congruence(A, B, C, A', B', C')`：三角形 ABC 与 A'B'C' 全等
### 2. 四边形 (Quadrangle)

**定义**：由四个点确定的四边形。

**关键谓词**：
- `is_quadrangle(A, B, C, D)`：A、B、C、D 构成四边形
- `is_eq_quadrangle(A, B, C, D)`：等边四边形（对边相等）

**特殊四边形**：
- `is_trapezoid(A, B, C, D)`：梯形（AB ∥ CD）
- `is_eq_trapezoid(A, B, C, D)`：等腰梯形
- `is_parallelogram(A, B, C, D)`：平行四边形
- `is_rectangle(A, B, C, D)`：矩形
- `is_square(A, B, X, Y)`：正方形
### 3. 五边形 (Pentagon)

**定义**：由五个不共线的点确定的五边形。

**关键谓词**：
- `is_pentagon(A, B, C, D, E)`：A、B、C、D、E 构成五边形

---
## 几何量

### 1. 长度 (Length)

**函数**：
- `length_of_finite_line(fl)`：线段 fl 的长度（实数）

**性质**：
- 全等的线段长度相等

### 2. 角度 (Angle Measure)

**函数**：
- `deg_of_angle(a)`：角 a 的度数（实数）

**性质**：
- 全等的角度数相等

### 3. 距离 (Distance)

**函数**：
- `distance_of_point_to_line(A, l)`：点 A 到直线 l 的距离（正实数）

---
## 特殊点和线

### 1. 中点 (Midpoint)

**定义**：线段上到两端点距离相等的点。

**关键函数**：
- `mid_point_of(A, B)`：线段 AB 的中点

**关键谓词**：
- `is_mid_point(M, A, B)`：M 是线段 AB 的中点

### 2. 角平分线 (Angle Bisector)

**定义**：将角分成两个相等部分的射线。

**关键函数**：
- `angle_bisector_of(r1, r2)`：由射线 r1 和 r2 形成的角的角平分线

### 3. 垂足 (Foot)

**定义**：从一点到直线的垂线与直线的交点。

**关键函数**：
- `foot(A, l)`：点 A 到直线 l 的垂足
### 4. 重心 (Centroid)

**定义**：三角形三条中线的交点。

**关键函数**：
- `centroid_of(A, B, C)`：三角形 ABC 的重心

### 5. 内心 (Incenter)

**定义**：三角形三条角平分线的交点。

**关键函数**：
- `incenter_of(A, B, C)`：三角形 ABC 的内心

### 6. 外心 (Circumcenter)

**定义**：三角形外接圆的圆心。

**关键谓词**：
- `center_of_circle_of_triangle(O, A, B, C)`：O 是三角形 ABC 的外心

### 7. 垂心 (Orthocenter)

**定义**：三角形三条高线的交点。

**关键函数**：
- `orthocenter_of(A, B, C)`：三角形 ABC 的垂心
### 8. 垂直平分线 (Perpendicular Bisector)

**定义**：过线段中点且垂直于该线段的直线。

**相关概念**：
- `is_on_bline(X, A, B)`：点 X 在 AB 的垂直平分线上

---
## 圆的相关概念

### 1. 点与圆的关系

- `intersect_of_line_and_circle(l, c)`：直线与圆相交
- `line_is_tangent_to_circle(l, c)`：直线与圆相切
- `line_and_circle_disjiont(l, c)`：直线与圆相离

### 2. 圆与圆的关系

- `two_circles_intersect(c1, c2)`：两圆相交
- `two_tangent_circles(c1, c2)`：两圆相切
- `two_disjiont_circles(c1, c2)`：两圆相离

### 3. 切点

- `tangency_point_of_line_and_circle(l, c)`：直线与圆的切点
- `tangency_point_of_circles(c1, c2)`：两圆的切点
- `tangent_points(A, O, B)`：从点 A 到圆（圆心 O，过点 B）的两条切线的切点

---
## 连续性公理

### 阿基米德公理 (Archimedes' Axiom)

对于任意两条线段 AB 和 CD，存在正整数 n，使得 n 个 CD 长度的线段连续排列，从 A 沿 AB 方向延伸，会超过点 B。

**关键谓词**：
- `archimedes_number(A, B, C, D, n)`：n 是满足阿基米德公理的正整数

---
