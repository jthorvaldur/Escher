# Escher — Hyperbolic Tilings of the Poincare Disk

A Python script for generating Escher-like tilings of the Poincare disk model of hyperbolic geometry. Given a triangle satisfying the hyperbolic constraint `1/p + 1/q + 1/r < 1`, the script fills the disk with reflected copies of user-supplied images, producing the kind of infinite, self-similar patterns seen in M.C. Escher's *Circle Limit* woodcuts.

**Original author:** Balazs Strenner, UW-Madison Mathematics Department (initial C++ version 2006; Python rewrite January 2014).
**Forked by:** Joel Thorarinson.

Distributed under the [GNU General Public License (GPL)](http://www.gnu.org/licenses/).

---

## Mathematical Background

### The Poincare Disk

The Poincare disk is a model of hyperbolic geometry in which the points are the interior of the unit disk and the "lines" are either diameters through the origin or circular arcs that meet the unit circle at right angles. A hyperbolic triangle is a region bounded by three such line segments. Angles between hyperbolic lines are measured the same way as Euclidean angles — but the angle-sum of a hyperbolic triangle is always *strictly less* than 180 degrees, and can take any value in the open interval (0, 180).

### Euclidean Tilings by Reflection

On the Euclidean plane, start with a triangle and keep reflecting it across its own sides. You tile the whole plane (without overlap or gaps) only when every angle of the triangle evenly divides 360 degrees, i.e., each angle equals `360/a` for some positive integer `a >= 3`. The angle-sum condition `360/a + 360/b + 360/c = 180` then reduces to:

```
1/a + 1/b + 1/c = 1/2
```

Only three triples satisfy this: **(3, 6, 6)**, **(4, 6, 12)**, and **(6, 6, 6)**.

### Hyperbolic Tilings

In the hyperbolic plane the constraint relaxes to a strict inequality:

```
1/a + 1/b + 1/c < 1/2
```

Infinitely many integer triples satisfy this, which is why hyperbolic tilings are so much richer than Euclidean ones.

### Even-Angle Restriction

When all of `a`, `b`, `c` are even, every edge of every triangle lies along a full line of the tessellation — the geometry is clean. When any value is odd, reflection lines cut through the interiors of neighboring triangles and the combinatorics get more complicated. This script therefore works with the parametrization `(a, b, c) = (2p, 2q, 2r)`, giving the **triangle condition**:

```
1/p + 1/q + 1/r < 1
```

where `p`, `q`, `r` are positive integers. The script computes the triangle vertices via the hyperbolic law of cosines and maps pixels through Moebius transformations to produce the final tiling.

---

## What the Program Does

- Constructs a hyperbolic triangle with angles `pi/p`, `pi/q`, `pi/r` inside the Poincare disk.
- For each pixel in the output image, reflects it back into the fundamental triangle using the three boundary lines, counting reflections.
- Fills each triangle with a user-supplied image (or a solid color), using barycentric-like weight coordinates adapted to hyperbolic geometry via Ceva's theorem.
- Multiple images can be provided: with two images they alternate (e.g. Tom and Jerry chasing each other to infinity); with more, the assignment cycles by reflection count.
- Triangles whose source coordinates fall outside the input image are filled with a configurable default color.

---

## Requirements

- **Python 3**
- **Pillow** (the maintained fork of PIL)

Install Pillow with:

```bash
pip install Pillow
```

---

## Usage

### Basic: two alternating images

```python
import escher

triangle_image = escher.TriangleImage("stinkbug.png", ((0, 599), (0, 0), (799, 0)))
triangle_image2 = escher.TriangleImage(default_color=(50, 223, 146))
escher.create_image([triangle_image, triangle_image2], 3, 3, 4, 500, "output.png")
```

### From a rectangular image

The helper `create_image_from_rectangle` splits a rectangular image into upper-left and lower-right triangles automatically:

```python
escher.create_image_from_rectangle("stinkbug.png", 5, 5, 5, 500, "output.png")
```

This is shorthand for:

```python
t1 = escher.TriangleImage("stinkbug.png", ((0, 599), (0, 0), (799, 0)))
t2 = escher.TriangleImage("stinkbug.png", ((0, 599), (799, 599), (799, 0)))
escher.create_image([t1, t2], 3, 3, 4, 500, "output.png")
```

### Solid-color tiling

```python
t1 = escher.TriangleImage(default_color=(255, 0, 0))
t2 = escher.TriangleImage(default_color=(0, 255, 0))
t3 = escher.TriangleImage(default_color=(0, 0, 255))
escher.create_image([t1, t2, t3], 6, 9, 12, 1000, "colorful.png")
```

### API Reference

**`TriangleImage(image_file=None, vertices=None, default_color=(255, 255, 255))`**

- `image_file` — path to an image file. If omitted, the triangle is filled with `default_color`.
- `vertices` — list of three `(x, y)` pixel coordinates, or the string `"upperleft"` / `"bottomright"` to auto-clip from a rectangular image. Out-of-bounds coordinates are accepted; missing pixels get `default_color`.
- `default_color` — RGB tuple, default white `(255, 255, 255)`.

**`create_image(triangle_images, p, q, r, size, output_file_name)`**

- `triangle_images` — list of `TriangleImage` objects. The count must divide all of `p`, `q`, `r`.
- `p`, `q`, `r` — positive integers satisfying `1/p + 1/q + 1/r < 1`.
- `size` — output image is `size x size` pixels.
- `output_file_name` — output path with extension (e.g. `"output.png"`).

**`create_image_from_rectangle(input_file_name, p, q, r, size, output_file_name)`**

Convenience wrapper that splits a rectangular image into two triangles and calls `create_image`.

---

## Running Tests

The module includes doctests:

```bash
python escher.py
```
