# 개인 홈페이지 운영 매뉴얼 (MANUAL)

이 문서는 `https://hwchoi0302.github.io` 홈페이지를 직접 수정하고 관리하기 위한 가이드입니다.
(`_config.yml`의 `exclude`에 등록되어 있어 실제 홈페이지에는 노출되지 않고 저장소/로컬에서만 확인할 수 있습니다.)

---

## 0. 수정 후 반영 방법 (공통)

파일을 수정한 뒤 터미널에서 아래 3줄을 실행하면 GitHub Actions가 자동으로 빌드해 2~3분 안에 홈페이지에 반영합니다.

```bash
git add -A
git commit -m "update: 수정 내용 간단 요약"
git push
```

---

## 1. About 페이지 수정

- **본문 및 부제목 수정**: `_pages/about.md`
  - 상단 YAML 블록의 `subtitle`에서 소속·직함을 수정합니다.
  - `---` 아래 마크다운 본문에 본인 소개, 연구 관심사 등을 자유롭게 작성합니다.
- **프로필 사진 교체**:
  - `assets/img/prof_pic.jpg` 파일을 본인 사진으로 덮어쓰기하면 바로 바뀝니다.
  - 원형 프로필 사진을 원하면 `_pages/about.md`의 `image_circular: true`로 변경하세요.
- **이메일 / GitHub / Google Scholar 등 소셜 아이콘 수정**:
  - `_data/socials.yml`에서 원하는 항목을 추가하거나 주석(`#`)을 해제하면 됩니다.

---

## 2. Blog 에세이 올리기 (Medium 스타일)

1. `_drafts/essay-template.md` 파일을 복사해 `_posts/YYYY-MM-DD-영문슬러그.md` 이름으로 저장합니다.
   - 예: `_posts/2026-12-01-my-first-essay.md`
2. 상단 메타데이터(Front Matter)를 작성합니다:
   ```yaml
   ---
   title: "에세이 제목"
   date: 2026-12-01 10:00:00 +0900
   description: "목록과 제목 아래에 보일 한 줄 요약"
   tags: [essay, research]
   cover: assets/img/posts/my-first-essay/cover.jpg
   cover_caption: "상단 배경 이미지 캡션 (선택)"
   ---
   ```
   - 상단 커버 이미지가 필요 없으면 `cover:`와 `cover_caption:` 줄을 지우면 됩니다.
3. **글 속에 이미지 넣기**:
   - `assets/img/posts/<글-슬러그>/` 폴더에 이미지 파일을 넣습니다. (예: `assets/img/posts/my-first-essay/fig1.png`)
   - 마크다운 본문에 아래와 같이 작성합니다:
     ```markdown
     ![그림 설명](/assets/img/posts/my-first-essay/fig1.png){: data-zoomable="true" }
     ```
4. **표(Table) 넣기**:
   ```markdown
   | 항목 | 설명 | 비고 |
   | :--- | :---: | ---: |
   | A | 중앙 정렬 | 오른쪽 정렬 |
   ```
5. **저작권·인용 표기 및 댓글/좋아요**:
   - 모든 블로그 글 하단에 저작권 표시(`© Hyunwoo Choi`), APA/BibTeX 인용 박스, Giscus 댓글/좋아요 창이 **자동으로 추가**되므로 별도 작성할 필요가 없습니다.

---

## 3. Publications (논문) 추가

- 파일 위치: `_bibliography/papers.bib`
- 아래 양식대로 BibTeX 항목을 추가하면 **Publications** 페이지에 연도순으로 자동 정리됩니다.
- 본인 이름(`Choi, Hyunwoo`)은 자동으로 볼드/밑줄 강조됩니다.
- About 페이지 하단 **Publications** 섹션에도 함께 노출하려면 `selected = {true}`를 넣으세요.

```bibtex
@inproceedings{choi2026paper,
  abbr        = {CONF},
  bibtex_show = {true},
  title       = {Paper Title Here},
  author      = {Choi, Hyunwoo and Coauthor, Name},
  booktitle   = {Proceedings of Conference Name},
  year        = {2026},
  month       = {May},
  abstract    = {Paper abstract text here.},
  pdf         = {my_paper.pdf},          % assets/pdf/my_paper.pdf 에 넣거나 외부 URL 입력
  arxiv       = {2601.00000},            % arXiv ID (선택)
  code        = {https://github.com/...},% 코드 링크 (선택)
  selected    = {true}                   % About 페이지에도 표시하려면 true
}
```

---

## 4. CV (웹 + PDF) 수정

- **웹에 표시되는 CV 내용 수정**: `_data/cv.yml`
  - `Education`, `Research Experience`, `Publications`, `Awards & Honors`, `Skills` 항목을 YAML 형식에 맞춰 편집합니다.
- **PDF 파일 교체**:
  - `assets/pdf/cv.pdf` 파일을 본인의 최신 CV PDF로 덮어쓰기하면 CV 페이지 우측 상단 PDF 버튼과 소셜 아이콘에 바로 반영됩니다.

---

## 5. 색상 테마 및 부가 기능 설정

- **주간/야간 모드 색상 변경**: `_includes/head.liquid` 맨 아래 `<style>` 블록에서 색상을 바꿀 수 있습니다.
  - 주간 모드(`:root`): 딥톤 블루 (`#1b3a6b`)
  - 야간 모드(`html[data-theme="dark"]`): 쿨톤 레드 (`#e04868`)
- **댓글/좋아요(Giscus) 활성화**:
  1. GitHub 저장소 **Settings → General → Features → Discussions** 체크
  2. [giscus.app/ko](https://giscus.app/ko)에서 `hwchoi0302/hwchoi0302.github.io` 입력 후 발급된 `repo_id`, `category_id`를 `_config.yml`의 `giscus:` 아래에 입력
- **방문자 통계(GoatCounter) 활성화**:
  1. [goatcounter.com](https://www.goatcounter.com/)에서 무료 계정 생성
  2. 생성한 코드(예: `hwchoi0302`)를 `_config.yml`의 `analytics.goatcounter:`에 입력
