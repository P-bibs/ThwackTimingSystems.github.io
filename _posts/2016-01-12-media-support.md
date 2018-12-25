---
title: Media support
type: major
---

ChatApp introduces media support! Send images, videos and documents to your contacts.

**Features:**

* Image support
* Video support
* Document support

**Fixes:**

* Edge case contact syncing issue
* All memory leaks obliterated

ruby -r rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::Blogger.run({
      "source"                => "/Users/paulbiberstein/Desktop/blog-12-25-2018.xml",
      "no-blogger-info"       => false, # not to leave blogger-URL info (id and old URL) in the front matter
      "replace-internal-link" => false, # replace internal links using the post_url liquid tag.
    })'