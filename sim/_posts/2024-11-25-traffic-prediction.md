---
layout: post
title: AIMM 시뮬레이터 개선 - Phase 1
description: >
  **Date**: 2024.11.25, 
  **Tag**: [Traffic Prediction], [Carbon Emission], [Graduation]
image: 
  path: /assets/img/blog/green_ai/green-ai.png 
  srcset: 
    1920w: /assets/img/blog/green_ai/green-ai.png
    960w:  /assets/img/blog/green_ai/green-ai@0,5x.png
    480w:  /assets/img/blog/green_ai/green-ai@0,25x.png
# accent_image: /assets/img/blog/pawel-czerwinski-848z7lbCjoo-unsplash.jpg
excerpt_separator: <!--more-->
sitemap: false
---

<!--more-->

* toc
{:toc .large-only}


### 디렉토리 구조

```
timeseries-predictor/
├── src/
│   └── main.py (아직 작성 안 됨)
├── kubernetes/
│   ├── configmap.yaml      (완료)
│   ├── secret.yaml         (완료)
│   ├── deployment.yaml     (완료)
│   ├── cronjob.yaml        (완료)
│   └── pvc.yaml           (추가 필요)
├── Dockerfile              (완료)
└── requirements.txt        (완료)
```

### 1. PostgreSQL 비밀번호 

```
export POSTGRES_PASSWORD=$(kubectl get secret --namespace database postgresql -o jsonpath="{.data.postgres-password}" | base64 -d)

echo $POSTGRES_PASSWORD
```
