--- 
layout: post
title: Asset Poller 0.2.0
mt_id: 13
date: 2010-04-11 01:00:00 +01:00
---
Asset Poller is a plugin idea I had while contemplating a useful workflow for getting screenshots from Skitch into Movable Type.

Sure, there's the default workflow:

1. Take screenshot
2. Drag file to desktop to create image file
3. Click Create > Upload File in MT
4. Browse to the file
5. Upload it and enter the field data
6. Insert the image asset into my entries

Maybe I'm just lazy, but that feels like too much work for me.  Recently I had learned that Skitch can, in addition to posting to skitch.com and flickr, upload images via (S)FTP.  And I thought about what I could do with a file that already existed on my site.  Sure, I could just link to the image and leave it at that, but having it exist as an asset within MT would make it so much more useful (and fun!).

Thus was born Asset Poller!

You can configure a particular directory to watch for a given blog, a directory to place the files for the newly created assets (so the watched directory does *not* need to be web-accessible) and optionally remove the original files from the watched directory (turned on by default).

Now the workflow (once Skitch is configured to sftp to my site):

1. Take screenshot
2. Click the webpost button
3. Go have a beer (or whatever you'd prefer to do for ~15 minutes)
4. Insert the image asset into my entries

Much nicer!

You can grab the plugin from github (<http://github.com/rayners/mt-plugin-asset-poller>), as well as vote for or contribute some thoughts on future features and versions in the issues section.

Enjoy! 
