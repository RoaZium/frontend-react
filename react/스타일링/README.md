CSS는 이상하게도 웹 개발자가 배우기 가장 쉬우면서 가장 어려운 언어 중 하나로 여겨집니다. 확실히 시작은 쉽습니다. 특정한 엘리먼트에 적용할 스타일 프로퍼티와 값을 정의하면... 거의 끝입니다! 하지만, 더 큰 프로젝트의 경우에는 의미있는 CSS로 구성하는 것이 어렵고 복잡합니다. 한 페이지의 어떤 엘리먼트를 스타일링 하기 위해 CSS의 어떤 라인을 변경하면, 종종 다른 페이지의 엘리먼트가 의도하지 않게 변경됩니다.

CSS 고유의 복잡성을 처리하기위해서, 모든 종류의 다양한 모범 사례(best practice)가 확립되었습니다. 문제는 어떤 모범 사례가 실제로 제일 나은지 대한 합의된 내용이 없고, 모범 사례 중 많은 것들이 서로를 완전히 반박하는 것처럼 보인다는 것입니다. 만약 처음으로 CSS를 배우려고 한다면, 이 말이 혼란스러울 수 있습니다.

이 글의 목표는 CSS 방식과 툴이 어떻게 2018년 현재의 모습으로 발전했는지 역사적인 맥락을 알려주는 것입니다. 이 역사를 이해하면 각 방식을 이해하는 것이 더 쉬워지고, 장점으로 활용하는 법을 쉽게 이해할 수 있습니다. 시작해 봅시다!

CSS로 기본적인 스타일링하기
간단한 index.html과 거기에 연결되는 index.css 파일로 기본적인 웹사이트를 시작해봅시다.

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Modern CSS</title>
  <link rel="stylesheet" href="index.css">
</head>
<body>
  <header>This is the header.</header>
  <main>
    <h1>This is the main content.</h1>
    <p>...</p>
  </main>
  <nav>
    <h4>This is the navigation section.</h4>
    <p>...</p>
  </nav>
  <aside>
    <h4>This is an aside section.</h4>
    <p>...</p>
  </aside>
  <footer>This is the footer.</footer>
</body>
</html>
지금 우리는 HTML의 클래스나 id나 class를 사용하지않고, 단지 시멘틱 태그만 사용합니다. CSS가 없으면 웹사이트는 다음과 같습니다(더미 텍스트를 사용):

라이브 예제를 보려면 여기를 클릭하세요

기능적이긴 하지만 그리 예쁘지는 않습니다. 우리는 index.css에 기본적인 타이포그래피를 개선하는 CSS를 추가할 수 있습니다:

/_ 기본 폰트 _/
/_ 출처: <https://github.com/oxalorg/sakura> _/
html {
font-size: 62.5%;
font-family: serif;
}
body {
font-size: 1.8rem;
line-height: 1.618;
max-width: 38em;
margin: auto;
color: #4a4a4a;
background-color: #f9f9f9;
padding: 13px;
}
@media (max-width: 684px) {
body {
font-size: 1.53rem;
}
}
@media (max-width: 382px) {
body {
font-size: 1.35rem;
}
}
h1, h2, h3, h4, h5, h6 {
line-height: 1.1;
font-family: Verdana, Geneva, sans-serif;
font-weight: 700;
overflow-wrap: break-word;
word-wrap: break-word;
-ms-word-break: break-all;
word-break: break-word;
-ms-hyphens: auto;
-moz-hyphens: auto;
-webkit-hyphens: auto;
hyphens: auto;
}
h1 {
font-size: 2.35em;
}
h2 {
font-size: 2em;
}
h3 {
font-size: 1.75em;
}
h4 {
font-size: 1.5em;
}
h5 {
font-size: 1.25em;
}
h6 {
font-size: 1em;
}
여기에 있는 대부분의 CSS는 타이포그래피(폰트 사이즈, 행간 등), 색상, 가운데 정렬 레이아웃에 대한 스타일을 지정합니다. 이 각각의 속성에 적절한 값을 선택하려면 디자인을 공부해야 하지만(이 스타일들은 sakura.css에서 나온 것입니다), 여기에서 사용되는 CSS는 읽기 그렇게 복잡하지 않습니다. 결과는 다음과 같습니다:

라이브 예제를 보려면 여기를 클릭하세요

정말 다르군요! 프로그래밍이나 복잡한 로직을 요구하지 않고 단순한 방법으로 문서에 스타일을 추가하는 것이 CSS의 약속입니다. 안타깝지만 CSS를 타이포그래피, 색상 이상의 (다음에 다룰) 작업에 사용하면 점점 복잡해 집니다.

CSS로 레이아웃 잡기
1990년대에, CSS가 널리 사용되기 전에는 페이지에 컨텐츠를 배치할 수 있는 옵션이 많지 않았습니다. HTML은 원래 사이드바, 컬럼이 있는 동적인 웹사이트가 아닌 일반적인 문서를 만드는 언어로 설계되었습니다. 초기에는, HTML 테이블로 레이아웃을 잡았습니다. 전체 웹페이지가 테이블 안에 있어, 행과 열안에 컨텐츠를 구성하기 위해 사용할 수 있었습니다. 이러한 방식은 효과가 있었지만, 내용와 표현이 강하게 결합해서, 사이트의 레이아웃을 변경하려면 상당한 양의 HTML을 다시 작성해야 한다는 단점이 있었습니다.

