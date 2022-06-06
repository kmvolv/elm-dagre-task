---
# elm-dagre Task

## Difference b/w Render and Dagre Module
| Render | Dagre |
| ------ | ----- |
| Utilized to individually configure the dimensions of each node and edge of the graph which is specified through a dictionary. | Used to represent the nodes and edges entered by the user in Sugiyama Style with the help of the Dagre folder present in the repo. |

## Dagre Module Attributes
The following attributes are utilized for this project:
- `rankDir` - To specify the direction of representation of graph. User has four choices : top-to-bottom, bottom-to-top, left-to-right and right-to-left.
- `widthDict` - Configuration of node width of each node through a dictionary with key-value pair as node number and width respectively. 
- `heightDict` - Configuration of node height of each node, in a similar representation as the `widthDict` attribute. 
- `width` - Specification of default width of nodes, it is used when `widthDict` doesn't define a width for a node. 
- `height` - Similar to width, used when `heightDict` doesn't define a height for a particular node. 

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
## StandardDrawer.attributes
- `label` - Used to set a custom label for nodes and edges
- `onClick` - Adds an event listener to the element which when triggered, calls function specified by the user.  
- `strokeColor` - Modifies the stroke color of the desired node or edge. 
- `strokeWidth` - Modifies the stroke width of desired node or edge.
- `strokeDashArray` - To add a dashed boundary to node or to make edges dashed. 
- `style` - Adds inline css to a node/edge. 
- `title` - Modify tooltip for a node or edge when hovered upon. 
#### Node-Specific Attributes:
- `shape` - Change the shape of node as __Circle, Ellipse, Box, or RoundedBox__
- `fill` - Add fill color to the node
- `xLabel` - To add an additional label for the node.
- `xLabelPos` - Set the position of the label specified through `xlabel`

#### Edge-Specific Attributes:
- `arrowHead` - Change the shape of arrow head pointing to node as __Triangle, Vee, or None__
- `linkStyle` - Edges to be linked using either __Polyline or Spline__ (Curved line)
- `alpha` - Used along with `linkStyle` as Spline to set the alpha value of the same.
- `orientLabelAlongEdge` - A boolean to either align the edge label along its curvature or not.  

## Reason for separate Dagre and Draw Attributes
- A simple reason for this could be to make the code clean and easy to modify. 
- Had the attributes been defined in just a single attribute folder, there is a possibility of clashes with attributes such as `shape`.
- It is also much more organized this way, as the contents of the dagre attributes is kept seperate from the draw attributes.
