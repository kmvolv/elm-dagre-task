---
# elm-dagre Task

## Difference b/w Render and Dagre Module
| Render | Dagre |
| ------ | ----- |
| Utilized to individually configure the dimensions of each node and edge of the graph which is specified through a dictionary. | Used to represent the nodes and edges entered by the user in Sugiyama Style with the help of the Dagre folder present in the repo. |

## Dagre Module Attributes
The following attributes are utilized for this project:
- `rankDir` - To specify the direction of representation of graph. User has four choices : top-to-bottom, bottom-to-top, left-to-right and right-to-left.

| bottom-to-top | top-to-bottom | left-to-right | right-to-left |
|---|---|---|---|
| <img src = "/imgs/rankdirBT.png" alt = "graph" width = "300" height = "300"> | <img src = "/imgs/rankdirTB.png" alt = "graph" width = "300" height = "300"> | <img src = "/imgs/rankdirLR.png" alt = "graph" width = "300" height = "300"> | <img src = "/imgs/rankdirRL.png" alt = "graph" width = "300" height = "300"> |



- `widthDict` - Configuration of node width of each node through a dictionary with key-value pair as node number and width respectively. 

| `DA.widthDict(Dict.fromList [( 1,20 ), ( 2,40 ), ( 3,60 ), ( 4,80 ), ( 5,100 )])`  | <img src = "/imgs/widthdict.png" alt = "widthdict" width = "300" height = "300"> |
| - | - |
- `heightDict` - Configuration of node height of each node, in a similar representation as the `widthDict` attribute. 

| `DA.heightDict(Dict.fromList [( 1,20 ), ( 2,40 ), ( 3,60 ), ( 4,80 ), ( 5,100 )])`  | <img src = "/imgs/heightdict.png" alt = "heightdict" width = "300" height = "300"> |
| - | - |
- `width` - Specification of default width of nodes, it is used when `widthDict` doesn't define a width for a node. 

| `DA.width 60`  | <img src = "/imgs/width.png" alt = "width" width = "300" height = "300"> |
| - | - |
- `height` - Similar to width, used when `heightDict` doesn't define a height for a particular node. 

| `DA.height 60`  | <img src = "/imgs/height.png" alt = "height" width = "300" height = "300"> |
| - | - |

## Render.draw
Render.draw takes in three parameters:
- `edits1` - A list of attributes specified in `Dagre.Attributes`. The individual attributes have been described about in the previous sub-heading.
- `edits2` - List containing the desired configurations for the nodes and edges. Styling and handling of _onClick_ events can be taken care of using this parameter. 
- `graph` - Definition of nodes and edges of graph using the elm-community/graph module.

Using these three parameters, the user is able to generate a graph with the liberty of applying their desired configuration, and using a default configuration otherwise.

## Conversion to Dagre Attributes
The attributes passed into the `Render.draw` is overwritten on the default configuration with the help of the following line :
``` dagreConfig = List.foldl (\f a -> f a) D.defaultConfig edits1```
#### Where `edits1` is the list of desired attributes entered by the user, and `D.defaultConfig` is the default configuration of attributes.
It doesn't matter if we overwrite the attributes from left to right or from right to left, so using `List.foldr` will also give the same result. 

## Passing of Layout Values to Drawers
Similar to how the Dagre attributes were obtained from the attributes entered in `Render.draw`, the layout values are configured as such :
``` drawConfig = List.foldl (\f a -> f a) defDrawConfig edits2 ```
#### Where `edits2` is the desired configuration of the nodes and edges by the user, which overwrites the default configuration in `defDrawConfig` 

## Drawer Specification and Standard Drawers
The drawer configuration is a combination of two entities - 
* `EdgeDrawerConfig` 
* `NodeDrawerConfig`

Both of these configurations have a set number of attributes, some in common, and some unique to only that particular entity. The attributes have been described about in the the next heading. 

__Standard Drawers__ is an encapsulation of attributes, types and configuration of the node and edge. It can be used by the user to modify the appearance of a particular entity in the node or edge. 

## StandardDrawer.attributes
- `label` - Used to set a custom label for nodes and edges

| <img src = "/imgs/labelnode.png" alt = "labelnode" width = "200" height = "200"> <img src = "/imgs/labeledge.png" alt = "labeledge" width = "250" height = "200">  | <img src = "/imgs/label.png" alt = "label" width = "300" height = "300"> |
| - | - |
- `onClick` - Adds an event listener to the element which when triggered, calls function specified by the user.  