CSS가 나타나자, (HTML로 작성한) 컨텐츠와 (CSS로 작성한) 표현를 분리해서 유지하는 것이 강하게 추진되었습니다. 그래서 사람들은 HTML에서 (더 이상 테이블이 아닌) 모든 레이아웃 코드를 CSS로 옮길 방법을 찾았습니다. HTML처럼 CSS도 실제로 페이지의 컨텐츠를 배치하기 위해서 설계된 것이 아니었기 때문에, 이렇게 분리하려는 초기의 시도는 깔끔하게 달성하기 어려웠습니다.

위 예제에서 실제로 이것이 어떻게 작동하는지 살펴 보겠습니다. CSS 레이아웃을 정의하기 전에, 우리는 먼저 (레이아웃 계산에 영향을 미치는) magrin과 padding을 초기화 하고, 섹션 별로 고유한 색상을 지정합니다.(예쁘게 하기 위해서가 아니라, 서로 다른 레이아웃을 테스트할 때 시각적으로 각 섹션이 눈에 띄도록 하기 위해서)

/_ 레이아웃 리셋과 색상 추가 _/

body {
margin: 0;
padding: 0;
max-width: inherit;
background: #fff;
color: #4a4a4a;
}
header, footer {
font-size: large;
text-align: center;
padding: 0.3em 0;
background-color: #4a4a4a;
color: #f9f9f9;
}
nav {
background: #eee;
}
main {
background: #f9f9f9;
}
aside {
background: #eee;
}
이제 웹사이트는 일시적으로 이렇게 보입니다:

라이브 예제를 보려면 여기를 클릭하세요

이제 CSS를 사용하여 페이지의 컨텐츠를 배치할 준비가 되었습니다. 우리는 시간 순으로 세 가지 다른 방법을 살펴볼 것입니다. 고전적인 float 기반 레이아웃부터 시작합니다.

Float 기반 레이아웃
CSS float 속성은 원래 텍스트 컬럼에 이미지를 왼쪽이나 오른쪽에 띄우기 위해 도입 되었습니다(종종 신문에서 볼 수 있습니다.) 2000년대 초반의 웹 개발자들은 단순히 이미지를 띄우는 것이 아니라, 모든 엘리먼트를 띄울 수 있다는 것을 이점으로 활용했습니다. 콘텐츠의 모든 div를 띄워 테이블의 행, 열로 만든 것과 같은 환상을 만들 수 있었습니다. 그러나 다시 말하자면, float은 이런 목적을 위해 만들어 진 것이 아니기 때문에, 이러한 환상을 만드는 것은 일관적인 방식으로 쉽게 풀리지 않았습니다.

2006년, A List Apart는 성배(Holy Grail)를 찾아서라는 유명한 기사를 내보냈습니다. 기사에서 성배(Holy Grail) 레이아웃(헤더, 세개의 컬럼, 푸터로 구성 됨)를 만드는 상세하고 철저한 방법을 요약했습니다. 꽤나 간단해보이는 레이아웃을 성배라고 부르는 것이 미친 소리같겠지만, 당시에 순수한 CSS를 사용하여 일관된 레이아웃을 만드는 것이 얼마나 힘든 일인지 보여주는 것입니다.

다음은 그 기사에서 설명한 기술을 기반으로 한 float 기반의 레이아웃 예제입니다:

/_ float 기반 레이아웃 _/

body {
padding-left: 200px;
padding-right: 190px;
min-width: 240px;
}
header, footer {
margin-left: -200px;
margin-right: -190px;  
}
main, nav, aside {
position: relative;
float: left;
}
main {
padding: 0 20px;
width: 100%;
}
nav {
width: 180px;
padding: 0 10px;
right: 240px;
margin-left: -100%;
}
aside {
width: 130px;
padding: 0 10px;
margin-right: -100%;
}
footer {
clear: both;
}

- html nav {
  left: 150px;
  }
  CSS를 살펴보면, 잘 동작하게 하기위해 몇 가지 핵을 사용한 것을 알 수 있습니다(음수 값 margin, clear: both속성, 하드 코딩한 width 계산, 등). 그 기사는 각각 핵의 이유를 자세히 설명해놓았습니다. 결과는 아래와 같습니다:

라이브 예제를 보려면 여기를 클릭하세요

훌륭하지만, 3개의 열이 높이가 같지 않고, 페이지가 화면의 높이를 채우지 못하는 것을 볼 수 있습니다. 이 문제는 float 기반의 방법이 문제입니다. float이 할 수 있는 일은 컨텐츠를 섹션의 왼쪽이나 오른쪽에 배치하는 것 뿐입니다. CSS는 다른 섹션의 높이를 알 수 있는 방법이 없습니다. 이 문제는 수년 후 flexbox기반의 레이아웃으로 해결되었습니다.

Flexbox 기반 레이아웃
CSS flexbox 속성은 2009년에 처음 제안되었지만, 2015년 전까지는 브라우저 지원 율이 크게 떨어졌습니다. flexbox는 공간이 한 개의 열이나 행에서 나눠지는 방식을 정의하도록 설계되어서, float을 사용하는 것에 비해 레이아웃을 정의하는데 더 적합합니다. 즉, float 기반 레이아웃을 사용한지 10년이 지난 후에, 웹 개발자는 드디어 float에 필요한 핵 없이 레이아웃용 CSS를 사용할 수 있었습니다.

