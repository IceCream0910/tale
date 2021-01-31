---
layout: post
author: "Ice Cream"
title:  "브라우저를 위한 서비스, 확장앱"
subtitle: "네이버 웨일 브라우저 확장앱 개발기"
type: "Personal Project"
projects: true
text: true
ridi: true
portfolio: true
post-header: true
header-img: "https://whale-store.pstatic.net/20190731_251/1564570419662rzlXa_PNG/1.png?type=f790_495"
main-img: "https://whale-store.pstatic.net/20190731_251/1564570419662rzlXa_PNG/1.png?type=f790_495"
role-title: "디자인/개발"
role-specific: ""
platforms: "Chrome Extension"
date: "2020.03 - 현재"
order: 1
---

# Google Keep
## 이제 사이드바에서 만나보세요

[다운로드](https://store.whale.naver.com/detail/mpigbcflpddfcbidjdnaadbccaffdene)

![스크린샷](https://whale-store.pstatic.net/20181114_263/15421901137710girQ_PNG/slide1.png?type=f790_495)

처음으로 개발한 아주아주 간단한 확장앱입니다.

확장앱을 런칭할 '네이버 웨일' 브라우저에는 사이드바라는 기능이 있습니다. 브라우저 창 옆에서 다른 창을 모바일버전으로 띄워 동시에 작업할 수 있는 기능인데요. 이 사이드바에 확장앱을 넣을 수도 있습니다. 물론 사이트도 추가할 수 있었죠.

그래서 스마트폰에서 자주 사용하던 Google Keep(keep.google.com) 주소를 추가해 사용하려 했습니다.
그런데 앱을 설치하라는 팝업이 계속 뜨더군요. 모바일버전으로 열리기 때문에 이런 것이었습니다.(현재는 개선되어 최초1회만 표시되는 것 같아요)

이런 문제를 해결하기 위해 사이드바에 PC환경으로 페이지를 불러오는 확장앱을 만들었습니다. Google Keep 페이지는 반응형이었기 때문에 쉽게 구현이 가능했죠.

## 어려웠던 점
이렇게 평화롭게 동작했던 확장앱에 Google Keep의 디자인 개편과 함께 문제가 찾아옵니다. 사이드 툴바가 왼쪽에 표시되는데 사이드바 페이지 크기를 작게 하면 메모의 오른쪽 부분이 일부 잘리는 문제가 있었습니다.(사실 구글에서 해결해주면 좋은 문제여서 기다리다가 개선했습니다)

이를 해결하기 위해 content_scripts 이용했답니다. 처음에는 아예 이 툴바를 없애버렸는데요. 이게 또 필요한 경우가 있더군요.
그래서 상단바에 있는 메뉴버튼(선 세개)를 누르면 요 툴바가 보였다 안보였다 하게 만들어 개선했습니다.

~~~
"content_scripts": [
        {
            "matches": [
                "https://keep.google.com/*"
            ],
            "run_at": "document_end",
            "all_frames": true,
            "js": [
                "script.js"
            ]
        }
    ]
~~~
요렇게 하고
~~~
if (navigator.userAgent.includes("sidebar")) {
  document.querySelector(
    "body > div.notes-container > div:nth-child(2) > div:nth-child(1)"
  ).style.display = "none";
}
~~~
script.js에 이런식으로 해주면 사이드바에서 google keep을 열때 css를 제어할 수 있습니다.

---

# Blockit - 사이트 차단
## 집중을 방해하거나 유해한 웹 사이트를 간단히 차단하세요.


[다운로드](https://store.whale.naver.com/detail/gfdaidimgcibdjiidpmbobhhaojnjbfd)

![스크린샷](https://whale-store.pstatic.net/20191229_257/1577546353275xMyTc_PNG/1.png?type=f790_495)

집중을 방해하거나 유해한 웹 사이트를 간단히 차단하세요.
인터넷을 하다가 불필요한 사이트에 접속해 업무에 방해가 된 적이 있나요?
자녀가 부적절한 사이트에 들어갈까 봐 걱정되시나요?
그렇다면, Blockit을 사용해보세요.

STEP 1: 사이드바에 추가된 Blockit 아이콘을 눌러 실행하세요.
STEP 2: 사이트 주소 입력 란에 차단을 원하는 사이트 주소를 입력하세요.
STEP 3: 엔터 키나 입력창 오른쪽 + 버튼을 눌러주세요.
STEP 4: 입력창 아래 리스트에 사이트가 추가되었다면, 이제 해당 사이트로의 접속이 차단됩니다.

- 확장 앱 상단 2번째 버튼(W 모양)을 눌러 키워드 차단을 설정할 수 있어요.
- 확장 앱 상단 3번째 버튼을 눌러 예외 처리해보세요.

* 네이버를 차단할 경우 웨일의 일부 기능이 동작하지 않으며, 이외에도 사이트에 따라 이용에 제한이 있을 수 있습니다.

## 어려웠던 점
어느 날 어마어마한 문제가 발생합니다. 앞으로 서비스를 만들 때 더 책임감을 가지고 신중하게 개발해야 겠다는 생각을 하게 된 일이죠.

문제가 발생한 버전에서는 외부 api를 불러오는 코드가 있었는데요.
개발 시 만들었다가 실제로는 사용하지 않을 기능이기에 없애야 했지만, 남아있는채로 출시했습니다.
그런데 이 api 서버가 삭제된 순간 오류를 내뿜으며 브라우저를 완전히 먹통으로 만들었습니다....

확인하자마자 업데이트를 배포하고 스토어 댓글과 사용자 커뮤니티에 가서 사과를 해야했습니다 :(

혹시 문제를 겪으셨던 분이 이걸 보고계시다면 다시 한 번 사과드립니다.

---

### 이 외에도 이런 확장앱들이 있어요.
[T-REX Runner](https://store.whale.naver.com/detail/jindgfnppjdpmgdfiakaonemdkkjgcdj)

[Breaklock](https://store.whale.naver.com/detail/jindgfnppjdpmgdfiakaonemdkkjgcdj)