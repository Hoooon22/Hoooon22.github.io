---
layout: default
title: Cursor 에디터 사용 규칙
parent: STUDY
---

# Cursor 에디터 사용 규칙
{: .no_toc }

## 목차
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 마크다운 파일 이미지 삽입 규칙

GitHub Pages에서 마크다운 파일에 이미지를 삽입할 때는 다음 규칙을 준수해주세요.

### 1. HTML 태그 방식으로 이미지 삽입 (권장)

마크다운 형식(`![텍스트](경로)`) 대신 HTML 태그를 사용합니다:

```html
<img src="../../../../assets/images/카테고리/파일명.png" alt="이미지 설명">
```

**장점**:
- 이미지 표시 문제 최소화
- 스타일 및 크기 조정 가능
- 더 안정적인 렌더링

### 2. 이미지 파일명 가이드라인

- **간결하게 유지**: 파일명은 짧고 명확하게 지정
- **특수문자 회피**: 공백이나 특수문자 대신 하이픈(`-`)이나 언더스코어(`_`) 사용
- **의미있는 이름**: `screenshot-123.png` 대신 `dashboard.png`와 같이 내용을 설명하는 이름 사용

예시:
- ❌ `screencapture-devzip-site-traceboard-2025-04-14-00_55_02.png`
- ✅ `dashboard.png`

### 3. 이미지 경로 지정

상대 경로 사용 시 문서 위치에 따라 적절한 깊이 조정:

- `docs/projects/my-project/file.md` 문서에서 `assets/images/` 접근 시: `../../../../assets/images/`
- 경로가 복잡한 경우 절대 경로도 가능: `/assets/images/카테고리/파일명.png`

### 4. 이미지 설명 추가

이미지 바로 아래에 이탤릭체로 설명 추가:

```markdown
<img src="../../../../assets/images/카테고리/파일명.png" alt="이미지 설명">
*이미지에 대한 상세 설명을 여기에 작성합니다.*
```

## 문제 해결

이미지가 표시되지 않을 경우:

1. HTML 태그 방식으로 변경
2. 파일명 단순화
3. 이미지 파일 존재 확인
4. 경로 깊이 재확인

## 일반 마크다운 작성 규칙

1. **Front Matter** 항상 포함:
```
---
layout: default
title: 문서 제목
parent: 상위 카테고리
grand_parent: 최상위 카테고리
---
```

2. **목차 제외 태그** 추가:
```
# 문서 제목
{: .no_toc }

## 날짜
{: .no_toc .text-delta }
```

3. 코드 블록은 언어 지정하여 사용:
```markdown
```javascript
function example() {
  console.log("Hello World");
}
```
```

이 규칙들을 따르면 GitHub Pages에서 문서가 일관되게 표시되고 이미지 관련 문제를 최소화할 수 있습니다. 