---
layout: post
title:  "How to run ungit on Cloud9"
date:   2014-07-09 10:55:00
categories: Work
---
## Prerequisites
- An account on [Cloud9][cloud9] (supports GitHub accounts)
- A VM on [Cloud9][cloud9]
- node.js on the VM
- A git repository
- Watching the [intro video][ungit video] of [ungit][ungit]

## Installation
1. Open your terminal
2. Run `npm install -g ungit`
3. Run `ungit --urlBase http://$IP --port $PORT`
  - `$IP` is mapped to `0.0.0.0`
  - `$PORT` is mapped to `8080`
4. Open your browser and navigate to `https://<vm-name>-c9-<username>.c9.io/`
  - you can get the values from the ide-url which looks like `https://ide.c9.io/<username>/<vm-name>`
5. Enter the path to your repository, starting with `/home/ubuntu/`
6. Alternatively you can open the direct link `https://<vm-name>-c9-<username>.c9.io/#/repository?path=/home/ubuntu/<path>`
7. Have fun with [ungit][ungit]!
 - ungit have [a lot of options][ungit options] that might be handy, i.e. [gerrit][gerrit] support

## Known Issues
[Cloud9][cloud9] only have a single port that is exposed to the internet which is internally set to 8080. For some reason it's not possible to expose multiple services at once which means you have to stop any other web application before you can launch ungit.

  [ungit video]: http://youtu.be/hkBVAi3oKvo
  [ungit]: https://github.com/FredrikNoren/ungit
  [cloud9]: https://c9.io/
  [ungit options]: https://github.com/FredrikNoren/ungit/blob/master/source/config.js
  [gerrit]: https://code.google.com/p/gerrit/
