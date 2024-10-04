---
layout: project
title: 'Hydejack Site'
caption: Dogfooding Hydejack to sell Hydejack.
description: >
  While Hydejack is built for personal sites, it's versatility allows it to be used a product page as well.
date: '01-01-2016'
image: 
  path: /assets/img/projects/hydejack-site.jpg
  srcset: 
    1920w: /assets/img/projects/hydejack-site.jpg
    960w:  /assets/img/projects/hydejack-site@0,5x.jpg
    480w:  /assets/img/projects/hydejack-site@0,25x.jpg
links:
  - title: Link
    url: https://hydejack.com/
sitemap: false
---

# O-RAN AIMLFW

## Introduction


## Installation

1. 설치 스크립트 실행
   
```
bin/install_traininghost.sh
```

![Fig 1](/assets/img/projects/aimlfw/installation_1.png)


2. 10 - 20분 정도 기다린 후 파드가 잘 설치되어 있는지 확인
   
```
kubectl get pod -A
```

![Fig 2](/assets/img/projects/aimlfw/installation_2.png)