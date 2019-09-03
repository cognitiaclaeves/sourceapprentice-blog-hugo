+++
author = "cognitiaclaeves"
comments = false
date = "2019-09-03T17:07:00+00:00"
discussionId = ""
draft = true
lastmod = ""
summary = ""
tags = ["Blog Announcer", "BlogAnnouncer", "project"]
thread = "Blog Announcer"
title = "Project: Blog Announcer"

+++
* Uses git layer
* Receives JSON, containing:
  * "blog_repo": "git URL for blog repo"
  * "state_json": "state determined by StaticBlogStateUpdater, or user"
* Pulls down repo for blog
* Parses .directory.config yaml
  * , includes:
    * consumers
      * slack_status
        * sends status reports here
      * slack^n
      * twitter^n
* Determines next blog to be announced
  * Any blogs with future publish dates are ignored
  * If a blog has never been announced, then it takes priority
  * Blogs with fewer publish dates have priority over blogs with more publish dates
  * If it comes down to multiple blogs with the same number of publish dates, the first blog that has been published the earliest takes precedence
* Publishes to consumers (including slack-status)
* Updates state for blog published
* Updates state to .directory.state-file or dynamo-db.*, according to config
  * Note: Will need to create new state file while reading in state, updating for any slugs in the state JSON, and rename when done
* Push new state file into git repo