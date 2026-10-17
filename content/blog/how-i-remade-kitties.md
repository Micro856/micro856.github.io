+++
title = "How I remade Kitties"
description = "Learn how I restored Kitties after losing its original source code"
date = "2026-10-17"
updated = "2026-10-17"
draft = false

[taxonomies]
categories = ["Development"]
tags = ["Development","macOS","Swift","SwiftUI","Cats"]

[extra]
lang = "en"
toc = true
comment = false

+++
# Introduction to Kitties
Kitties is an app I made in Swift to learn about macOS app development. It is pretty simple, all it does is ask some APIs for a picture of a cat.

# Introduction to the problem
I started making Kitties during summer. I've finished the first release, even though I wasn't fully pleased with it. I sent that release to my friend to test it, and also include as a freebie with their app - [Google Balls Swift Port](https://github.com/weeniemount/googleballs-app/releases/download/1.9.0/GoogleBalls-swift.dmg). Straight away I started working on the 1.1 release of Kitties. I've asked my friends to make translations, I added another API to get another cat in the app, I also tried to implement image downloads. One day I wanted to move on to something diffrent, and come back to Kitties another day. I've deleted XCode off my mac, pushed Kitties to GitHub, and removed its source code off my mac. I pushed it to GitHub, should be alright, right? WELL NO! I didn't stash the commits, so what I commited is the Initial commit XCode makes when setting up a git repo for the project. Recently, the same friend, that got the first release of Kitties as first, tried Hackintoshing their main desktop. I've asked them "have you ran Kitties on it yet?" So, they ran it, and I've asked them "Why don't you run the newer version? I've no build of it, but the source code is there." They've downloaded the source code, open it in XCode, and what did they see? The hello world app XCode generates as the basic project. Original Kitties source code became lost media.

# What to do now?
Thankfully, I was doing a lot of screenshots during development, which I sent to my friends. From a few of them, I've managed to get MOST of Kitties 1.1 source code. I also had some screenshots of Kitties 1.0 code, so I could also glue them together with my memory into a remake of 1.0. But I met a problem, I didn't have Rory's API code entierly screenshoted.

![A screensot of Kitties 1.1 code](/blog/how-i-remade-kitties/KittiesCodeScreenshot1.png)

As you can see on the picture above, in ONE screenshot I had almost the entire codebase. I also had a screenrecording of the app after I implemented the API calls, in which the code for Gary and Goober API calls is visible. I would love to put it here, but it doesn't want to embed, so here's a screenshot of the exact moment in the video with the code:

![A screensot of Kitties 1.0 API calling code](/blog/how-i-remade-kitties/KittiesCodeScreenshot2.png)

Well, there's no Rory's code, what will I do? Well, that's the moment when this innovative feature of your brain comes to the rescue, it is called memories. I remember that Rory API calls were just a copy of Gary ones but of course the link changed. Well now this is done. Oh wait, these APIs return completly diffrent JSONs. Well this is a problem. How did I solve it? Let's take a look at both previous screenshots again. 

![XCode sidebar - Cropped first screenshot](/blog/how-i-remade-kitties/KittiesCodeScreenshot3.png)

Can you see this sidebar? It shows your code but tiny. Now you might ask me, how the hell did you read code from that. Well it's simple, I didn't. Let's look at the structure of the code there, and the API code from the 2nd picture. What can we deduce? We have 2 very similair blocks of code, that's the Gary and Rory API calls. Below we have the line "#Preview {
    ContentView()
}", then what appears the be a struct declaring the structure of the JSON, and again 2 similair blocks of code, that's the error codes. For some reason I made seperate error codes for Rory and Gary APIs, something I fixed in the 1.1-remake. Okay we know the structure, what does it solve? Well as I said, we can see Gary and Rory API calls are almost identical, so I could just copy the code for Gary API and change the URL. But wait in the 2nd screenshot we can see the struct have 2 values for JSON, and the sidebar appears to be showing only one. Now we can blame my laziness. Instead of figuring out how to convert between Rory's ID parameter and Gary's Number, I've decided to only use one parameter they shared, so the url, and decided to figure out it later. Only missing thing from code was the download button, but that was as easy as copying the Randomize button, check for the button styles that were on Kitties 1.1 screenshots on Apple Docs, and looking for download icon in the SF Symbols app, yes the button did originally just randomize, I have that engaved in my memory very well. 

![Original Kitties 1.1 screenshot](/screenshots/Kitties.png)

Only thing left were the translations, I had them lying around Discord just like the code screenshots, so it wasn't a problem.

# Kitties 2.0
Upcoming Kitties 2.0 release is more of what Kitties 1.1 was supposed to be if I would finish it originally. It has gotten a brand new icon, about it later. Part of 1.1 was also supposed to be image downloading, did I manage to implement it in the end? NOPE. It was the only moment when Apple Docs and online resources weren't helpful. I was managing to get the image to download to user's Downloads folder, but it was being saved as a .tmp file with a very temporary name, it was as simple as renaming it manualy to get the proper image, but I did not like that at all. So I scrapped downloading, well you still can also download them, as I provide you with the original URL in the app, which I was going to do no matter if downloading gets implemented, this URL showing is something I came up with for Kitties 2.0. One thing, you really should play around with the UI, even a bit aggressively.
## Desigining a new Icon
Now to the app's icon. I wanted to make it a bit better. Here's the first idea I had:
![Icon Idea 1 in App](/blog/how-i-remade-kitties/KittiesNewIconinApp.png)
![Icon Idea 1 in XCode](/blog/how-i-remade-kitties/KittiesNewIconinXCode.png)
I really like the idea, but it looked HORRIBLY on small scale, and on MacOS Tahoe (and so earlier macOS, because XCode will render a .icns for them based on how the icon displays on Tahoe) I think I might reuse the idea for when I make a Libadwaita port for Linux.

The final Kitties 2.0 icon was pretty simple. Let's go back to the cat's head and remake it. Also why not base it on one of my cats, instead of the Twemoji cat.
![Icon Idea 2 in Figma](/blog/how-i-remade-kitties/KittiesNewIconinFigma.png)
I'd say it looks way better. I fixed up the colors in Icon Composer, played A LOT with the background color. And the final icon for Kitties 2.0 looks like this:
![Icon Idea 2 in XCode](/blog/how-i-remade-kitties/KittiesFinalIconinXCode.png)
It's cute, I'd say. I also had an idea for the icon for macOS lower than Tahoe. Here's a sketch of it:
![Icon Idea 2 but for Big Sur - a sketch](/blog/how-i-remade-kitties/KittiesBigSurSketch.png)
And here's a trial of making it in Figma:
![Icon Idea 2 but for Big Sur - a a mockup in Figma](/blog/how-i-remade-kitties/KittiesBigSurFigma.png)
Well, you will rather not see it in Kitties 2.0, but meybe???

# Thank you!
Thank you for reading this blog post! I hope you will try out Kitties when 2.0 releases for macOS or when I will port it to Libadwaita.