아래는 Solved by Flexbox 라는 (여러가지 flexbox 예제를 보여주는 인기있는)사이트에서 설명한 기술을 기반으로 만든 flexbox 기반의 레이아웃 예제입니다. flexbox를 동작하게 하려면, HTML의 세 개의 열에 대한 추가적인 div 래퍼(wrapper)가 필요합니다.

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Modern CSS</title>
  <link rel="stylesheet" href="index.css">
</head>
<body>
  <header>This is the header.</header>
  <div class="container">
    <main>
      <h1>This is the main content.</h1>
      <p>...</p>
    </main>
    <nav>
      <h4>This is the navigation section.</h4>
      <p>...</p>
    </nav>
    <aside>
      <h4>This is an aside section.</h4>
      <p>...</p>
    </aside>
  </div>
  <footer>This is the footer.</footer>
</body>
</html>
CSS의 flexbox 코드는 다음과 같습니다:

/_ flexbox 기반 레이아웃 _/

body {
min-height: 100vh;
display: flex;
flex-direction: column;
}
.container {
display: flex;
flex: 1;
}
main {
flex: 1;
padding: 0 20px;
}
nav {
flex: 0 0 180px;
padding: 0 10px;
order: -1;
}
aside {
flex: 0 0 130px;
padding: 0 10px;
}
float 기반 레이아웃 방식에 비해 훨씬 컴팩트합니다! flexbox 속성과 값은 얼핏 보기에 꽤 혼란스럽지만, float 기반 레이아웃에서 필요한 음수값 margin같은 핵이 많이 필요하지 않습니다. 아주 큰 승리죠. 결과는 다음과 같이 보여질 것입니다:

라이브 예제를 보려면 여기를 클릭하세요

훨씬 낫군요! 열은 모두 높이가 같고, 페이지의 전체 높이를 차지합니다. 어떤 의미에서는 이것이 완벽해 보일 수 있지만, 이 방법에는 몇 가지 사소한 단점이 있습니다. 하나는 브라우저 호환성입니다. 현재 모든 최신 브라우저는 flexbox를 지원하지만, 일부 오래된 브라우저는 영원히 지원하지 않을 것입니다. 다행히 브라우저 업체는 이런 오래된 브라우저 지원을 끝내기 위해 많은 노력을 기울이고 있으며, 웹 디자이너들을 위해 일관된 개발 환경을 만들고 있습니다. 또 다른 단점은 마크업에 <div class="container>를 추가해야 한다는 것입니다. 피할 수 있다면 좋겠지요. 이상적인 세계라면, 레이아웃 관련 CSS 때문에 HTML을 변경할 필요가 전혀 없을 것입니다.

가장 큰 단점은 CSS 코드 자체입니다. flexbox는 수많은 float 핵을 제거하지만, flexbox의 코드는 레이아웃을 정의하기에는 직관적이지 않습니다. flexbox CSS를 읽고 모든 요소들이 시각적으로 어떻게 페이지에 배치되는지 이해하는 것은 어렵습니다. 이 점이 flexbox 기반 레이아웃을 작성할 때 많이 추측하고 확인하게합니다.

중요한 것은 flexbox는 한 개의 열 또는 행의 요소를 배치하도록 설계되었습니다는 것입니다—전체 페이지 레이아웃을 위해 디자인 된것이 아닙니다! 이 것으로 서비스 할 수 있는 결과를 만들수 있지만(float 기반 레이아웃보다 훨씬 효율적임), 여러 행과 열을 가진 레이아웃을 처리할 수 있는 다른 스펙이 특별히 개발되었습니다. 이 스펙은 바로 CSS grid입니다.

Grid 기반 레이아웃
CSS grid는 2011년에 처음 제안되었으며(flexbox 제안 이후 그렇게 오래 걸리지는 않음), 브라우저에 널리 동작하기까지는 오랜 시간이 걸렸습니다. 2018년 초반부터, CSS grid는 대부분의 최신 브라우저에서 지원됩니다(1~2년 전부터 큰 개선이 있었습니다).

다음은 CSS tricks의 기사에서 첫번째 방법을 기반으로한 grid 기반의 레이아웃입니다. 이 예제에서는 flexbox 기반 레이아웃에서 추가해야 했던 <div class="container">를 제거할 수 있습니다. 수정없이 원본 HTML을 간단하게 사용할 수 있습니다. 여기 CSS는 다음과 같습니다:

/_ grid 기반 레이아웃 _/

body {
display: grid;
min-height: 100vh;
grid-template-columns: 200px 1fr 150px;
grid-template-rows: min-content 1fr min-content;
}
header {
grid-row: 1;
grid-column: 1 / 4;
}
nav {
grid-row: 2;
grid-column: 1 / 2;
padding: 0 10px;
}
main {
grid-row: 2;
grid-column: 2 / 3;
padding: 0 20px;
}
aside {
grid-row: 2;
grid-column: 3 / 4;
padding: 0 10px;
}
footer {
grid-row: 3;
grid-column: 1 / 4;
}
결과는 flexbox 기반 레이아웃과 시각적으로 똑같습니다. 하지만, 여기에서 CSS가 원하는 레이아웃을 명확하게 표현한다는 점에서 훨씬 개선되었습니다. 열과 행의 크기와 모양은 body 선택자에서 정의되며, grid안의 각 항목은 자신의 위치로 직접 정의됩니다.

