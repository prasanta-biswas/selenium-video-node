Additional Features
===================

# Video Node Arguments

    -Dvideo.framerate=<value>

Sets the framerate that we try to record video at - default value is "8" frames a second. At the moment we can only support up to about 10 frames a second (we spend a lot of time taking screenshots on the Java end). 

Selecting higher values seems to have no harmful side-effects (apart from not getting the requested framerate), while selecting lower values will consume less CPU resources.

# Hub Arguments

## Video Storage Arguments

The Hub supports an extensible plugin system to decide how to store the recorded videos.

    -Dvideo.storage=<classname>

Changes the backend implementation for how we store videos. This can be either a plugin provided by this project, or a user-supplied plugin on the classpath.

### com.mooo.aimmac23.hub.videostorage.LocalTempFileStore (default)

This implementation stores the videos as temporary files, and deletes them if too many accumulate. It also tends to forget about currently stored videos if the hub gets restarted.

There are currently no configurable options for this plugin.

### com.mooo.aimmac23.hub.videostorage.LocalFileVideoStore

Stores videos in a directory on disk. Videos persist over Hub restarts, and are never deleted. Note that clients can request any file in the configured directory, so be aware of where they are stored.

    -Dvideo.path=<path>
    
Uses the given directory to store the videos.

### com.mooo.aimmac23.hub.videostorage.BasicWebDAVStore

Uploads videos to a server which supports WebDAV. Following HTTP redirects when uploading is not supported.

    -Dwebdav.url=<url>
    
The URL can be either start with http:// or https://.

    -Dwebdav.username=<username>
    
Optionally provide a username to use when uploading the video.

    -Dwebdav.password=<password>
    
Optionally provide a password to use when uploading the video.