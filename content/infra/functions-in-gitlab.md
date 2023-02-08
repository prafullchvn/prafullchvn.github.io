---
title: 'Functions in Gitlab'
date: 2023-02-08T10:41:29+05:30
draft: true
---

## setup.yml

```yml
image: alpine
.setup:
  script:
    - echo "in setup action"
    - echo "ending setup action"
.teardown:
  script:
    - echo "in teardown action"
    - echo "ending teardown action"
```

## use of it `setup.yml`

```yml
include:
  - setup.yml
test:
  script:
    - echo "before running setup
    - !reference [.setup, script]
    - !reference [.teardown, script]
```
