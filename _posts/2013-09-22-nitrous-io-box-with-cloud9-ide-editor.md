---
layout: post
title:  "NITROUS.IO Box with Cloud9 IDE Editor"
date:   2013-09-22 22:42:00
categories: Work DotNet
---

![][1]  
[**Nitrous.IO**][2] is a wonderful way to develop software in the cloud and I'm a participant from the first minute. The platform is still in BETA and lacks with a good code editor.

![][3]  
[**Cloud9 IDE**][4] exists since 2010 and offers cloud development as well as the Cloud9 IDE itself as [open source][5] on GitHub.

I love the Nitrous.IO and the Cloud9 IDE so I thought it would be cool to combine them to a unbeatable beast. I presume you created an account on both platforms to follow this Guide:

1.  Create a new **NodeJS** Box on Nitrous.IO  
    ![nitro-step1][6]
2.  Note the information about the new box  
    ![nitro-step2][7]
3.  Add a new **SSH** Workspace on Cloud9  
    In my case the current version of node is v0.10.11 and is located in the Node Version Manager directory `/home/action/.nvm/v0.10.11/bin/node`.
    ![nitro-step3][8]
4.  Copy the SSH Key shown in the Cloud9 window
5.  Create a new file on the Nitrous.IO under `~/.ssh/authorized_keys` and paste the copied SSH Key as it is into the file. Save the file.  
    ![nitro-step4][9]
6.  You can now connect to the Nitrous.IO box via the Cloud9 IDE.

Enjoy C9 IDE code completion running on Nitrous.IO box (in this case a default [Meteor][10] project)  
![nitro-step5][11]

**Cheers!**

 [1]: /assets/nitrousio-logo.png
 [2]: https://www.nitrous.io/
 [3]: /assets/logo_cloud9.png
 [4]: https://c9.io/
 [5]: https://github.com/ajaxorg/cloud9
 [6]: /assets/nitro-step1.png
 [7]: /assets/nitro-step2.png
 [8]: /assets/nitro-step3.png
 [9]: /assets/nitro-step4.png
 [10]: http://www.meteor.com/
 [11]: /assets/nitro-step5.png