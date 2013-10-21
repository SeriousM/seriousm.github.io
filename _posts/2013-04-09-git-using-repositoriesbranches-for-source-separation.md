---
layout: post
title:  "Git: Using repositories/branches for source separation"
date:   2013-04-09 13:07:00
categories: Work DotNet
---

![Git Logo][1]

[Git][2] is a wonderful and easy way to manage your source code of any kind of project and using [GitHub][3] as the central is a smart move. Especially when you developing a web project it is always good to have a [staging site][4] where you can see the latest stage of the development in a production-like environment.

But what if your company wants you to separate the source code into development, staging and production stages? You can use branches even completely separated repositories to achieve that.

In my current project I've set up this branching system with a single repository:

*   master
*   protected/development
*   protected/staging
*   protected/production
*   [...] all other branches from my team

*Note: the prefix `protected/` is a valid prefix for branch names*

The workflow is:

*   everything that is in `master` will be pushed periodically to `protected/development`
*   as soon as changes in `protected/development` are detected, the development site will be deployed
*   every morning the latest source from `protected/development` will be pushed to `protected/staging` and the staging deployment site is started
*   once we are happy with the state of the staging site, we decide to manually start the deployment of the production site by pushing the source from `protected/staging` to `protected/production`
*   using the `protected/*` branches directly by the team members is not allowed

We are using [JetBrains Teamcity][5] to manage and execute these steps automatically. One of these steps is a shell script to synchronize the git branches.

[gist id=5344861 file=sync_repos_1branch.sh]

you can call this script as following: `./sync_repos.sh [path_to_work_in] [ssh/http-origin] [ssh/http-destination] [origin-branch] [destination-branch]`

example: `./sync_repos.sh ~/repos/dev git@github.com:user/project.git git@github.com:user/project.git protected/development protected/staging`

*Note: The `path_to_work_in` is necessary to create a bare repository as working base*

*Bonus:* [here is a script][6] that makes a backup of you whole repository including the tags.

Have fun setting up your own branching system!

 [1]: /assets/git_header.png
 [2]: http://git-scm.com/
 [3]: http://github.com/
 [4]: http://en.wikipedia.org/wiki/Staging_site
 [5]: http://www.jetbrains.com/teamcity/
 [6]: https://gist.github.com/SeriousM/5344861#file-sync_repos_full-bat