| <img src = "/imgs/onclickcode.png" alt = "onclickcode" width = "250" height = "200">  | <img src = "/imgs/onclick.png" alt = "onclick" width = "300" height = "300"> |
| - | - |
- `strokeColor` - Modifies the stroke color of the desired node or edge. 

| <img src = "/imgs/strokecolorcode.png" alt = "strokecolorcode" width = "250" height = "200">  | <img src = "/imgs/strokecolor.png" alt = "strokecolor" width = "300" height = "300"> |
| - | - |
- `strokeWidth` - Modifies the stroke width of desired node or edge.

| <img src = "/imgs/strokewidthcode.png" alt = "strokewidthcode" width = "250" height = "200">  | <img src = "/imgs/strokewidth.png" alt = "strokewidth" width = "300" height = "300"> |
| - | - |
- `strokeDashArray` - To add a dashed boundary to node or to make edges dashed. 

| <img src = "/imgs/strokedasharraycode.png" alt = "strokedasharraycode" width = "250" height = "200">  | <img src = "/imgs/strokedasharray.png" alt = "strokedasharray" width = "300" height = "300"> |
| - | - | 
- `title` - Modify tooltip for a node or edge when hovered upon. 

| <img src = "/imgs/titlecode.png" alt = "titlecode" width = "250" height = "200">  | <img src = "/imgs/title.png" alt = "title" width = "300" height = "300"> |
| - | - |
#### Node-Specific Attributes:
- `shape` - Change the shape of node as __Circle, Ellipse, Box, or RoundedBox__

| Circle | Ellipse | Box | RoundedBox |
|---|---|---|---|
| <img src = "/imgs/circle.png" alt = "circle" width = "300" height = "300"> | <img src = "/imgs/ellipse.png" alt = "ellipse" width = "300" height = "300"> | <img src = "/imgs/box.png" alt = "box" width = "300" height = "300"> | <img src = "/imgs/rbox.png" alt = "rbox" width = "300" height = "300"> |
- `fill` - Add fill color to the node

| `RSDA.fill (\_ -> Color.lightOrange)`  | <img src = "/imgs/fill.png" alt = "fill" width = "300" height = "300"> |
| - | - |
- `xLabel` - To add an additional label for the node.

| `RSDA.xLabel (\_ -> "x")` | <img src = "/imgs/xlabel.png" alt = "xlabel" width = "300" height = "300"> |
| - | - |
- `xLabelPos` - Set the position of the label specified through `xlabel`

| `RSDA.xLabelPos (\_ _ _-> (10,20) )` | <img src = "/imgs/xlabelpos.png" alt = "xlabelpos" width = "300" height = "300"> |
| - | - |

#### Edge-Specific Attributes:
- `arrowHead` - Change the shape of arrow head pointing to node as __Triangle, Vee, or None__

| Triangle | Vee | None |
|---|---|---|
| <img src = "/imgs/triangle.png" alt = "triangle" width = "300" height = "300"> | <img src = "/imgs/vee.png" alt = "vee" width = "300" height = "300"> | <img src = "/imgs/none.png" alt = "none" width = "300" height = "300"> 
- `linkStyle` - Edges to be linked using either __Polyline or Spline__ (Curved line)

| Polyline | Spline |
| --- | --- |
| <img src = "/imgs/polyline.png" alt = "polyline" width = "300" height = "300"> | <img src = "/imgs/spline.png" alt = "spline" width = "300" height = "300"> |
- `alpha` - Used along with `linkStyle` as Spline to set the alpha value of the same.

| `RSDA.alpha 2.5` | <img src = "/imgs/alpha.png" alt = "alpha" width = "300" height = "300"> |
| - | - |
- `orientLabelAlongEdge` - A boolean to either align the edge label along its curvature or not.  

| `RSDA.orientLabelAlongEdge True` | <img src = "/imgs/align.png" alt = "align" width = "300" height = "300"> |
| - | - |

## Reason for separate Dagre and Draw Attributes
- A simple reason for this could be to make the code clean and easy to modify. 
- Had the attributes been defined in just a single attribute folder, there is a possibility of clashes with attributes such as `shape`.
- It is also much more organized this way, as the contents of the dagre attributes is kept seperate from the draw attributes.
