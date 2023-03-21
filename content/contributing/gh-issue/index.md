---
title: "Creating a GitHub Issue"
date: 2022-03-08T11:15:22-06:00
weight: 2
draft: false
---

## What are GitHub Issues

GitHub Issues is a powerful feature built into GitHub that allows individuals to **raise issues** directly inside the source code of a project. These issues are monitored by the maintainers of the project and the maintainers use the information inside of an individual issue to improve the overall project.

GitHub issues often include:

1. bugs
1. feature requests
1. found vulnerabilities
1. package updating requests
1. optimization requests

The maintainers of the project can use these GitHub issues to crowd source bug fixes, and plan additional work to be added to the project that are reported directly from the users.

Project maintainers have no obligation to include any suggested features, to patch any bugs or vulnerabilities, but do often use the issues to best determine what work needs to happen on any given project.

### GitHub Issues Example: `nodejs/node`

Let's take a look at the GitHub repo for the [NodeJS Project](https://github.com/nodejs/node).

![node-js-homepage](pictures/node-js-homepage.png?classes=border)

This is the standard homepage for any GitHub repository. It contains information around:

1. name of organization: "nodejs"
1. name of repo: "node"
1. repo visibility: Public
1. repo watchers (2.9k), forks (23k), and stars (86.3k)
1. the current branch: `master`
1. a listing of all of the directories and files in the project

You should notice a list of tabs that can be selected for more information:

1. The currently selected, default tab: Code
1. Issues
1. Pull requests
1. Discussions
1. Actions
1. Projects
1. Security
1. Insights

Let's click the *Issues* tab and see the currently open issues of this repo:

![node-js-issues](pictures/node-js-issues.png?classes=border)

At the time of this photo there are 1320 *open* & 12987 *closed* issues. As you may have guessed `node` is a tremendously popular and widely used tool. In the `nodejs/node` repository, users constantly report bugs and vulnerabilities and propose possible optimizations and new features.

Two of the three issues we can see are clearly marked with a `feature request` label. Both of these issues are requests made by node users for additional features they would like to see incorporated into the project.

## LaunchCode Curriculum GitHub Issues

At LaunchCode we store all of our curriculum in GitHub repositories. Our curriculum is going through constant changes and as you work through the curriculum you may find bugs, vulnerabilities, compatibility mismatches, or you may have ideas for features that can be added.

Creating a new GitHub Issue can be a daunting task. For this reason we have pre-configured three different GitHub Issue Templates to help you in providing us with the information we need to continue improving the curriculum.

Available LaunchCode Provided Issue Templates:

1. Bug
1. Clarity Request
1. Feature Request

{{% notice blue "Note" "rocket" %}}
Outside of the three available templates, you can also open a new blank to bring our attention to an issue.
{{% /notice %}}

## Creating a New LaunchCode GitHub Issue

### Bug

A bug issue is your way to inform us about a bug in the curriculum.

Common bugs include:
 
1. a copy/edit error (misspelling, grammar mistake)
1. broken links
1. missing images
1. un-executable code in code-fences
1. buggy features (like the search, or the menu)

As you are working through the curriculum you may encounter any of the above bugs, or ones not mentioned in the list. In the case of encountering the bug we encourage you to create a new issue by using the Bug Issue Template.

#### Example

Let's take a look at the Bug Form.

![bug-form-blank](pictures/bug-form-blank.png?classes=border)

You must provide us with:

1. Title of the issue, such as "Typo on Why Learn to Code"
1. The URL where the bug exists, such as `https://education.launchcode.org/intro-to-professional-web-dev/chapters/introduction/why-learn-to-code.html`
1. The nature of the bug
  - What bug did you encounter? 
    - How was it supposed to behave? (expected behavior)
    - How did it actually behave? (actual behavior)
  - For example: "I clicked on the Learn More link, but the resource could not be found with a 404 status code."

Additionally, we ask that you provide any more information around the context of this bug. To adequately fix the bug we have to first recreate the bug on our system. This verifies the existence of the bug and gives us insight into identifying the underlying problem that is causing the bug. These steps have to be completed in order to fix the bug.

### Clarity Request

Confusion is a natural part of the learning journey. We try to create and organize content in a way that reduces confusion for as many different learning styles as possible.

There may be instances where a large number of students and course staff will encounter confusion around the same section of curriculum. When this happens it's a good indicator that a section should be reworded, reorganized, or rebuilt in a way to reduce the confusion experienced by a large number of individuals.

The Clarity Request Form is the mechanism that allows students and course staff to provide feedback around clarity improvements that can be made to the curriculum.

{{% notice blue "Note" "rocket" %}}
Please talk to other students and course staff about your confusion before creating a new clarity request. They may be able to help you better understand the material before you make a clarity request. If they agree it is confusing and your class is struggling to move forward, please contact your Candidate Engagement Manager. The Education team may be able to intervene and assist your class to prevent the confusion from impeding your class's progress. If it is not impeding the progress of the class, please make a clarity request.
{{% /notice %}}

#### Example

Let's take a look at the Clarity Request Form:

![clarity-request-form-blank](pictures/clarity-request-form-blank.png?classes=border)

You must provide us with:

1. Title of the issue
1. The URL to the issue
1. Confusing section

Additionally we ask that you provide:

1. Any suggestions you may have for improving the clarity.
1. Additional information to help us understand the nature of your confusion, or the underlying issue.

### Feature Request

In some instances you may have ideas about new features to the website hosting the curriculum, or new content that might have a positive impact on the experience of students and course staff working through a LaunchCode program.

Features of the website include:

1. text search
1. buttons
1. navigation bars
1. menus
  1. table of contents
1. next and previous buttons

Content may include:

1. more code examples
1. more exercises
1. more concept checks
1. additional sections to chapters
1. additional chapters
1. additional explanations
1. additional definitions
1. additional diagrams

There are many things that could be added to the website or to the content of the curriculum. Reaching a consensus amongst course staff and students as to what should be added will increase the likelihood that LaunchCode Education approves the feature request as we are dedicated to serving our students and course staff and providing the best education possible.

#### Example

Let's take a look at the Feature Request Form:

![feature-request-form-blank](pictures/feature-request-form-blank.png?classes=border)

You must provide us with a title and a short description of the feature you would like. The description is required. We cannot add new features or content if we do not have a description.

Additionally we ask you to provide an additional longer description of the feature and suggestions on where/how the feature or content should be added.

Providing as many details as possible about the new feature or content is necessary for LaunchCode to determine if the feature/content is feasible, and if/when it should be developed. This makes the longer description of the feature section an important part of the form.

Providing suggestions on where the feature should be added is also important for LaunchCode to determine where and how the feature or content should be implemented.

## Review

GitHub Issues are a way for the users of a project to communicate directly with developers or maintainers of a project about improvements that can be made to a project.

LaunchCode encourages students, course staff, and allies of LaunchCode to create issues when encountering bugs, requesting new features, or requesting clarity reviews. We encourage you to utilize the templates when doing so.

## Closing Remarks

All issues will be considered by a LaunchCode representative. However, making an issue does not guarantee that the encountered bug, clarity request, feature request or any other issue will be incorporated into the curriculum.

Any issues may be closed without discussion or reason by a LaunchCode representative.

LaunchCode reserves the final say in all things related to the curriculum.

We appreciate any and all feedback gathered through GitHub Issues and we thank you for your work towards creating better experiences for future students!