---
layout: post
title:  "I just did it"
date:   2014-06-30 14:51:00
categories: Work
---
**Usually I'm very keen to prepare myself for a project**
I create a project document in my Google Docs with a well thought name, a few lines of introduction and the description about the technical stack like language(s), hosting and package I plan to use. Then I create a GitHub repository and start coding, at least that what I aim for; but instead I get distracted by all the details I was thinking of in the first place and read/try them out instead doing what I should focus on.

**But this time it was different**
I didn't created a project document, I didn't evaluated the pros and cons about every single package and I didn't used a source control at all.
I just opened the terminal and my text editor of my choice and started coding. Yes I did mistakes and yes one or two times I would like to have a source control to recover my mistakes, but I knew that committing source in this early stage would block my creativity because every step would have to feel like a "feature".

Now, after I finished my [MVP][mvp] I committed my source code and can start thinking in features I like to add. I guess only you have at least "something" ([MVP][mvp]) you can start enhancing it instead doing premature optimizations to "nothing".

Here is my [MVP][mvp] called [yournal][yournal] ([GitHub][yournal-github]), a personal journal without all the unnecessary wrinkles others have.
I still have some plans to enhance it a bit but in the end that's what it should be.

**Meteor**
[Meteor.js][meteor] was a great help realizing my idea. It helps me focusing on the application instead on the framework. This might sounds wrong because meteor *is* a framework but once you setup the routing the only thing you have to code is html (template) and javascript (event handling).

**TL;DR;**
Don't prematurely optimize your ideas, build at least a [MVP][mvp] to see if it works out as expected.

  [mvp]: http://en.wikipedia.org/wiki/Minimum_viable_product
  [meteor]: https://www.meteor.com/
  [yournal]: https://yournal.meteor.com/
  [yournal-github]: https://github.com/SeriousM/yournal