"열의 시작점 / 열의 끝 점"을 정의하는 grid-column 속성이 혼란스러울 수 있습니다. 이 예에서는 3개의 열이 있지만 숫자 범위에서는 1~4이므로 혼동을 줄 수 있습니다. 아래 그림을 보면 더 명확해질 것입니다:

라이브 예제를 보려면 여기를 클릭하세요

첫번째 열은 1에서 시작하여 2에서 끝나고, 두번째 열은 2에서 시작하여 3에서 끝나고, 세번째 열은 3에서 시작하겨 4에서 끝납니다. 헤더는 grid-column이 1/4로 전체 페이지에 걸쳐있고, 네비게이션은 1/2로 grid-column으로 첫번째 열에 걸쳐있습니다.

한번 grid 문법에 익숙해지면, CSS에서 레이아웃을 표현하는 이상적인 방법이 됩니다. grid 기반의 레이아웃의 유일한 단점은 브라우저 호환성이며, CSS grid의 브라우저 지원은 지난 한해 동안 크게 향상되었습니다. CSS grid는 레이아웃을 위해 설계된 실질적인 CSS의 첫번째 툴이기 때문에 매우 중요합니다. 어떤 의미에서, 웹디자이너는 창의적인 레이아웃을 만드는 것에 항상 보수적이여야했습니다. 지금까지 나온 도구들이 다양한 핵과 꼼수를 사용해서 깨지기 쉬웠기 때문입니다. 이제는 CSS grid가 존재하기 때문에, 이전에는 불가능했던 창의적인 레이아웃 디자인의 새로운 물결을 일으킬 가능성이 있습니다. 흥미진진하네요!

새 문법을 위한 CSS 전처리기 사용하기
지금까지 레이아웃과 기본 스타일링을 위해 CSS를 사용하는 것에 대해 다루었습니다. 이제 CSS 전처리기(preprocessor)부터 시작해서 CSS라는 언어를 사용 경험을 향상시키는데 도움을 줄 도구들에 대해 살펴보겠습니다.

CSS 전처리기를 사용하면 다른 언어를 이용하여 스타일을 작성할 수 있게 해주고, 그 코드를 브라우저에서 이해할 수 있는 CSS로 변환할 수 있습니다. 브라우저가 새로운 기능을 구현하는 속도가 매우 느릴 때에는 매우 중요한 것이였습니다. 첫번째 유명한 CSS 전처리기는 2006년에 릴리즈된 Sass입니다. 새롭고 간결한 문법(대괄호 대신 들여쓰기, 세미콜론 없음 등)과 변수, 헬퍼 함수, 계산과 같은 CSS엔 없는 고급 기능이 추가되었습니다. 이전 예제의 섹션 컬러링을 Sass 변수로 사용하면 다음과 같습니다:

$dark-color: #4a4a4a
$light-color: #f9f9f9
$side-color: #eee
body
color: $dark-color

header, footer
background-color: $dark-color
color: $light-color

main
background: $light-color
nav, aside
  background: $side-color
$ 기호로 재사용가능한 변수를 정의할 수 있습니다. 괄호와 세미콜론을 제거해서 깔끔한 구문을 만들수도 있습니다. Sass의 깔끔한 문법도 훌륭하지만, 당시에는 변수와 같은 기능들은 매우 혁명적이였습니다. 깨끗하고 유지 보수하기 쉬운 CSS를 작성하는 새로운 가능성을 열었습니다.

Sass를 사용하려면 Sass코드를 CSS코드로 컴파일하는데 사용되는 프로그래밍언어인 Ruby를 설치해야 합니다. 그런 다음 Sass gem을 설치하고, .sass 파일을 .css파일로 변환하는 명령어를 커맨드 라인에 입력해 실행합니다. 다음은 명령어의 예시입니다:

sass --watch index.sass index.css
이 명령어는 index.sass라는 파일에 작성된 sass코드를 index.css 파일에 일반 CSS로 변환합니다(--watch 인자는 저장 시에 내용이 바뀔 때마다 명령을 실행하는 편리한 기능입니다).

이 과정을 빌드 과정이라고 하며, 2006년 전에는 상당히 진입 장벽이 있었습니다. 만약 Ruby와 같은 프로그래밍 언어를 사용하는데 익숙하다면, 이 과정은 매우 간단합니다. 하지만 당시 많은 프론트엔드 개발자들은 HTML과 CSS만 사용했습니다. 그런 도구들을 필요하지 않았습니다. 따라서 누군가 CSS 전처리기가 제공하는 기능을 쓰기 위해서는 전체적인 생태계를 배우도록 하는 것이 중요합니다.

2009년에는 Less라는 CSS 전처리기가 출시 되었습니다. 이것 또한 Ruby로 작성되었고, Sass와 유사한 기능을 제공합니다. 주요한 차이점은 문법이 CSS와 최대한 비슷하게 디자인 되었다는 것입니다. 즉, 어떤 CSS코드라도 Less코드로 쓸 수 있습니다. 똑같은 예제를 Less 구문을 사용하여 작성 한 것을 봅시다:

