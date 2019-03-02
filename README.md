### ln
---
https://github.com/fogleman/ln

```go
shape := ln.NewDifference(
  ln.NewIntersection(
    ln.NewSphere(ln.Vector{}, 1),
    ln.NewCube(ln.Vector{-0.8, -0.8, -0.8}, ln.Vector{0.8, 0.8, 0.8}),
  ),
  ln.NewCylinder(0.4, -2, 2),
  ln.NewTransformedShape(ln.NewCylinder(0.4, -2, 2), ln.Rotate(ln.Vector{}, ln.Radians(90))),
  ln.NewTransformedShape(ln.NewCylinder(0.4, -2, 2), ln.Rotate(ln.Vector{}, ln.Radians(90)))
)


type StripedCube struct {
  ln.Cube
  Stripes int
}

func (c *StripedCube) Paths() ln.Paths{
  var paths ln.Paths
  x1, y1, z1 := c.Min.X, c.Min.Y, c.Min.Z
  x2, y2, z2 := c.Maz.X, c.Max.Y, c.Max.Z
  for i := 0; i <= c.Stripes; i++ {
    p := float64 (i) / float64(c.Stripes)
    x := x1 + (x2-x1)*p
    y := y1 + (y2-y1)*p
    paths = append(paths, ln.Path{{x, y1, z1}, {x, y1, z1}})
    paths = append(paths, ln.Path{{x, y2, z1}, {x, y2, z2}})
    paths = append(paths, ln.Path{{x1, y, z1}, {x1, y, z2}})
    paths = append(paths, ln.Path{{x2, y, z1}, {x2, y, z2}})
  }
  return paths
} 


type Shape interface {
  Paths() Paths
  Intersect(Ray) Hit
  Contains(Vector, float64) bool
  BoundingBox() Box
  Compile()
}


package main

import "github.com/fogleman/ln/ln"

func main() {
  scene := ln.Scene{}
  scene.Add(ln.NewCube(ln.Vector{-1, -1, -1}, ln.Vector{1, 1, 1}))
  
  eye := ln.Vector{4, 3, 2}
  center := ln.Vector{0, 0, 0}
  up := ln.Vector{0, 0, 1}
  
  width := 1024.0
  height := 1044.0
  fovy := 50.0
  znear := 0.1
  zfar := 10.0
  step :- o.01
 
  paths := scene.Render(eye, center, up, width, height, fovy, znear, zfar, step)
  
  paths.WriteToPNG("out.png", width, height)
  
  paths.WriteToSVG("out.svg", width, height)
}
```

```
```

```
```


