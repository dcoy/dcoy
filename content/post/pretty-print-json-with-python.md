---
title: "Pretty Printing JSON with Python"
description: "A simple way to pretty print JSON"
date: 2018-07-05T19:16:27-05:00
draft: false
tags: 
  - python
  - json
comments: false
slug: ""
showpagemeta: false
showcomments: false
enableToc: false
---

# Pretty Printing JSON with Python

Python can be used to pretty-print JSON files locally, by invoking the `json.tool` module. It can turn "ugly" JSON

{{< highlight bash >}}
➜  roles cat web.json
{"name": "web","description": "Web server role.","json_class": "Chef::Role","default_attributes": {"chef_client": {"interval": 300,"splay": 60}},"override_attributes": {},"chef_type": "role","run_list": ["recipe[chef-client::default]","recipe[chef-client::delete_validation]","recipe[learn_chef_apache2::default]"],"env_run_lists": {}}
{{< /highlight >}}

into pretty-printed JSON:

{{< highlight bash >}}
➜  roles python -m json.tool web.json
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
    "override_attributes": {},
    "chef_type": "role",
    "run_list": [
        "recipe[chef-client::default]",
        "recipe[chef-client::delete_validation]",
        "recipe[learn_chef_apache2::default]"
    ],
    "env_run_lists": {}
}
{{< /highlight >}}