@dark-color: #4a4a4a;
@light-color: #f9f9f9;
@side-color: #eee;
body {
color: @dark-color;
}

header, footer {
background-color: @dark-color;
color: @light-color;
}

main {
background: @light-color;
}
nav, aside {
background: @side-color;
}
($ 대신 @를 변수 접두어로 쓰는 것 빼고) 대부분 비슷하지만, CSS와 같이 중괄호와 세미콜론을 사용해서 Sass 예제처럼 코드가 예쁘지는 않습니다. 그러나 CSS와 비슷하기 때문에 개발자가 Less를 선택하기 쉽게 만들었습니다. 2012년, Less는 컴파일을 위해 Ruby 대신 JavaScript(정확히는 Node.js)로 다시 작성되었습니다. Less는 Ruby를 사용할 때보다 빠르게 만들었고, 이미 Node.js를 개발에 사용하고 있던 개발자들에게 더욱 어필할 수 있었습니다.

이 코드를 일반 CSS로 변환하려면, 먼저 Node.js를 설치해야합니다. 그다음 Less를 설치하고 다음 명령어를 실행시킵니다:

lessc index.less index.css
이 명령은 index.less 파일에 적힌 Less 코드를 index.css파일의 일반 CSS로 변환합니다. lessc 명령어는 sass 명령어와 달리 파일의 변화를 감지하는 방식을 제공하지 않습니다. 즉, 자동으로 감시해서 .less파일을 컴파일하고 싶다면 다른 툴을 설치해야해서, 과정이 조금 더 복잡해집니다. 다시 말하지만, 커맨드 라인 사용에 익숙한 프로그래머라면 어렵지 않겠지만, 단순하게 그냥 CSS 전처리기를 사용하려는 사람에게는 진입장벽이 됩니다.

Less가 인지도를 더 얻으면서, Sass 개발자들은 SCSS라고 하는 새로운 문법을 2010년에 추가했습니다(Less와 비슷하게 CSS를 포함하는 상위 집합). 또한 Ruby Sass 엔진을, C/C++로 포팅한 LibSass를 출시하여 빠르고 다양한 언어를 사용할 수 있습니다.

또 다른 CSS 전처리기는 Stylus입니다. Stylus는 2010년에 Node.js로 작성되었고, Sass 나 Less에 비해 좀 더 깨끗한 문법에 중점을 둡니다. 일반적으로 CSS 전처리기에 대한 이야기는 가장 인기있는 세가지(Sass, Less, Stylus)에 초점을 둡니다. 결국 그것들이 제공하는 기능은 모두 매우 비슷합니다. 그래서 어떤 것을 고르던지 잘못될 일은 없습니다.

하지만 몇 사람들은 CSS 전처리기가 덜 필요하게 될것이라고 주장합니다. 브라우저가 마침내 전처리기의 기능들(변수나 계산 같은 기능)을 구현하기 시작했기 때문입니다. 게다가, CSS 후처리기로 알려진 다른 방식이 있습니다. 이 것은 CSS 전처리기를 쓸모없게 만들 수 있는 힘이 있습니다(이에 대해 논란이 있긴 합니다). 다음 장에서 알아봅시다.

변형 기능을 위해서 CSS 후처리기 사용하기
CSS 후처리기(postprocessor)는 JavaScript를 이용해 작성한 CSS코드를 분석하고 유효한 CSS로 변형합니다. 이 점에서는 CSS 전처리기와 매우 유사합니다. 동일한 문제를 해결하려는 다른 접근 방식이라고 생각할 수 있습니다. 주요한 차이점은 CSS 전처리기가 특별한 문법을 사용하여 변환해야 할 대상을 식별하는 반면에, CSS 후처리기는 일반적인 CSS 구문을 분석하고 특별한 문법 없이 변환할 수 있다는 것입니다. 아래 예를 통해 잘 설명할 수 있습니다. 헤더 태그의 스타일을 지정하기 위해 위에서 정의한 CSS의 일부를 살펴보겠습니다:

h1, h2, h3, h4, h5, h6 {
-ms-hyphens: auto;
-moz-hyphens: auto;
-webkit-hyphens: auto;
hyphens: auto;
}
상위 3개의 항목을 벤더 프리픽스라고 합니다. 벤더 프리픽스는 브라우저가 실험적으로 새로운 CSS 기능을 추가하거나 테스트 할 때 사용되며, 개발자가 구현이 완료되는 동안에 새로운 CSS 속성을 사용할 수 있도록 제공합니다. 여기서 -ms 프리픽스는 마이크로소프트 인터넷 익스플로러용이며, -moz 프리픽스는 모질라 파이어폭스용이고, -webkit 프리픽스는 (구글 크롬, 사파리, 최신 버전 오페라와 같이) 웹킷 렌더링 엔진을 사용하는 브라우저용입니다.

이 CSS 속성을 사용하기 위해서 모든 다른 벤더 프리픽스를 붙이 것을 기억하는 일은 매우 짜증납니다. 필요한 경우에 자동으로 벤더 프리픽스를 넣어주는 도구가 있다면 좋겠군요. 우리는 이것을 CSS 전처리기로 처리할 수 있습니다. 예를 들어서, 다음과 같이 SCSS로 처리할 수 있습니다:

