---
layout: post
title:  "Modular Redux"
published: false
---
## Modular structure
There is no idiomatic way to write/structure redux apps today, and unsurprisingly, as a consequence of this, a plethora of paradigms have emerged.

One that stands out for me personally is the ducks/re-ducks proposal.
Duck proposal: 
    https://github.com/alexnm/re-ducks

....

However, the main thing to bear in mind though is that the structure is driven by the state which is in turn driven by the presentation.

    Presentation [drives -> ] State [drives -> ] Folder structure.

This way it is easy to conceptualise where things are as there is no dissonance between folder, state and presentation.

Another important point is that modules cannot have knowledge of its parent (or anything above it) nor sibling modules, but can reach into child submodules however far down the stream. However, all access to modules MUST go through the module interface defined in the index.js file. Bypassing the module interface is possible, but strongly discouraged. 

This will encourage loose coupling and save you a lot of pain in the future. Additionally, you can be confident that you will gracefully skirt away from the circular dependency problem.

It is important to note that the ideas in these links are not mandatory, and developer discretion is still needed.




In-depth: 
    https://jaysoo.ca/2016/02/28/organizing-redux-application/
    http://blog.sapegin.me/all/react-structure
