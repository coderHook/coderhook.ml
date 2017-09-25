+++
# Projects widget.
# This widget displays all projects from `content/project/`.

date = "2016-04-20T00:00:00"
draft = false

title = "Projects"
subtitle = "Here you can see most of the projects made by me. Javascript Front-End / Back-End projects and DataScience projects with Python and its libraries"
widget = "projects"

# Order that this section will appear in.
weight = 50

# View.
# Customize how projects are displayed.
# Legend: 0 = list, 1 = cards.
view = 1

# Filter toolbar.
# Add or remove as many filters (`[[filter]]` instances) as you like.
# Use "*" tag to show all projects or an existing tag prefixed with "." to filter by specific tag.
# To remove toolbar, delete/comment all instances of `[[filter]]` below.
[[filter]]
  name = "All"
  tag = "*"

  [[filter]]
    name = "Algorithms"
    tag = ".algo"

[[filter]]
  name = "React.js"
  tag = ".reactjs"

  [[filter]]
    name = "D3.js"
    tag = ".d3js"

  [[filter]]
    name = "Vue.JS"
    tag = ".vuejs"

    [[filter]]
      name = "Node.Js"
      tag = ".nodejs"

      [[filter]]
        name = "Others"
        tag = ".algo"

      [[filter]]
        name = "DataScience"
        tag = ".datascience"

+++