@mixin hyphens($value) {
-ms-hyphens: $value;
-moz-hyphens: $value;
-webkit-hyphens: $value;
hyphens: $value;
}
h1, h2, h3, h4, h5, h6 {
@include hyphens(auto);
}
여기서 우리는 Sass의 mixin 기능을 사용합니다. 이 기능을 사용하면 CSS 덩어리를 한번 정의한 다음 다른 곳에서 재사용 할 수 있습니다. 이 파일은 일반 CSS로 컴파일하면, @include문은 @mixin의 CSS로 바뀝니다. 전반적으로 나쁘지 않은 해결책이지만, 매번 벤더 프리픽스가 필요한 CSS 속성에 한번씩 mixin을 정의해야 합니다. 브라우저가 CSS 호환성을 업데이트 하면서, 더 이상 필요하지 않은 특정 벤더 프리픽스를 제거할 수 있으므로 정의한 mixin에 유지보수가 필요합니다.

mixin을 사용하는 대신, 일반 CSS를 작성하고 프리픽스가 필요한 속성을 툴이 자동으로 식별하여 적절하게 추가하도록 하는 것이 좋습니다. CSS 후처리기라면 정확하게 수행할 수 있습니다. 예를 들어 PostCSS를 autoprefixer 플러그인과 함께 사용한다면, 벤더 프리픽스 없이 일반 CSS를 다 작성할 수 있습니다. CSS 후처리기가 나머지 작업을 수행하도록 할 수 있기 때문입니다:

h1, h2, h3, h4, h5, h6 {
hyphens: auto;
}
이 코드에서 CSS 후처리기를 실행하면, hypens: auto;이 있는 행이 적절한 벤더 프리픽스로 바뀝니다. (autoprefixer 플러그인에 정의되어있으니, 직접 관리할 필요가 없습니다.) 호환성이나 특수한 문법에 대해서 걱정할 필요가 없이 일반적인 CSS를 작성할 수 있다는 것을 의미합니다. 멋있군요!

PostCSS의 autoprefixer이외에도 멋진 일을 할 수 있는 플러그인이 있습니다. cssnext플러그인을 사용하면 아직 실험적인 CSS 기능을 사용할 수 있습니다. CSS modules는 이름 충돌을 피하기 위해서 클래스 명을 자동으로 바꿔주는 플러그인입니다. stylelint 플러그인은 CSS에 있는 오류나 일관적이지 않은 컨벤션을 식별합니다. 이 도구들은 지난 1~2년 사이에 시작해서, 이전에는 불가능했던 개발자의 워크플로우를 보여주고 있습니다.

하지만 후처리기를 사용하는 데에는 약간의 지불해야할 대가가 있습니다. PostCSS와 같은 CSS 후처리기를 설치하고 사용하는 것은 CSS 전처리기를 사용하는 것과 비교해서 더 복잡합니다. 커맨드 라인을 이용하여 툴을 설치/실행하는 것 뿐아니라, 각 플러그인을 설치/설정하고, 더 복잡한 규칙들을(타겟으로 하는 브라우저 등) 정의해야 합니다. 많은 개발자들이 커맨드 라인에서 직접 PostCSS를 실행하는 대신 프론트엔드 워크플로우에서 사용할 수 있는 Grunt, Gulp와 같은 설정할 수 있는 빌드 시스템이나 다른 빌드 도구를 관리하는 webpack에 통합해서 사용합니다.

참고: 이전에 한번도 최신 프론트엔드 빌드 시스템을 구축하는데 필요한 것을 배우지 않았더라면 꽤 힘들 것입니다. 만약 처음부터 시작하고 싶다면, 프론트엔드 개발자를 위해 이 최신 기능의 장점 활용하는데에 필요한 모든 JavaScript 툴을 설명하는 Modern JavaScript Explained For Dinosaurs(공룡을 위한 모던 Javascript)라는 내 글을 읽어보기 바랍니다.

CSS 후처리기에 대한 논쟁이 있지만, 그것은 별로 논할 가치가 없습니다. 어떤 사람들은 용어가 혼란스럽다고 주장합니다(모두 다 CSS 전처리기라고 부르자는 주장, 모두 다 간단하게 CSS 처리기라고 부르자는 또 다른 주장 등). 일부에서는 CSS 후처리기가 CSS 전처리기의 필요성을 없앤다고 하고, 일부는 두 개를 꼭 같이 사용해야한다고 생각합니다. 어쨌든 CSS로 가능한 것의 한계를 뛰어넘는 데에 관심이 있다면 CSS 후처리기를 사용하는 방법을 배우는 것은 분명 가치가 있을 겁니다.

유지보수를 위해 CSS 방법론을 사용하기
CSS 전처리기와 CSS 후처리기와 같은 도구는 CSS 개발 경험을 향상시키는데 도움이 됩니다. 하지만 이러한 도구만으로는 큰 CSS 코드베이스를 유지보수하는 문제를 해결하기엔 충분하지 않습니다. 이를 해결하기 위해 사람들은 일반적으로 CSS 방법론이라고 하는 CSS를 작성하는 방법에 대한 여러 가이드라인을 문서화하기 시작했습니다.

