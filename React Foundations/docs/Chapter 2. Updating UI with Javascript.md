Chapter 2

# JavaScript로 UI 업데이트하기

자바스크립트와 DOM 메서드를 사용하여 프로젝트에 `h1` 태그를 추가하는 방법을 살펴봅시다.

코드 편집기를 열고 새로운 `index.html` 파일을 만들어보세요. HTML 파일 안에 다음의 코드를 추가합니다:

```html
<html>
  <body>
    <div></div>
  </body>
</html>
```

그런 다음 `div`에 나중에 대상으로 지정할 수 있도록 고유한 `id`를 지정해보세요.

```html
<html>
  <body>
    <div id="app"></div>
  </body>
</html>
```

HTML 파일 내에서 자바스크립트를 작성하려면 `script` 태그를 추가하세요:

```html
<html>
  <body>
    <div id="app"></div>
    <script type="text/javascript"></script>
  </body>
</html>
```

이제, `script` 태그 안에서, DOM 메서드인 `getElementById()`를 사용해 `id`로 `<div>` 요소를 선택할 수 있습니다:

```html
<html>
  <body>
    <div id="app"></div>

    <script type="text/javascript">
      const app = document.getElementById('app');
    </script>
  </body>
</html>
```

새로운 `<h1>` 요소를 만들기 위해 계속해서 DOM 메서드를 사용할 수 있습니다:

```html
<html>
  <body>
    <div id="app"></div>

    <script type="text/javascript">
      // 'app' id를 가진 div 요소 선택
      const app = document.getElementById('app');

      // 새로운 H1 요소 만들기
      const header = document.createElement('h1');

      // H1 요소용 새 텍스트 노드 생성
      const text = 'Develop. Preview. Ship. 🚀';
      const headerContent = document.createTextNode(text);

      // 텍스트를 H1 요소에 추가
      header.appendChild(headerContent);

      // H1 요소를 div 안에 배치
      app.appendChild(header);
    </script>
  </body>
</html>
```

잘 작동하는지 확인하려면 HTML 파일을 원하는 브라우저에서 열어보세요. 'Develop. Preview. Ship. 🚀'라고 쓰인 h1 태그가 보일 것입니다.

&nbsp;

### HTML vs. DOM

[브라우저 개발자 도구](https://developer.chrome.com/docs/devtools/overview/) 내에서 DOM 요소를 살펴보면 DOM에 `<h1>` 요소가 포함되어 있음을 알 수 있습니다. 페이지의 DOM은 소스 코드(당신이 작성한 원본 HTML 파일)와 다릅니다.

![DOM과 소스 코드(HTML)의 차이점](https://nextjs.org/_next/image?url=%2Fstatic%2Fimages%2Flearn%2Ffoundations%2Fsource-code.png&w=1920&q=75&dpl=dpl_68SyDasVh5cW8stCg4cSvM4vtq44)

처음에 만든 HTML 파일은 **초기 페이지 콘텐츠**를 나타내는 반면에, DOM은 당신이 작성한 자바스크립트 코드로 변경된 **업데이트된 페이지 콘텐츠**를 나타내기 때문입니다.

순수 자바스크립트로 DOM을 업데이트하는 것은 매우 강력하지만 코드가 길어질 수 있습니다. 당신은 이렇게 모든 코드를 작성하여 `<h1>` 요소를 추가했습니다:

```html
<script type="text/javascript">
  const app = document.getElementById('app');
  const header = document.createElement('h1');
  const text = 'Develop. Preview. Ship. 🚀';
  const headerContent = document.createTextNode(text);
  header.appendChild(headerContent);
  app.appendChild(header);
</script>
```

앱이나 팀의 크기가 커질수록 이 방식으로 애플리케이션을 구축하는 것은 점점 어려워질 수 있습니다.

이 방법을 사용하면 개발자는 컴퓨터에게 **어떻게** 해야 하는지 지시하는 명령을 많이 작성해야 합니다. 그런데 DOM을 **어떻게** 업데이트할지는 컴퓨터에게 맡기고 당신은 **무엇을** 보여주고 싶은지 설명한다면 더 좋지 않을까요?

&nbsp;

### 명령적 vs. 선언적 프로그래밍

위의 코드는 **명령적 프로그래밍**의 좋은 예입니다. 사용자 인터페이스가 **어떻게** 업데이트되어야 하는지에 대한 단계를 작성하고 있습니다. 그러나 사용자 인터페이스를 구축할 때 선언적 접근 방식이 선호되는 경우가 많습니다. DOM 메서드를 작성하는 대신 개발자가 **무엇을** 표시할지 선언할 수 있다면 유용할 것입니다(이 경우 텍스트가 포함된 `h1` 태그).

다시 말해, **명령적 프로그래밍**은 요리사에게 피자를 어떻게 만들어야 하는지 단계별 지시를 하는 것과 같습니다. **선언적 프로그래밍**은 피자가 어떻게 만들어지는지에 대해 걱정하지 않고 피자를 주문하는 것과 같습니다. 🍕

개발자가 사용자 인터페이스를 구축하는 데 도움이 되는 선언적 라이브러리 중 하나가 [React](https://react.dev/)입니다.

&nbsp;

### React: 선언적 UI 라이브러리

개발자로서, 당신은 React에게 사용자 인터페이스에 대한 원하는 대로 알릴 수 있으며, React는 당신을 대신하여 **어떻게** DOM을 업데이트할 것인지 단계를 파악할 것입니다.

다음 섹션에서 React를 시작하는 방법에 대해 알아보겠습니다.

&nbsp;

> 추가 자료:
>
> - [HTML 대 DOM](https://developer.chrome.com/docs/devtools/dom/#appendix)
> - [선언적 UI와 명령적 UI 비교](https://react.dev/learn/reacting-to-input-with-state#how-declarative-ui-compares-to-imperative)
