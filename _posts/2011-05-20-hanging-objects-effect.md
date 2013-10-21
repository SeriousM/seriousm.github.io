---
layout: post
title:  "Hanging Objects Effect"
date:   2011-05-20 18:08:00
categories: Work Blender3D
---

![][1]
## Do you want to archive an effect like this? You found the solution.

_You can follow the full guide or skip the optional steps._

**1)** _Open a new Scene, delete the default Cube and add Suzanne (Monkey)._

![][2]

**2)** _Look through your Camera [NUM0] and rotate the Mesh as you want (tap [RKEY] twice for Trackball rotation)._
![][3]

**3)** _Apply the rotation with [CTRL]%2B[AKEY]. This is needed for the direction of the Threads._
![][4]

**4 opt)** _Add a Subdivision Surface Modifier (Level 2) to the Mesh and apply it because we need the additional Vertices count._
![][5]

**5 opt)** _Go into Edit Mode with [TAB], switch to Orthographic View with [NUM5] and to Top View with [NUM7]._
![][6]

**6 opt)** _Now select some random Vertices you can see from above (Top View) with the right mouse button and the [SHIFT] key._
![][7]

**7 opt)** _Switch to the Object Data in the properties panel, create a new Vertex Group with the plus sign and assign the selection to the Group. Leave the Edit Mode with [TAB]._
![][8]

**8)** _Now change to the Particles in the Properties Panel. Create a Particle System with the plus sign and change the type to Hair._
![][9]

**9)** _Tick the Advanced Options Check-box. Now set the amount to about 20 (depends on the selected Vertices), Emit from to Verts (Vertices) and set the velocity parameters (Normal to zero, Z to 1). If you rotate your Viewport now, you will see that the Hairs stands upwards now._
![][10]

**10 opt)** _Now scroll all the way down to Vertex Groups and expand the Panel. Chose the Group (selected Vertices) for Density. Now we have control where the Hairs are coming from._
![][11]

**11)** _Change to the Materials in the Properties Panel and create a new Material. You can leave the Settings as they are._
![][12]

**12)** _Change to the Textures in the Properties Panel and create a new Texture. You can chose the Texture Type Magic for an instant colorized result or chose an Image._
![][13]
![][14]
_ You can now render with [F12] and you will see a hanging Monkey face._

_The reason why this works is because the Hairs take over the color from the Material as long as the Material index is set to the Objects Material._

![][15]

**And that’s my render result:**

![][16]

Happy blending :D

   [1]: /assets/chadreau_small-200x300.jpg (chadreau_small)
   [2]: /assets/hanging_objects_step01.png (hanging_objects_step01)
   [3]: /assets/hanging_objects_step02.png (hanging_objects_step02)
   [4]: /assets/hanging_objects_step03.png (hanging_objects_step03)
   [5]: /assets/hanging_objects_step04.png (hanging_objects_step04)
   [6]: /assets/hanging_objects_step05.png (hanging_objects_step05)
   [7]: /assets/hanging_objects_step06.png (hanging_objects_step06)
   [8]: /assets/hanging_objects_step07.png (hanging_objects_step07)
   [9]: /assets/hanging_objects_step08.png (hanging_objects_step08)
   [10]: /assets/hanging_objects_step09.png (hanging_objects_step09)
   [11]: /assets/hanging_objects_step10.png (hanging_objects_step10)
   [12]: /assets/hanging_objects_step11.png (hanging_objects_step11)
   [13]: /assets/hanging_objects_step12.png (hanging_objects_step12)
   [14]: /assets/hanging_objects_step13.png (hanging_objects_step13)
   [15]: /assets/hanging_objects_step14.png (hanging_objects_step14)
   [16]: /assets/hanging-objects-300x168.jpg (hanging objects)
  