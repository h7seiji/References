# Geometry

## Corner cases

- Zero values. This always gets people.

## Techniques

- Distance between two points
  When comparing the distance between two points, using dx^2 + dy^2 is sufficient. It is unnecessary to square root the value. Examples: K Closest Points to Origin

- Overlapping circles
  To find out if two circles overlap, check that the distance between the two centers of the circles is less than the sum of their radii.

- Overlapping rectangles
  Two rectangles overlap if the following is true:

```
overlap = rect_a.left < rect_b.right and \
  rect_a.right > rect_b.left and \
  rect_a.top > rect_b.bottom and \
  rect_a.bottom < rect_b.top
```
