---
source_url: https://go.dev/pkg/image/draw/
title: draw package - image/draw - Go Packages
crawl_date: 2025-07-25T12:08:27.426226
watsonmd_version: 0.1.0
---

[ ![Go](/static/shared/logo/go-blue.svg) ](https://go.dev/)

# draw

package standard library ![](/static/shared/icon/content_copy_gm_grey_24dp.svg)

[ Version:  go1.24.5 ](?tab=versions)

Opens a new window with list of versions in this module. 

Latest Latest  ![Warning](/static/shared/icon/alert_gm_grey_24dp.svg)

This package is not in the latest version of its module.

[ Go to latest ](/image/draw) Published: Jul 8, 2025  License: [BSD-3-Clause](/image/draw?tab=licenses)

Opens a new window with license information. 

[ Imports: 3 ](/image/draw?tab=imports)

Opens a new window with list of imports. 

[ Imported by: 11,220 ](/image/draw?tab=importedby)

Opens a new window with list of known importers. 

Main Versions  Licenses  Imports  Imported By 

## Details

  * ![checked](/static/shared/icon/check_circle_gm_grey_24dp.svg) Valid [go.mod](https://cs.opensource.google/go/go/+/go1.24.5:src/go.mod) file ![](/static/shared/icon/help_gm_grey_24dp.svg)

The Go module system was introduced in Go 1.11 and is the official dependency management solution for Go. 

  * ![checked](/static/shared/icon/check_circle_gm_grey_24dp.svg) Redistributable license ![](/static/shared/icon/help_gm_grey_24dp.svg)

Redistributable licenses place minimal restrictions on how software can be used, modified, and redistributed. 

  * ![checked](/static/shared/icon/check_circle_gm_grey_24dp.svg) Tagged version ![](/static/shared/icon/help_gm_grey_24dp.svg)

Modules with tagged versions give importers more predictable builds.

  * ![checked](/static/shared/icon/check_circle_gm_grey_24dp.svg) Stable version ![](/static/shared/icon/help_gm_grey_24dp.svg)

When a project reaches major version v1 it is considered stable.

  * [Learn more about best practices](/about#best-practices)



## Repository

[ cs.opensource.google/go/go ](https://cs.opensource.google/go/go "https://cs.opensource.google/go/go")

## Links

  * [ ![](/static/shared/icon/security_grey_24dp.svg) Report a Vulnerability ](https://go.dev/security/policy "Report security issues in the Go standard library and sub-repositories")



##  ![](/static/shared/icon/code_gm_grey_24dp.svg) Documentation ¶

### Overview ¶

Package draw provides image composition functions. 

See "The Go image/draw package" for an introduction to this package: <https://golang.org/doc/articles/image_draw.html>

### Index ¶

  * func Draw(dst Image, r image.Rectangle, src image.Image, sp image.Point, op Op)
  * func DrawMask(dst Image, r image.Rectangle, src image.Image, sp image.Point, ...)
  * type Drawer
  * type Image
  * type Op
  *     * func (op Op) Draw(dst Image, r image.Rectangle, src image.Image, sp image.Point)
  * type Quantizer
  * type RGBA64Image



#### Examples ¶

  * Drawer (FloydSteinberg)



### Constants ¶

This section is empty.

### Variables ¶

This section is empty.

### Functions ¶

####  func [Draw](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=110) ¶

    
    
    func Draw(dst Image, r [image](/image).[Rectangle](/image#Rectangle), src [image](/image).[Image](/image#Image), sp [image](/image).[Point](/image#Point), op Op)

Draw calls DrawMask with a nil mask. 

####  func [DrawMask](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=116) ¶

    
    
    func DrawMask(dst Image, r [image](/image).[Rectangle](/image#Rectangle), src [image](/image).[Image](/image#Image), sp [image](/image).[Point](/image#Point), mask [image](/image).[Image](/image#Image), mp [image](/image).[Point](/image#Point), op Op)

DrawMask aligns r.Min in dst with sp in src and mp in mask and then replaces the rectangle r in dst with the result of a Porter-Duff composition. A nil mask is treated as opaque. 

### Types ¶

####  type [Drawer](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=60) ¶ added in go1.2

    
    
    type Drawer interface {
    	// Draw aligns r.Min in dst with sp in src and then replaces the
    	// rectangle r in dst with the result of drawing src on dst.
    	Draw(dst Image, r [image](/image).[Rectangle](/image#Rectangle), src [image](/image).[Image](/image#Image), sp [image](/image).[Point](/image#Point))
    }

Drawer contains the Draw method. 

Example (FloydSteinberg) ¶
    
    
    package main
    
    import (
    	"fmt"
    	"image"
    	"image/color"
    	"image/draw"
    	"math"
    )
    
    func main() {
    	const width = 130
    	const height = 50
    
    	im := image.NewGray(image.Rectangle{Max: image.Point{X: width, Y: height}})
    	for x := 0; x < width; x++ {
    		for y := 0; y < height; y++ {
    			dist := math.Sqrt(math.Pow(float64(x-width/2), 2)/3+math.Pow(float64(y-height/2), 2)) / (height / 1.5) * 255
    			var gray uint8
    			if dist > 255 {
    				gray = 255
    			} else {
    				gray = uint8(dist)
    			}
    			im.SetGray(x, y, color.Gray{Y: 255 - gray})
    		}
    	}
    	pi := image.NewPaletted(im.Bounds(), []color.Color{
    		color.Gray{Y: 255},
    		color.Gray{Y: 160},
    		color.Gray{Y: 70},
    		color.Gray{Y: 35},
    		color.Gray{Y: 0},
    	})
    
    	draw.FloydSteinberg.Draw(pi, im.Bounds(), im, image.Point{})
    	shade := []string{" ", "░", "▒", "▓", "█"}
    	for i, p := range pi.Pix {
    		fmt.Print(shade[p])
    		if (i+1)%width == 0 {
    			fmt.Print("\n")
    		}
    	}
    }
    

Share Format Run
    
    
    var FloydSteinberg Drawer = floydSteinberg{}

FloydSteinberg is a Drawer that is the Src Op with Floyd-Steinberg error diffusion. 

####  type [Image](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=21) ¶

    
    
    type Image interface {
    	[image](/image).[Image](/image#Image)
    	Set(x, y [int](/builtin#int), c [color](/image/color).[Color](/image/color#Color))
    }

Image is an image.Image with a Set method to change a single pixel. 

####  type [Op](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=44) ¶

    
    
    type Op [int](/builtin#int)

Op is a Porter-Duff compositing operator. 
    
    
    const (
    	// Over specifies “(src in mask) over dst”.
    	Over Op = [iota](/builtin#iota)
    	// Src specifies “src in mask”.
    	Src
    )

####  func (Op) [Draw](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=55) ¶ added in go1.2

    
    
    func (op Op) Draw(dst Image, r [image](/image).[Rectangle](/image#Rectangle), src [image](/image).[Image](/image#Image), sp [image](/image).[Point](/image#Point))

Draw implements the Drawer interface by calling the Draw function with this Op. 

####  type [Quantizer](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=37) ¶ added in go1.2

    
    
    type Quantizer interface {
    	// Quantize appends up to cap(p) - len(p) colors to p and returns the
    	// updated palette suitable for converting m to a paletted image.
    	Quantize(p [color](/image/color).[Palette](/image/color#Palette), m [image](/image).[Image](/image#Image)) [color](/image/color).[Palette](/image/color#Palette)
    }

Quantizer produces a palette for an image. 

####  type [RGBA64Image](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go;l=30) ¶ added in go1.17

    
    
    type RGBA64Image interface {
    	[image](/image).[RGBA64Image](/image#RGBA64Image)
    	Set(x, y [int](/builtin#int), c [color](/image/color).[Color](/image/color#Color))
    	SetRGBA64(x, y [int](/builtin#int), c [color](/image/color).[RGBA64](/image/color#RGBA64))
    }

RGBA64Image extends both the Image and [image.RGBA64Image](/image#RGBA64Image) interfaces with a SetRGBA64 method to change a single pixel. SetRGBA64 is equivalent to calling Set, but it can avoid allocations from converting concrete color types to the [color.Color](/image/color#Color) interface type. 

##  ![](/static/shared/icon/insert_drive_file_gm_grey_24dp.svg) Source Files ¶

[View all Source files](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw)

  * [draw.go](https://cs.opensource.google/go/go/+/go1.24.5:src/image/draw/draw.go "draw.go")



Click to show internal directories. 

Click to hide internal directories.