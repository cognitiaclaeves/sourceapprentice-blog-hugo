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
* TBD: Determines next blog to be announced
* Publishes to consumers
* Updates state for blog published
* Writes state to .directory.state-file or dynamo-db.*, according to config
* Pushes new state file