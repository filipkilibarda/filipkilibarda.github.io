---
layout: default
title: Hacking Youtube's UI to gain HYPER SPEED
subtitle: Boredom leads me to discover a hidden gem amongst Youtube's UI source code
---

I recently started watching videos on 2x playback speed and I've found it to be a huge time saver. It's interesting how one's brain can accept & comprehend speech at speeds much faster than anyone can speak.
 
On Youtube the maximum allowed speed is 2x, which is actually **too slow** in my opinion, surprisingly. I was aware that there were plugins that could make HTML5 Video go arbitrarily fast, but I figured I'd kill some time and take a break from learning dynamic programming. So I decided to try and patch Youtube's UI code to accommodate faster speeds.
 
I had to find the section of code that set the playback speed, but amongst Youtube's massive, obfuscated UI code base, this was not an easy task.
 
Fist, I tried navigating event listeners on the DOM button listeners:
 
![](/assets/images/youtubehack/1.png)
 
The "Event listeners" tab in the devtools UI showed that "click" had a listener.
 
![](/assets/images/youtubehack/2.png)
 
Found the handler for the settings button, but with all those obfuscated names, it didn't seem like a great place to start. So that was a dead end.
 
This was proving to be tricky so I reverted to just `Ctrl+F`ing for key terms like "speed", "playback", "rate".
 
![](/assets/images/youtubehack/11.png)
 
Hmm what the heck. `enable_faster_speeds`?? How fast can I go?!?
 
![](/assets/images/youtubehack/9.png)
 
Well looked like `enable_faster_speeds` wasn't a defined attribute on the `a` object. Strange. So I defined it to `true`, and the result:
 
<!-- ![](/assets/images/youtubehack/10.png) -->
![](/assets/images/youtubehack/demo.gif)
 
Alright so Youtube's UI javascript just has this hidden `enable_faster_speeds` attribute, which is normally `undefined`, but if set to `true`, you get 15x speed hahaha. So strange. This attribute doesn't seem to be documented anywhere. Passing `enable_faster_speeds=true` as a URL parameter doesn't work either. Maybe it's just an old artifact?

...And now I must learn how to do dynamic programming so I can get a job.