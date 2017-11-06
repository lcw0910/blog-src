---
title: Atom 프론트엔드 개발환경 세팅하기
date: 2017-10-28 15:57:31
tags:
- editor
- Atom
- 에디터
- 플러그인
- 개발환경 세팅
categories:
- Development
- Setting
---
## 플러그인 설치하기
- atom-beautify
https://atom.io/packages/atom-beautify
HTML, CSS, JavaScript, PHP, Python, Ruby, Java, C, C++, C#, Objective-C, CoffeeScript, TypeScript 등의 코드를 아릅답게 정렬해 주는기능

- docblockr
https://atom.io/packages/docblockr
메소드 작성 완료 후 윗라인에 “/**”을 치고 엔터를 치면 함수명, 파라미터명, 리턴타입등 깔끔한 주석 포멧을 제공해준다.
설명과 파라미터, 리턴타입등에 대한 추가 정보만 입력하면 된다. javascript 외에도 많은 언어를 지원한다.

- emmet
https://atom.io/packages/emmet
흔히 젠코딩이라 불리는 플러그인이다. 손가락 관절에 무리를 줄여주고 커피시간을 벌어주는 편리한 플러그인.

- minimap
https://atom.io/packages/minimap
작업중인 파일에 대한 미니맵 제공, 미니맵은 미니맵에 diff표시, 선택영역 하이라이트등 다양한 플러그인이 있지만 그닥 유용하지 않아
해당 플러그인만 사용중. 미니맵을 드래그하여 페이지 상하 이동이 가능하여 긴 내용의 코드 작성시 유용하다.

- open-in-browser
https://atom.io/packages/open-in-browser
아톰에서 작업중인 html파일을 브라우저에서 열어보는 플러그인.
가장 무난하고 깔끔해서 계속 사용중.

- run-in-atom
https://atom.io/packages/run-in-atom
아톰 에디터에서 바로 스크립트를 돌려볼 수 있는 플러그인.
사실상 크롬 개발자도구에서 작성한 js파일을 실행하는 방식이지만 생각보다 유용하다.

- seti-icon
https://atom.io/packages/seti-icons
아톰 아이콘 패키지로 개인취향이다. 해당 아이콘팩에 아톰 style.less를 조금 수정하여 사용한다.
참고로 다운로드 수는 file-icons(https://atom.io/packages/file-icons)가 20배이상 높다 ㅋ

- split-diff
https://atom.io/packages/split-diff
원래는 간단하게 diff확인할 경우 https://www.diffchecker.com/ 통해서 확인햇었는데
아톰에서 바로 확인할 수 있는 심플한 플러그인이라 애용중이다.
diff확인 및 변경이력 적용도 가능하다.

- color-picker
https://atom.io/packages/color-picker
컬러피커로 rgb, rgba, hex등 다양한 색상값을 바로 얻을 수 있다.

- markdown-preview-plus
https://atom.io/packages/markdown-preview-plus
아톰에는 markdown-preview가 기본으로 탑재되어 있다. 해당 플러그인을 사용할러면 기본 플러그인을 disable처리해 줘야한다.
아니면 설정값을 두번씩 해주면 되긴하다. 실시간으로 마크다운 프리뷰를 확인할 수 있으며 프리뷰 창에서 우클릭하여 브라우저로 확인하거나 export to disk를 누르면 html, pdf, ebook로 내보낼 수 있다. 문서 내용이 길어지면 약간 버벅이지만 유용한 플러그인
