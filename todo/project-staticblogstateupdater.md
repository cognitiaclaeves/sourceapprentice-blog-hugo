+++
author = "cognitiaclaeves"
comments = true
date = "2019-09-03T14:00:00+00:00"
discussionId = ""
draft = true
lastmod = ""
summary = "A project to track the state of social media announcements for a static blog."
tag = ["project", "StaticBlogStateUpdater", "Blog Announcer"]
tags = ["Blog Announcer", "project", "StaticBlogStateUpdater"]
thread = "Blog Announcer"
title = "Project: StaticBlogStateUpdater"

+++
* Uses git layer
* Receives JSON call
  * repo for static blog
    * .directory for StateUpdater
      * blog state file
        * json_lines format:
          * each line is a line of JSON
            * this incompatible format to anything known is meant to
              * prevent the resulting JSON call to BlogAnnouncer from growing without bounds,
              * and to cause the data to be processed in a manner similar to how it would be processed for dynamo_db (or other data source)
      * config file (YAML)
        * source: { type: json_lines, location: file_location }
        * source: { type: dynamo_db, location: table_name }
        * publish_timestamps: \[ list of timestamps \]
        * blog_paths: \[ list of paths (file masks for oswalk) \]
        * blog_announcer: URL for Blog Announcer Lambda
* Additional front-matter for blog entry:
  * publish_completed: {date}
  * publish_dates: \[ list \]
    * not completed until all publish_dates in config are processed
  * future_publish_startdate: {date}
    * blog will not be announced until this date
  * publish_slug: file_path
    * will be added to front-matter when entry is added to state file
* Program Flow:
  * Read state file
  * Iterate through lines
    * process_data(function) <- depends on config source.type
  * if !publish_completed, add to JSON response
  * build 2 dictionaries keyed to publish_slug
    * completed_publications
      * \[publish-slug\]: publish-completed: { published: date }
    * wip_publications
      * \[publish-slug\]: state JSON
  * Iterate through config blog-paths
    * capture any entries needing announcement into wip-publications
    * update if existing (state) doesn't match file contents (front matter)
      * (file contents should win?)
* Send JSON to BlogAnnouncer