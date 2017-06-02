---
layout: post
title: My Challenges in Learning Software Development
---

As someone coming from a Network/Security/Data Warehouse background, learning software development as a beginner was relatively intimitating. There are many terminologies and concepts to understand and, facing a myriad of mainstream languages with different purposes in each one, I was worried a year's time would not be sufficient for me to even start as a junior developer in any company.

Maybe my age also adds to the worries. I will be 30 years old in three days with close to zero professional development experience. I don't know what that translates to in regards to today's competitiveness in the development industry. Am I too late to start? Or should I just stick with security, which I am not as passionate about as I was three years ago (perhaps I shouldn't have picked firewall administration to start my career).

So hopefully this is the right call. It has been about six months since I started my journey with Bloc. So far I can definitely say that my confidence has increased, but still doubtful if applying for a software development position, since I have only learned the front-end courses but not the back-end courses which seem to take about 80% of the entire track. 

### Git

The biggest challenges I've faced are the initial setup using Git and understanding some of the Bloc instructions. I've spent a lot of time just trying to find a console where I can start entering Git commands. After that, I spent a lot of time to understand how to commit a checkpoint or an assignment, and even more time understanding the terms like HEAD, fast-forward, feature, etc, because I'd run into a lot of Git errors. For example:

```
error: failed to push some refs to 'https://github.com/wongkx/bloc-jams-angular.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Some of the Git errors like this one are not as simple as Googling for an answer and quickly find a universal solution that is guaranteed to work, especially if multiple mistakes were made at the same time. I recalled this was when I started using Node.js/NPM, and it was not set up properly (missing dependencies, install in wrong directory, misconfiguration in JSON file, etc). I'd also unknowingly check in/out branch in different folders, such as /bloc-jams-angular/ vs. /bloc-jams-angular/app/. If I find a suggestion and apply it incorrectly, I might not be able to undo the Git command and revert to previous state, but open more worms instead.

### Angular.js

Angular.js was also difficult to learn. For each checkpoint, I was used to making changes in just 1-2 files, and could still use the Developer's tool and console.log to see my progress, one step at a time. However, in Angular.js MVC, multiple files might be involved. For examples, when creating a modal pop-up that accepts user inputs, I'd make changes to the home HTML that calls the modal, the modal HTML, the home controller, the modal controller, and the model that manages the data. 

So, debugging now becomes a challenge, since Angular.js errors are not very intuitive. For example, I see something like "Error: ng:areq Bad Argument…. Argument 'fn' is not a function, got string". Or, "[$injector:modulerr]". Without knowing which file, what line #, I don’t even know where to begin troubleshooting. And I can't just backtrack one step, to see at which point the issue occurs; I'd have to go all the way to the end due to the interdependency between the files.

