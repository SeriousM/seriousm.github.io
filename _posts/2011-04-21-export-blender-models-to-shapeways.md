---
layout: post
title:  "Export Blender Models to Shapeways"
date:   2011-04-06 13:02:00
categories: Work Blender3D
---

Here is the way how i get my model compatible for [ShapeWays](http://www.shapeways.com/).
Please check the FAQ and other pages on [ShapeWays](http://www.shapeways.com/) if you have questions that are not fit into this todo. here is the list: 

* create your 3d model
* convert all curves to meshes and apply all modifiers
* join all parts of the model together into a single mesh
* check that the model do not have any floating parts if you do not want them
* check the model for "non manifold" parts (edit mode - deselect all -> select -> non manifold) => [tutorial](http://www.shapeways.com/video/fixing-non-manifold-meshes)
*  * unwrap the model
*  * put the texture on the same directory level as the blend file
*  * set the texture to the model
* enable units under scene -> units in Blender
* set the dimensions of your model with the help of the units (eg. 12cm)
* IMPORTANT: apply the scale to the model (ctrl-a -> scale)
* export to collada (*.dae)
* open the exported model with [MeshLab](http://meshlab.sourceforge.net/) (free)
* save the model without any modifications as VRML (*.wrl) file
* pack the VRML file and the texture (same directory level!) into a zip file and upload it to [ShapeWays](http://www.shapeways.com/)
*  * -or- upload only the VRML file to [ShapeWays](http://www.shapeways.com/)
* check your email inbox for error / success messages

&#42; *= for colored print*

**i hope i could help!**