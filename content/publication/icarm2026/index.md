---
title: 'Learning Robust Quadrupedal and Bipedal Locomotion on a Quadruped Robot using One Policy'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - me
  - Shengcong Sang
  - Yan Huang

# Author notes (optional)
# author_notes:
#   - 'Equal contribution'
#   - 'Equal contribution'

date: '2026-07-28T00:00:00Z'
# doi: '10.1109/ICARM62033.2024.10715938'

# Schedule page publish date (NOT publication's date).
publishDate: '2026-07-28T00:00:00Z'

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ['conference']

# Publication name and optional abbreviated publication name.
publication: In *2026 International Conference on Advanced Robotics and Mechatronics (ICARM)*
publication_short: In *ICARM 2026* **(Best Conference Paper Finalist)**

abstract: Locomotion is an essential ability for legged robots to be applied in various conditions. The ability to perform quadrupedal and bipedal locomotion on one robot can bring excellent versatility for legged robots. However, few works have studied learning both quadrupedal and bipedal locomotion using one policy. Using different policies for different locomotion requires switching between polices. The switching process may introduce undesired behaviors during the transition because of distribution shift. In this work, we propose a framework for a quadruped robot to learn quadrupedal and bipedal locomotion in a unified policy via reinforcement learning (RL). Through task-dependent reward designs based on binary task indicators, a policy can learn both kinds of locomotion even they are mutually conflicting. Results show that the quadruped robot can perform robust bipedal and quadrupedal locomotion on complex terrains. Besides, the robot can perform smooth transition within 1 second between two kinds of locomotion even during motion at speeds as high as 1.5 m/s. Our framework outperforms previous methods in terms of training efficiency and still demonstrates comparable terrain traversal performance on stairs and slopes.

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
  - Reinforcement Learning
  - Bipedal Robot
  - Quadrupedal Robot

# Display this page in the Featured widget?
featured: false

# Custom links (uncomment lines below)
links:
- type: pdf
  url: 'uploads/20261010_ICARM.pdf'
# url_code: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_dataset: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: 'https://github.com/HugoBlox/hugo-blox-builder'
# url_video: 'https://youtube.com'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: ''
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: [Learning Robust Quadrupedal and Bipedal Locomotion on a Quadruped Robot using One Policy]

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---
