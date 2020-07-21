---
layout: default
title: 기술기준 및 판단기준
parent: Electricity
nav_order: 5
---

# 전기설비 기술기준 및 판단기준
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 전선로

### 경간

- **표준경간(판단기준 제76조, 제124조)**

|                                  |       | 경간                            | 경간                            |
|                                  | 고압   | 지름 5[mm] 이상                | 단면적 22[mm<sup>2</sup>] 이상 |
| 지지물의 종류                     | 특고압 | 단면적 22[mm<sup>2</sup>] 이상 | 단면적 55[mm<sup>2</sup>] 이상 |
|:---------------------------------|:------|:-------------------------------|:--------------------------------|
| 목주, A종 철주 또는 철근콘크리트주 |        | 150[m] 이하                   | 300[m] 이하                    |
| B종 철주 또는 철근콘크리트주       |       | 250[m] 이하                    | 500[m] 이하                    |
| 철탑                             |        | 600[m] 이하                   | 600[m] 이하                    |

- **보안공사(판단기준 제77조, 제125조)**  가공전선이 건조물, 도로, 횡단 보도교, 가공 약전선, 안테나, 다른 가공전선, 기타의 공작물과 접근 상태로 시설되거나 교차하여 시설하는 경우에 일반장소보다 강화하는 것을 보안공사라 한다.

`표준경간과 보안공사의 경우 경간`

| 지지물의 종류                     | 표준경간 | 저·고압보안공사 | 1종 특고 보안공사 | 2,3종 특고 보안공사 |
|:---------------------------------|:--------|:---------------|:-----------------|---------------|
| 목주, A종 철주 또는 철근콘크리트주 | 150     | 100             | 목주, A종 사용불가 | 100          |
| B종 철주 또는 철근콘크리트주       | 250     | 150            | 150                | 200          |
| 철탑                             | 600     | 400            | 400(단주 300)      | 400(단주 300) |








## Docker CentOS 8 설정

안녕하세요.  By default, Just the Docs uses a native system font stack for sans-serif fonts:

```scss
-apple-system, BlinkMacSystemFont, "helvetica neue", helvetica, roboto, noto, "segoe ui", arial, sans-serif
```

ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz
{: .fs-5 .ls-10 .code-example }

For monospace type, like code snippets or the `<pre>` element, Just the Docs uses a native system font stack for monospace fonts:

```scss
"SFMono-Regular", Menlo, Consolas, Monospace
```

ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz
{: .fs-5 .ls-10 .text-mono .code-example }

---

## 파이선 가상환경 설정

Just the Docs uses a responsive type scale that shifts depending on the viewport size.

| Selector              | Small screen size `font-size`    | Large screen size `font-size` |
|:----------------------|:---------------------------------|:------------------------------|
| `h1`, `.text-alpha`   | 32px                             | 36px                          |
| `h2`, `.text-beta`    | 18px                             | 24px                          |
| `h3`, `.text-gamma`   | 16px                             | 18px                          |
| `h4`, `.text-delta`   | 14px                             | 16px                          |
| `h5`, `.text-epsilon` | 16px                             | 18px                          |
| `h6`, `.text-zeta`    | 18px                             | 24px                          |
| `body`                | 14px                             | 16px                          |

---

## uWSGI 를 이용하여 Nginx 와 Flask 연결

Headings are rendered like this:

<div class="code-example">
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>
</div>
```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

---

## 개발환경 구성과 배포에 대해...

Default body text is rendered like this:

<div class="code-example" markdown="1">
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
</div>
```markdown
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```

---

## 도커를 이용한 서비스 배포(sparkc.tipsbdsys)

<div class="code-example" markdown="1">
Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](another-page).
</div>
```markdown
Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](another-page).
```

---

## Typographic Utilities

There are a number of specific typographic CSS classes that allow you to override default styling for font size, font weight, line height, and capitalization.

[View typography utilities]({{ site.baseurl }}{% link docs/utilities/utilities.md %}#typography){: .btn .btn-outline }
