---
title: "Pretty Printing JSON with Ruby"
description: "Another simple way to pretty print JSON"
date: 2018-07-05T19:16:27-05:00
draft: false
tags: 
  - ruby
  - json
comments: false
slug: ""
showpagemeta: false
showcomments: false
enableToc: false
---

Ruby can be used to pretty-print JSON files, by invoking the `JSON` module from the Ruby standard library. It can turn "ugly" JSON:

```shell
➜  roles cat web.json
{"name": "web","description": "Web server role.","json_class": "Chef::Role","default_attributes": {"chef_client": {"interval": 300,"splay": 60}},"override_attributes": {},"chef_type": "role","run_list": ["recipe[chef-client::default]","recipe[chef-client::delete_validation]","recipe[learn_chef_apache2::default]"],"env_run_lists": {}}
```

into pretty-printed JSON:

```shell
➜  roles ruby -rjson -e 'puts JSON.pretty_generate(JSON.parse(ARGF.read))' web.json
{
  "name": "web",
  "description": "Web server role.",
  "json_class": "Chef::Role",
  "default_attributes": {
    "chef_client": {
      "interval": 300,
      "splay": 60
    }
  },
  "override_attributes": {
  },
  "chef_type": "role",
  "run_list": [
    "recipe[chef-client::default]",
    "recipe[chef-client::delete_validation]",
    "recipe[learn_chef_apache2::default]"
  ],
  "env_run_lists": {
  }
}
```