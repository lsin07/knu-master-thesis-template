# 경북대학교 석사학위논문 LaTeX 템플릿

[English README](README.md)

> **주의:** 이 템플릿은 경북대학교 또는 전자전기공학부에서 배포하는 공식 템플릿이 아닙니다. 항상 학교 및 소속 학부·학과에서 공식 배포하는 학위논문 양식과 제출 지침을 우선하여 따르세요. 이 템플릿의 내용이 공식 양식이나 지침과 다를 경우, 공식 양식과 지침을 적용해야 합니다.

> **용지 규격 주의:** 이 템플릿의 PDF는 일반적인 **A4(210 × 297mm)가 아닌 사륙배판(190 × 260mm)**으로 생성됩니다. 용지 크기는 `thesis.sty`의 `geometry` 설정에 지정되어 있습니다. 인쇄·제본 시 이 규격을 확인하고, 원래 크기를 유지하려면 인쇄 배율을 **실제 크기(100%)**로 설정하세요. “A4에 맞춤”을 선택하면 문서가 확대되거나 배치가 달라질 수 있습니다.

경북대학교(KNU) 이학석사 학위논문 작성을 위한 LaTeX 템플릿입니다. **Gwenaelle Cunha Sergio**와 **Dennis Singh Moirangthem**이 작성한 Overleaf의 [PhD Thesis Template - KNU](https://www.overleaf.com/latex/templates/phd-thesis-template-knu/wzwwnhnmbdjq)를 수정했습니다. 표지, 심사위원 승인 페이지, 목차, 그림·표 목록, 참고문헌, 영문·국문 초록을 포함합니다.

XeLaTeX으로 컴파일하며, 영문 기본 글꼴은 TeX Gyre Termes를 사용합니다. 한글 본문과 표지 등에는 `fonts/`의 글꼴 파일을 사용합니다. 제출 전에는 소속 학과의 논문 작성 지침과 최종 PDF를 대조하세요.

## 환경 설정

### 로컬 설치

**XeLaTeX**, **BibTeX**, **latexmk**, **ko.TeX**(한글 조판)를 포함한 TeX 배포판이 필요합니다. Ubuntu/Debian에서는 다음 패키지로 시작할 수 있습니다.

```bash
sudo apt update
sudo apt install latexmk texlive-xetex texlive-lang-korean \
  texlive-latex-extra texlive-fonts-recommended texlive-publishers tex-gyre
```

macOS에서는 [MacTeX](https://www.tug.org/mactex/), Windows에서는 [TeX Live](https://www.tug.org/texlive/) 또는 [MiKTeX](https://miktex.org/)을 설치하고 동등한 패키지를 준비하세요. 참고문헌 양식은 `IEEEtran.bst`이며, Biber가 아닌 BibTeX을 사용합니다.

`thesis.tex`가 있는 디렉터리에서 터미널을 열고 확인합니다.

```bash
xelatex --version
bibtex --version
latexmk --version
kpsewhich kotex.sty
kpsewhich IEEEtran.bst
```

`fonts/`를 `thesis.tex`와 같은 디렉터리에 유지하세요. 스타일 파일이 아래 파일을 직접 읽으므로 운영체제에 별도로 설치할 필요는 없습니다.

- `batang.ttc`
- `unbatang-IT.ttf`
- `malgungothic-R.ttf`, `malgungothic-BD.ttf`, `malgungothic-IT.ttf`

### VS Code 사용 (선택)

이 디렉터리를 폴더로 열고 권장 확장인 **LaTeX Workshop** (`james-yu.latex-workshop`)을 설치하세요. 포함된 `.vscode/settings.json`은 파일 변경 시 latexmk를 통해 XeLaTeX과 BibTeX을 자동 실행하도록 설정되어 있습니다. `thesis.tex`를 연 상태에서 **LaTeX Workshop: Build LaTeX project** 명령을 사용할 수도 있습니다.

기본 빌드 레시피는 **latexmk (XeLaTeX + BibTeX)**입니다. latexmk가 필요한 경우 BibTeX을 실행하고, 목차·인용·교차 참조가 갱신될 때까지 XeLaTeX을 반복 실행합니다. `latexmk`, `xelatex`, `bibtex` 명령이 PATH에 있어야 합니다. `tex/` 안의 파일을 편집하다가 루트 문서가 잘못 선택되면 `thesis.tex`를 열고 빌드하세요.

### Overleaf 사용

소스 파일과 `tex/`, `figures/`, `fonts/`를 함께 Overleaf 프로젝트에 업로드하세요. 주 문서는 `thesis.tex`, 컴파일러는 **XeLaTeX**으로 설정하고 다시 컴파일합니다. 로컬에서 생성된 `.aux`, `.bbl`, `thesis.pdf` 등은 업로드하지 않아도 됩니다.

## 빌드

`thesis.tex`가 있는 디렉터리에서 실행합니다.

```bash
latexmk -xelatex -interaction=nonstopmode -file-line-error thesis.tex
```

결과는 `thesis.pdf`로 생성됩니다. 수동으로 빌드하려면 다음 순서로 실행하세요.

```bash
xelatex -interaction=nonstopmode -file-line-error thesis.tex
bibtex thesis
xelatex -interaction=nonstopmode -file-line-error thesis.tex
xelatex -interaction=nonstopmode -file-line-error thesis.tex
```

PDF를 남기고 중간 빌드 파일을 정리하려면 다음을 실행합니다.

```bash
latexmk -c thesis.tex
```

## 간단한 사용법

1. **논문 정보를 입력합니다.** `thesis.tex`의 `\title`, `\author`, `\submitdate`, `\supervisor`, `\department`와 심사위원 `\profA`, `\profB`, `\profC`를 수정하세요. 국문 정보인 `\titlekorean`, `\authorkorean`, `\supervisorkorean`, `\departmentkorean`도 입력합니다. 필요한 곳에는 `\\`로 줄바꿈을 넣을 수 있습니다. 표지에는 지도교수 필드 앞에 “Supervised by Professor”가 자동으로 붙습니다.
2. **예제 본문을 교체합니다.** `tex/introduction.tex`, `tex/sections.tex`, `tex/adding_equations.tex`, `tex/adding_refs.tex`, `tex/conclusion.tex`를 수정하세요. `article` 클래스를 사용하므로 본문의 큰 구분은 `\chapter`가 아니라 `\section`으로 시작합니다.
3. **초록을 작성합니다.** `tex/abstract_english.tex`와 `tex/abstract_korean.tex`의 예제 문장을 교체하세요. 영문 초록의 학부명은 현재 `thesis.sty`의 `\makeabstractheader`에 직접 적혀 있으므로 필요하면 해당 부분도 수정합니다.
4. **참고문헌을 추가합니다.** `bibliography.bib`에 항목을 넣고 `\cite{lin2004rouge}`처럼 키로 인용합니다. 인용을 수정한 뒤에는 전체 빌드를 실행하세요.
5. **그림을 추가합니다.** `figures/`에 파일을 넣고 `\includegraphics`, `\caption`, `\label`을 사용합니다. `tex/sections.tex`의 예제를 참고하세요.

새 절을 추가하려면 `tex/method.tex` 같은 파일을 만듭니다.

```latex
\section{Method}\label{sec:method}
Describe your method here.
```

`thesis.tex`의 원하는 위치에 기존 그림·표 번호 초기화 방식에 맞춰 삽입합니다.

```latex
\setcounter{figure}{0}
\setcounter{table}{0}
\input{tex/method} \pagebreak
```

| 경로 | 역할 |
| --- | --- |
| `thesis.tex` | 주 문서, 논문 정보, 본문 순서 |
| `thesis.sty` | 페이지 배치, 표지 매크로, 글꼴, 제목 서식 |
| `tex/packages.tex` | 추가 LaTeX 패키지 |
| `tex/` | 본문과 초록 |
| `bibliography.bib` | BibTeX 참고문헌 |
| `figures/` | 그림 파일 |
| `fonts/` | 스타일에서 직접 읽는 글꼴 |
| `.vscode/` | 공통 편집기 설정 |

`fontspec` 오류가 나면 XeLaTeX을 선택했는지 확인하세요. 글꼴 파일을 찾지 못하면 `fonts/`의 파일과 실행 디렉터리를 확인합니다. 인용이 `?`로 표시되면 `bibliography.bib`에 해당 키가 있는지 확인한 뒤 전체 빌드를 실행하세요.

## 저작권 및 라이선스

원본 템플릿의 저작권은 **Gwenaelle Cunha Sergio**와 **Dennis Singh Moirangthem**에게 있습니다. [Overleaf 원본 페이지](https://www.overleaf.com/latex/templates/phd-thesis-template-knu/wzwwnhnmbdjq)에 명시된 라이선스는 **Creative Commons 저작자표시 4.0 국제(CC BY 4.0)**입니다.

이 수정본에는 이학석사 학위명 적용, 한글 글꼴·배치 조정, 심사위원 날인용 원문자와 편집기 설정 추가, 로컬 사용 문서 작성이 포함됩니다. 소스의 원저작권 표기는 유지했습니다. 출처, 라이선스 링크 및 적용 범위는 [LICENSE](LICENSE)에 정리했습니다. 글꼴 등 제3자 자료는 각각의 이용 조건을 따르며, 템플릿 라이선스만으로 해당 자료의 재배포 권리가 확인되는 것은 아닙니다.