특정 CSS 방법론을 배우기 전에, 무엇이 시간이 지남에 따라 CSS를 유지하게 어렵게 만드는 것인지 이해하는 것이 중요합니다. 핵심은 CSS의 글로벌한(전역) 특성입니다. 정의한 모든 스타일은 페이지의 모든 부분에 글로벌하게 적용됩니다. 유니크한 클래스 이름을 유지하기 위해 상세한 네이밍 컨벤션을 제안하거나, 어떤 요소에 스타일을 적용하기 위해 명시도 규칙과 씨름하는 것이 여러분의 일이 될 것입니다. CSS 방법론은 큰 규모의 코드 베이스로 위와 같은 고통을 피하기 위해서 CSS를 작성하는 체계적인 방법을 제공합니다. 인기있는 방법론을 대략적인 시간 순서로 살펴보겠습니다.

OOCSS
OOCSS(Object Oriented CSS, 객체 지향 CSS)는 2009년에 발표된 방법론으로, 두 가지 주요 원칙으로 구성되어있습니다. 첫 번째 원칙은 구조와 겉모습의 분리입니다. 즉, (레이아웃 같은)구조를 정의하는 CSS와 (색상, 폰트 등과 같은)겉모습을 정의하는 CSS를 섞어서 정의하지 말라는 것입니다. 이렇게 하면 애플리케이션에 쉽게 "겉모습을 다시 입힐 수" 있습니다. 두 번째 원칙은 컨텐츠과 컨테이너의 분리입니다. 이것은 요소를 재사용 가능한 객체로 생각한다는 것을 의미합니다. 핵심 아이디어는 객체가 페이지에 어디에 있든지 동일하게 보인다는 것입니다.

OOCSS는 잘 설명된 가이드라인을 제공하지만, 방식의 세부에 대한 룰은 매우 러프합니다. 나중에 나온 SMACSS와 같은 방식은 핵심 컨셉을 취하고, 시작하기 쉽도록 세부사항을 추가했습니다.

SMACSS
SMACSS(Scalable and Modular Architecture for CSS, CSS를 위한 확장가능하고 모듈화된 아키텍처)는 2011년에 나온 CSS를 5가지 다른 카테고리로 나눠 작성하는 방법론입니다. 기본 규칙, 레이아웃 규칙, 모듈, 상태 규칙, 테마 규칙으로 나눕니다. SMACSS 방법론은 몇가지 네이밍 컨벤션을 권장합니다. 레이아웃 규칙의 경우, l-이나 layout-이라는 프리픽스를 클래스 이름에 붙입니다. 상태 규칙의 경우, 상태를 설명하는 클래스 앞에 프리픽스를 붙입니다. is-hidden이나 is-collapsed처럼요.

SMACSS는 OOCSS에 비해 방식이 더 구체적이지만, 마찬가지로 어떤 CSS 규칙이 어떤 카테고리에 속해야 하는지 신중하게 고려해서 결정해야 합니다. 다음에 나오는 BEM과 같은 방식은 적용하기 쉽도록 결정해야 하는 것의 일부를 없앴습니다.

BEM
BEM(Block, Element, Modifier)는 2010년에 소개된 방법론입니다. 사용자 인터페이스를 독립된 블록으로 나누는 아이디어를 중심으로 구성되었습니다. 블록(block)은 재사용 가능한 컴포넌트입니다(예: <form class="search-form">></form>으로 정의한 검색 폼). 엘리먼트(element)는 블록 안의 한 부분으로, 단독으로는 재사용할 수 없습니다(예: <button class="search-form__button">Search</button>로 정의한 검색 폼 내의 버튼). 수정자(Modifier)는 블록이나 엘리먼트의 생김새, 상태, 동작을 정의하는 엔티티입니다(예: <button class="search-form__button search-form__button--disabled">Search</button>으로 정의된 비활성화된 검색 폼 버튼).

BEM 방법론은 입문자들이 복잡한 결정을 내리지 않고도 적용할 수 있는 구체화된 네이밍 컨벤션때문에 이해하기 쉽습니다. 클래스의 이름이 매우 장황해지고, 의미있는 클래스 이름을 짓는 전통적인 룰을 따르지 않는다는 몇몇 단점이 있습니다. 다음에 나올 Atomic CSS와 같은 방식은 이와 같이 전통적이지 않은 방식을 완전히 다른 수준으로 취합니다.

Atomic CSS
Atomic CSS(함수형 CSS라고도 함)은 2014년에 소개된 방법론입니다. 시각적인 기능을 기반으로 하나의 목적을 가진 작은 클래스를 만드는 아이디어를 중심으로 구성되었습니다. 이 방식은 OOCSS, SMACSS, BEM과 완전히 반대입니다. Atomic CSS는 페이지의 요소를 재사용가능한 객체로 다루지 않고, 객체라는 개념을 무시하고, 각 엘리먼트를 재사용 가능한 하나의 목적을 가진 유틸리티 클래스들로 스타일링을합니다. 그래서 <button class="search-form__button">Search</button>과 같은 것 대신에, <button class="f6 br3 ph3 pv2 white bg-purple hover-bg-light-purple">Search</button>같은 것을 쓰게 될 겁니다.

