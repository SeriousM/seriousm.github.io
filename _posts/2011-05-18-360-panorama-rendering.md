---
layout: post
title:  "360° Panorama Rendering"
date:   2011-05-18 12:40:00
categories: Work Blender3D
---

I was searching for a way to create a panorama shot but just found some wired information’s about PartX properties.
Then i came to a [post](http://blenderartists.org/forum/showthread.php?205466-Blender-2.5-Panorama-render) where it was described how it works with blender 2.5.

But now i have more accurate settings for a better render this way.

The setup is now fairly easy:

* place the camera with horizontal alignment between the objects
* set the focal length to 5.050mm
* enable the panorama option

[![Screenshot-2011-08-20_08-17-21](/assets/Screenshot-2011-08-20_08.17.21.png)](/assets/Screenshot-2011-08-20_08.17.21.png)

Next we have to setup the render options:

* In the performance tab extend the Tiles X and Y to 360 and 180.
  (This will increase the render time but reduces the count of artifacts)

[![Screenshot-2011-08-20_08-11-14](/assets/Screenshot-2011-08-20_08.11.14.png)](/assets/Screenshot-2011-08-20_08.11.14.png)

With these settings, you get a result like this:

[![paonrama_render_result](/assets/panorama_render_result.jpg)](/assets/panorama_render_result.jpg)

Happy blending :)