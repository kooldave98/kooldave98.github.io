---
layout: post
title:  "Visual Studio 2015 - Task Runner"
date:   2015-08-08 19:55:37 +0100
categories: wts tech
---
This past week, I looked at exploring the features of the just released Visual Studio 2015, with a particular interest on the Task Runner feature that lets you use [npm](https://www.npmjs.com/) powered task automation engines like gulp/grunt to inject custom workflows into your *.NET* build. We have implemented a custom build task with *MSBuild*, but it isn't robust enough, and it is pretty much a re-invention of the wheel. Since Gulp has an ecosystem of re-useable task plugins that can simplify many common build tasks, why not embrace it to make our lives easier.

###Json content store

In our product, we implemented a simple homebrew content management sytem, we call it the `content-store`. It is how we isolate and dynamically manage non-user generated content from the application. The way my boss likes to think of content is: 'any thing in the application, that if I was Chinese, I would expect to be in Chinese'. This can be applied to images, icons etc, but we are only focused on textual content at this point in time.

<script src="https://gist.github.com/kooldave98/181f59e7e80b36a13953.js"></script>

We have many files like the above across our presentation layer, and the goal was to have, during development a convenient one resource file per feature, but at run-time one efficient compiled set of resource files, read once into memory.

###MSBuild
The first attempt was to use MSBuild to find all these json files and concatenate like this:

<script src="https://gist.github.com/kooldave98/e8501f5ea1599b9c7248.js"></script>

This worked sort of, but there were a few issues:

1. It concatenates- obviously not semantic merging.
2. Schema errors in the json file are not caught at compile time, but only at runtime.

The only way I could think of mitigating these was to hack out a weak solution using regex: `Out = Regex.Replace(In, "\r\n};{", ",");` see `MSBuild.xml` above, but then that is all that it was - a hack, with no real confidence on its reliability.

So I posted [a question on stack overflow](http://stackoverflow.com/q/28993751/502130), and then tweeted to Scott Hanselmann.

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/kooldave98">@kooldave98</a> like this? <a href="https://t.co/0h613UsMA9">https://t.co/0h613UsMA9</a> You need semantically appropriate merging, not just concatenating.</p>&mdash; Scott Hanselman (@shanselman) <a href="https://twitter.com/shanselman/status/575720492071440386">March 11, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I have been interested in augmenting our project build workflow with gulp since then.

####VS2015 Task Runner Explorer
We heard Visual Studio 2015 has these workflows built-in to the IDE, and Chris - my boss and I decided to give this *Gulp* thing a shot.

After setting up a new parallels VM with Windows 10 on my Macbook Pro, I installed VS2015, and SQLServer 2014 - the basic requirements for our source code to run locally; the total install time for everything (Windows 10, VS2015 and SQLServer 2014) clocked in at about 3hrs.

I created a `package.json` declaring my dependencies:

    {
      "version": "1.0.0",
      "name": "ASP.NET",
      "private": true,
      "devDependencies": {
        "gulp": "3.9.0",
        "gulp-extend": "0.2.0",
        "gulp-rimraf": "0.1.1"
      }
    }

followed by my gulp tasks in a `Gulpfile.js`:

    /// <binding BeforeBuild='merge-resource-jsons' />

    var gulp = require('gulp');
    var extend = require("gulp-extend");

    gulp.task('merge-resource-jsons', function (cb) {
        gulp.src('./Application/**/resource*.json')
            .pipe(extend('json-content-store-gulp-en.json'))
            .pipe(gulp.dest('./bin'));
    });

Just to be clear, this was all the code I had to write to achieve the same thing I was getting with the `MSBuild.xml` file above.

####Going forward
The results were impressive, but there were a few issues:

1. Duplicate json keys were not being caught, even though json schema errors were getting caught.
2. An error in the gulp task was not failing the build, but it gets displayed on the console - it's hard to miss, but you never know.

These 2 issues are sort of deal breakers for now, the goal of all of this was to allow for convenience whilst keeping the product performant and not to introduce product regression.

I really like the power of Gulp, and from looking online, it seems the possibilities for more complex workflows are endless.

Useful VS 2015 - resources

Gulp setup: http://blog.chrisbriggsy.com/Gulp-101-

Gulp build error:  http://blog.icanmakethiswork.io/2014/12/gulp-npm-long-paths-and-visual-studio-fight.html