이 예제를 본 당신의 첫번째 반응은 공포일겁니다. 당신 혼자만 그런 것은 아닙니다. 많은 사람들은 기존의 CSS 모범 사례를 완전히 파괴한 방법론으로 봤습니다. 그러나, 여러 다른 시나리오에서 기존의 모범 사례가 효과적인지에 대해 의문을 제기하는 훌륭한 토론들이 있었습니다. 이 글에서는 기존의 분리하는 방식이 (BEM과 같은 방법론을 쓴다 하더라도) HTML에 의존하는 CSS를 만들게 된다는 것을 강조하고 있습니다. 반면 Atomic 혹은 함수형 방법은 CSS에 의존하는 HTML을 만든다는 것을 보여주고 있습니다. 어느 쪽도 틀린 것은 아니지만, 자세히 살펴보면 CSS와 HTML사이에는 진정한 관계 분리는 완전하게 이루어질 수 없다는 것을 알 수 있습니다!

CSS in JS와 같은 다른 CSS 방법론은 CSS와 HTML이 항상 서로에게 의존한다는 개념을 전적으로 포용해서, 아직까지 가장 논란이 되고 있는 방법 중 하나입니다...

CSS in JS
CSS in JS(JavaScript 안의 CSS)는 별도의 스타일 시트가 아니라, 각 컴포넌트에 직접 정의하는 방법론으로 2014년에 소개되었습니다. 이 방법은 React Javascript 프레임워크에 대한 방법으로 소개 되었습니다. (이 프레임워크는 별도의 HTML 파일 대신 JavaScript안에 직접 컴포넌트의 HTML을 정의하는 논란이 많은 방식을 이미 취하고 있습니다.) 원래 이 방법론은 인라인 스타일을 사용했지만, 나중에는 JavaScript를 사용하여 (컴포넌트를 기반으로 유니크한 클래스 이름을 생성하여) CSS를 생성하고, 문서의 style 태그에 삽입하도록 구현되었습니다.

CSS in JS 방법론의 CSS는 기존의 관심사의 분리의 CSS 모범 사례에 완전히 반대되는 방향으로 가고 있습니다. 웹을 사용하는 방식이 시간이 지남에 따라서 극적으로 바뀌었기 때문입니다. 원래 웹은 주로 정적인 사이트로 구성되어 있었습니다. 여기에서 CSS 표현과 HTML 컨텐츠를 분리하는 것은 많은 의미가 있습니다. 요즘 웹은 동적 웹 어플리케이션을 만드는데 사용됩니다. 여기서는 재사용 가능한 컴포넌트로 분리하는 것이 좋습니다.

CSS in JS 방법론의 목표는 하나의 컴포넌트에 있는 CSS가 다른 컴포넌트에 영향을 미치지 않도록 자체적으로 캡슐화 된 HTML/CSS/JS로 구성된 뚜렷한 경계가 있는 컴포넌트를 정의 할 수 있게 하는 것입니다. React는 이러한 뚜렷한 경계를 갖는 컴포넌트를 첫번째로 널리 적용한 프레임워크 중에 하나입니다. Angular, Ember, Vue.js 와 같은 다른 주요 프레임워크에 영향을 미쳤습니다. CSS in JS 방법론은 비교적 새롭고, 개발자가 웹 어플리케이션용 컴포넌트의 시대에서 CSS를 위한 새로운 모범 사례를 확립하려고 시도하는 것에 따라 이 분야에서 많은 실험이 진행되고 있다는 것을 알아 두는 것이 중요합니다.

서로 다른 다양한 CSS 방법론에 압도당하기 쉽지만 정답은 없다는 점을 기억하세요. 많이 복잡한 CSS 코드베이스를 가지고 있을 때 사용할 수 있는 여러가지 툴이 있다는 것으로 기억하는 것이 좋습니다. 작업에 있어 선호도에 따라 고를 수 있는 그간 논의되어온 다양한 선택지들과, 최근에 진행되는 모든 실험은 결국 모든 개발자에게 장기적으로 도움이 됩니다!

결론
그래서 지금까지 간결하게 모던 CSS를 알아보았습니다. 우리는 타이포그래피 속성으로 기본 스타일링에 CSS를 사용하는 것과, float, flexbox, grid를 기반으로 한 방식을 이용하여 CSS로 레이아웃 잡는 것과, 변수나 믹스인과 같은 새로운 문법을 쓰는 CSS 전처리기를 사용하는 것과, 벤더 프리픽스를 붙이는 것 과 같은 변환 기능을 쓰는 CSS 후처리기를 사용하는 것과, CSS 스타일의 글로벌적인 특성을 다루기 위해서 유지보수를 위한 CSS 방법론을 사용하는 것을 살펴 봤습니다. 고급 선택자, 트렌지션, 애니메이션, 모양, 동적 변수와 같이 CSS가 제공하는 다른 많은 기능을 살펴볼 기회가 없었습니다. 그 기능 리스트는 계속 늘어나네요. CSS를 다루는 데에는 많은 배경지식이 있습니다. 쉽다고 말하는 사람은 아마 절반도 모를겁니다!

모던 CSS는 계속해서 빠르게 변화하고 발전하기 때문에 CSS를 사용할 때에 좌절을 느낄 수 있습니다. 어떻게 웹이 발전했는가 역사적 문맥을 기억하는 것이 중요합니다. CSS 모범 사례가 웹과 함께 바른 방향으로 발전할 수 있도록 구체적인 도구와 방법론을 만드려는 똑똑한 사람들이 많이 있다는 것을 아는 것도 중요합니다. 개발자가 되기 가장 좋은 시기이고, 저는 이 정보가 여러분의 여정을 도와줄 로드 맵으로 사용되기를 바랍니다!
