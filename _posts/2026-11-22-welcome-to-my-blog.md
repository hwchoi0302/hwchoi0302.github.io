---
title: "개인 홈페이지와 에세이 블로그를 시작하며"
date: 2026-11-22 21:00:00 +0900
description: "대학원 연구 기록과 에세이를 마크다운(.md)으로 정리하기 위한 첫 번째 샘플 글입니다."
tags: [essay, notes]
cover: assets/img/posts/welcome/cover.jpg
cover_caption: "상단 커버 이미지 예시 — front matter의 cover 항목에 이미지 경로만 적으면 자동으로 표시됩니다."
---

개인 홈페이지의 첫 번째 샘플 에세이입니다.
Medium처럼 상단에 와이드 커버 이미지를 두고, 본문에는 필요한 경우 **표(Table)**와 **이미지**를 자유롭게 추가할 수 있도록 구성했습니다.

## 1. 글 속에 이미지를 넣는 방법

새로운 에세이를 작성할 때는 해당 글 전용 이미지 폴더를 하나 만들어 두면 관리가 깔끔합니다.

1. `assets/img/posts/<글-슬러그>/` 폴더를 만들고 이미지를 넣습니다.
   - 예: `assets/img/posts/welcome/cover.jpg` (상단 배경 이미지)
   - 예: `assets/img/posts/welcome/sample-fig.jpg` (본문 이미지)
2. 본문에서는 표준 마크다운 문법 한 줄로 이미지를 삽입합니다:

```markdown
![본문 이미지 설명](/assets/img/posts/welcome/sample-fig.jpg)
```

실제 렌더링 결과는 아래와 같습니다:

![본문 이미지 예시](/assets/img/posts/welcome/sample-fig.jpg)

> 이미지를 클릭해 확대(Medium Zoom)하고 싶다면 `![설명](/assets/img/posts/welcome/sample-fig.jpg){: data-zoomable="true" }` 처럼 속성을 붙이거나 `figure.liquid`를 사용할 수 있습니다.

## 2. 표(Table) 작성 예시

일반 마크다운 표 문법을 그대로 사용하면 깔끔하게 스타일링됩니다.

| 항목 | 관리 파일 경로 | 비고 |
| :--- | :--- | :--- |
| **소개 (About)** | `_pages/about.md` | 프로필 사진: `assets/img/prof_pic.jpg` |
| **논문 (Publications)** | `_bibliography/papers.bib` | BibTeX 추가 시 자동 렌더링 |
| **이력서 (CV)** | `_data/cv.yml` + `assets/pdf/cv.pdf` | 웹 확인 + PDF 다운로드 |
| **에세이 (Blog)** | `_posts/YYYY-MM-DD-제목.md` | 푸시하면 자동 게시 + 댓글/좋아요 |

## 3. 댓글과 좋아요

각 블로그 글 하단에는 **Giscus (GitHub Discussions 기반)** 댓글과 이모지 리액션(좋아요) 영역이 자동으로 붙습니다.
사람 방문자는 물론, GitHub API/MCP를 사용하는 AI 에이전트도 해당 글의 Discussion에 댓글과 리액션을 남길 수 있습니다.
