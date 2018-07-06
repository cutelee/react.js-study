# React
react는 facebook에서 제작한 오픈소스 MVC 프레임워크로, 자바스크립트로 사용자 인터페이스를 구축하는 창의적인 접근 방법을 제공한다. View 부분을 컴포넌트로 만들기 위한 라이브러리이다.

1. Just the UI : UI 컴포넌트를 만들기 위한 라이브러리로, UI와 관련된 컴포넌트만 지원한다.
2. Virtual DOM : 자바스크립트 내에 DOM Tree와 같은 구조체(=virtual DOM)를 가진다.
	> 다시 그릴 때에는 구조체의 전/후 상태를 비교해서 변경이 필요한 최소한의 요소만 실제 DOM에 반영하기 때문에, 빠른 처리가 가능하다는 장점을 가진다.
3.  Data Flow : 단방향 데이터 바인딩

	* **데이터 바인딩**이란 [\[출처\]](https://sungjk.github.io/2015/11/22/AngularJS%282%29.html)
		두 데이터 혹은 정보의 소스를 모두 일치시키는 방법. 화면에 보이는 데이터와 브라우저 메모리에 있는 데이터를 일치시키는 기법이다.

		 1. *단방향 데이터 바인딩* : 대다수의 자바스크립트 프레임워크가 지원, 데이터와 템플릿을 결합해서 화면을 생성하는 방법이다.

		 2. *양방향 데이터 바인딩* : AngularJS에서 지원. 데이터의 변화를 감지하여 템플릿과 결합해 화면을 갱신하고, 화면에서의 입력에 따라서 데이터를 갱신한다. 즉, 데이터와 화면 사이의 데이터가 계속해서 일치.

## React의 정의
React는 자바스크립트와 (필요에 따라) XML을 이용해 조합형 사용자 인터페이스를 구축하는 엔진이다.

* React는 엔진:

* 조합형 사용자 인터페이스를 구축:

* 자바스크립트와 XML을 이용:

## React의 장점

### SPA; Single Page Application
단일 페이지 애플리케이션. 사용자가 페이지에서 수행하는 모든 상호작용(ex: 버튼클릭)이 다른 페이지로 넘어가는 것이 아니라, DOM의 일부를 변화시키는 것. 페이지를 이동시키면 서버로부터 새 페이지를 전송받아야 하지만, DOM을 바꾸면 새로 받아올 필요가 없다. 그러나 후자의 경우는 인터페이스가 복잡해지면 애플리케이션의 현재 상태를 조사, 적절한 변경사항 반영, 업데이트 작업이 어려워진다.

### 반응형 랜더링
컴포넌트의 모양, 동작을 선언식으로 정의하면 리액트가 데이터 변경을 감지하고 개념상으로 전체 인터페이스를 다시 랜더링한다. 그런데 실제로 전체 인터페이스를 랜더링 하는 것은 성능 저하를 감안할 때 불가능하기 때문에 가상 DOM을 활용한다.

#### SPA의 단점
앱의 규모가 커지면 자바스크립트 파일 사이즈가 너무 커진다는 것. 유저가 실제로 방문하지 않을 수도 있는 페이지와 관련된 렌더링 관련 스크립트를 불러오기 때문. [\[참고\]](https://velopert.com/3417)

#### Routing
다른 주소에 따라 다른 뷰를 보여주는 것을 라우팅이라고 한다. React 자체에는 이 기능이 내장되어 있지 않기 때문에, 직접 브라우저의 API를 사용하고 상태를 설정해 다른 뷰를 보여주어야 한다. react-router 라이브라러리를 이용하면 클라이언트 사이드에서 이루어지는 라우팅을 간단하게 해준다.

---
# Virtual DOM

## virtual DOM이란 무엇인가
[\[동영상참고\]](https://www.youtube.com/watch?v=muc2ZF0QIO4)


## 왜 virtual DOM이 필요한가
앞서 위에서 말했듯이, 실제 전체 인터페이스를 다시 랜더링 하는 것은 성능 저하때문에 불가능 하기 때문에, 애플리케이션 상태가 달라지면 리액트는 UI의 현재 상태와 원하는 상태를 비교하고 DOM의 바뀐 부분만 최소한으로 수정하게 된다.

---
# Component
## component 정의

## component의 생성
component는 두 가지 방법으로 생성할 수 있는데, 하나는 클래스로 생성하는 것이고 하나는 함수로 생성하는 것이다. 딱히 복잡한 기능이 없고 값만 부모로부터 받는 경우에는 함수로 제작하는 것이 좋다.
### 클래스로 component 생성
	    this is example code

### 함수로 component 생성
	import React from 'react';
	import './Test.css';

	const Test = () => (
	    <div className="Test">
	        POSTS
	    </div>
	)
	export default Test;

아래에서 언급하게 될 상태가 없는 component의 경우 functional component로 만드는 것이 좋다. 보기에 깔끔하고, 컴포넌트의 로직을 컴포넌트 밖으로 옮기기 때문에, 테스트하기 편하다. 함수형 컴포넌트는 **this에 접근이 불가하고, lifeCycle API를 사용할 수 없다.** 오직 (부모로부터) 전달받는 props에 의존한다.

## Component의 메소드
### 일반적인 방식
	class MyComponent extends Component {
		constructor(props) {
			super();
			this.myMethod = this.myMethod.bind(this);
		}
		myMethod() { .. }
		render() { .. }
	}

위와 같이 일반적인 방식으로 Component의 메소드를 선언할 경우, constructor에서 bind를 해주어 this에 접근할 수 있도록 만들어줘야 한다.

### 화살표 함수를 이용한 방식
	class MyComponent extends Component {
		constructor(props) {
			super();
		}
		myMethod = () => {
			..
		}
		render() { .. }
	}

이렇게 화살표 함수로 메소드를 선언할 경우, 별도의 binding이 필요하지 않다.
> babel 플러그인 transform-class-properties 가 적용되어 있기 때문이며, create-react-app으로 만든 프로젝트에는 자동으로 적용되어 있다고 한다.


---

# 개발 환경 설정

## Node.js, npm, yarn
React에 필요한 도구인 webpack, babel이 node.js로 제작되었기 때문에, react를 사용하기 위해서는 node.js의 설치가 필요하다. (*node.js는 브라우저 밖의 환경에서 자바스크립트를 실행할 수 있도록 해주는 JavaScript Runtime이다.*)

### webpack

번들러 프로그램. 프로젝트에 필요한 여러 파일들(.js, .css)을 하나로 묶어주는 역할을 한다.

### npm, yarn

npm은 node package manager로 여러 패키지들의 설치, 버전관리 등을 돕는 프로그램이다. yarn은 npm보다 개선된 버전의 패키지 매니저이다.

* yarn 설치 방법 (별도로 정리)

		$ sudo apt-get install yarn -g


---

# create-react-app
create-react-app을 통해서 복잡한 의존성 패키지 설치(webpack, babel 등의 설정)과정 없이 쉽게 react application을 제작할 수 있다. [\[참고\]](https://velopert.com/2037)
> ES6문법을 사용하려면 webpack설정을 하고 babel로 컴파일 하는 방법을 사용하는데 create-react-app 패키지는 이 모든 과정을 자동으로 설정해줘서 react 진입장벽을 낮춰줍니다. 물론 나중에 config파일 설정도 `npm run eject`명령을 이용해서 가능합니다. [\[원글\]](https://qvil.github.io/react.js/reactjs-tutorial/)

## create-react-app installation
	npm install -g create-react-app

글로벌로 설치해주면 된다. 초간단.

## react project 생성

     $ create-react-app [project-name]
     $ cd [project-name]
     $ yarn start	(=npm start)

## 불필요한 파일 지우기

	[파일 구조]
		project-folder/
			README.md
			.gitignore
			package.json
			yarn.lock
			src/
				App.js
				App.css
				index.css
				index.js
				registerServiceWorker.js
				logo.svg
			public/
				index.html
				..
			node_modules/
여기에 logo 파일은 필요없고, App.js에도 들어가면 return에 막 써져있는데 다 필요없으므로 지우고 \<div>\</div>만 남겨두자.		

---
# JSX
> JSX is a statically-typed, object-oriented programming language designed to run on modern web browsers. Being developed at [DeNA](http://dena.com/intl/) as a research project, the language has following characteristics.

라고 JSX github페이지에 정의되어 있다.

## JSX 정의 [\[참고\]](http://blog.sonim1.com/175)
JSX는 JavaScript와 XML의 합성어로, 기존 자바스크립트의 확장 문법이다. UI를 트리 구조로 작성할 수 있는 간결하고 익숙한 구문을 제공하며, 자바스크립트의 의미를 바꾸지 않고 자바스크립트 코드 안에 XML을 넣을 수 있게 해준다. HTML과 유사한 형태를 띄고 있다. 하지만 자바스크립트라는 점 주의. JSX의 사용을 배제하고 리액트를 이용하는 것도 가능하지만, 그것은 react를 충분히 활용하는 것이 아니게 된다고 한다.

## 기초 문법 정리

JSX는 다음과 같은 몇 가지 문법 규칙을 가지고 있다. ~~이것 말고도 매우 많겠지만 중요한 것만 먼저 정리했다.~~

> 1. 모든 태그는 반드시 닫아주어야 한다.
> 2. 두 개 이상의 element는 반드시 다른 태그로 감싸주어야 한다. (return 문은 단일 값만 반환하기 때문, fragment라는 태그 사용)
> 3. 조건부 랜더링은 삼항연산자를 사용하여 간단하게 표현할 수 있다.

- fragment 태그

이것은 설명이다.

- 조건부 랜더링

이것도 설명이다.

---

# Props, State
## Props
컴포넌트의 구성 정보에 해당한다. 속성은 상위 컴포넌트로부터 받으며, 이를 받은 컴포넌트 내에서는 변경이 불가능하다.

### 속성 유효성 검사
컴포넌트를 조합하고 재사용하기 위해서는 컴포넌트에서 어떤 속성을 사용할 수 있고, 어떤 속성이 필수이며, 어떤 형식의 값을 받는지 등을 명시적으로 지정해 두는 것이 좋다. propTypes는 컴포넌트를 문서화하는 데 도움을 주는데, 다음과 같은 두 가지 장점이 있다.
> 1. 언제든지 컴포넌트를 열고 어떤 속성이 필요한지, 속성의 형식이 무엇인지 알 수 있음.
> 2. 문제가 발생한 경우 리액트가 콘솔에 오류 메시지를 출력해 어떤 속성이 잘못되거나 누락되었는지, 문제가 발생한 render 메서드는 무엇인지 알려줌.

원래는 react 라이브러리(? 프레임워크?) 내에 들어있어서 'react'에서 import 하면 됐는데, react 버전이 올라가면서 따로 'prop-types'로 빼냈다고 한다. 이거 때문에 오류가 나서 슬펐다. [[참고]](https://reactjs.org/docs/typechecking-with-proptypes.html)

    import React, { Component } from 'react';
    import PropTypes from 'prop-types';

    class Test extends Component {
	    render() { ... }
    };

    Test.propTypes = {
	    prop1: PropTypes.number,
	    prop2: PropTypes.func.isRequired	// 필수
    };
    export default Test;

유효성 검사기는 기본으로 제공되는 .array, .bool, .oneOfType([]), .arrayOf 등이 있지만 커스터마이징해서 적용할 수도 있다. 유효성 검사기를 함수로 만든 후에 propTypes를 지정해 줄 때 해당 함수 명을 쓰면 된다.

	let titlePropType = (props, propName, componentName) => {
		if(props[propName]) {
			..
		}
	};

	class Test extends Component {
		render() { .. }
	};

	Test.propTypes = {
		title: titlePropType
	};

	export default Test;

### 기본 속성값 지정하기


## State
상태는 컴포넌트의 생성자에 정의된 기본값에서 시작해 여러 차례 변경될 수 있다. 일반적으로 사용자 이벤트에 의해 변경된다. 컴포넌트는 자신의 상태를 내부적으로 관리하고, 상태가 변경될 때마다 컴포넌트가 다시 랜더링 된다.

---
# 컴포넌트 조합 전략
## 상태 저장 컴포넌트, 순수 컴포넌트

리액트 컴포넌트에서 상태는 선택적이다. 대부분의 리액트 애플리케이션에서 컴포넌트는 상태를 관리하는 컴포넌트와 상태 없이 데이터만 표시하는 컴포넌트 두 가지 유형으로 나뉜다.

- 상태 저장 컴포넌트: 상태를 관리
- 순수 컴포넌트: (내부 상태가 없고) 데이터를 표시하는 역할만 담당. 속성을 받아서 이를 뷰에 랜더링 하는 것이 전부이므로 재사용하거나 테스트하기 수월함.

상태 저장 컴포넌트는 일반적으로 컴포넌트 계층에서 상위를 차지하고, 다른 컴포넌트(상태 저장이나 순수)를 하나 이상 래핑한다. 앱의 컴포넌트는 대부분 상태 비저장(순수)으로 만드는 것이 좋다.

## 상태가 필요한 컴포넌트

---
# Component Styling

## 인라인 스타일링

리액트 컴포넌트에서는 인라인 스타일을 자바스크립트 객체로 지정한다. 표기법은 Camel 표기법을 따른다. 또한, 자동으로 적절한 단위를 지정하기 때문에 픽셀 단위를 따로 정해주지 않아도 된다.

    import react, { Component } from 'react';
    import { render } from 'react-dom';

    class Test extends Component {
	    render() {
		    let divStyle = {
			    backgroundColor: black,
			    padding: 5
			};
			return <div style={divStyle}>Hello, React!</div>
		}
    }

## 컴포넌트와 스타일 관리
### scss
좀 더 개선된 CSS? 스타일을 위한 디렉토리를 따로 만들어서 scss 파일만 모으고, component와 scss 파일을 따로 분리해서 관리할 수 있다. [참고]/아직 링크 안달음.

### .css
모든 component와 css를 한 폴더에 죄다 몰아넣어도 되고(;) 각 컴포넌트 별로 폴더를 만들어서 .js, .css를 관리하는 방법도 있다. *두 파일이 멀리 떨어져 있으면 import할 때 경로 설정하기 복잡해지니까 같이 두는 듯.*

---

# 참고자료
* (책) 프로리액트: React.js를 이용한 모던 프런트엔드 구축
* https://velopert.com/ : 리액트 강의를 잘 정리해두셨다.

# React
react는 facebook에서 제작한 오픈소스 프로젝트로, 자바스크립트로 사용자 인터페이스를 구축하는 창의적인 접근 방법을 제공한다.

## React의 정의
React는 자바스크립트와 (필요에 따라) XML을 이용해 조합형 사용자 인터페이스를 구축하는 엔진이다.

* React는 엔진:

* 조합형 사용자 인터페이스를 구축:

* 자바스크립트와 XML을 이용:

## React의 장점

### SPA; Single Page Application
단일 페이지 애플리케이션. 사용자가 페이지에서 수행하는 모든 상호작용(ex: 버튼클릭)이 다른 페이지로 넘어가는 것이 아니라, DOM의 일부를 변화시키는 것. 페이지를 이동시키면 서버로부터 새 페이지를 전송받아야 하지만, DOM을 바꾸면 새로 받아올 필요가 없다. 그러나 후자의 경우는 인터페이스가 복잡해지면 애플리케이션의 현재 상태를 조사, 적절한 변경사항 반영, 업데이트 작업이 어려워진다.

### 반응형 랜더링
컴포넌트의 모양, 동작을 선언식으로 정의하면 리액트가 데이터 변경을 감지하고 개념상으로 전체 인터페이스를 다시 랜더링한다. 그런데 실제로 전체 인터페이스를 랜더링 하는 것은 성능 저하를 감안할 때 불가능하기 때문에 가상 DOM을 활용한다.

#### SPA의 단점
앱의 규모가 커지면 자바스크립트 파일 사이즈가 너무 커진다는 것. 유저가 실제로 방문하지 않을 수도 있는 페이지와 관련된 렌더링 관련 스크립트를 불러오기 때문. [\[참고\]](https://velopert.com/3417)

#### Routing
다른 주소에 따라 다른 뷰를 보여주는 것을 라우팅이라고 한다. React 자체에는 이 기능이 내장되어 있지 않기 때문에, 직접 브라우저의 API를 사용하고 상태를 설정해 다른 뷰를 보여주어야 한다. react-router 라이브라러리를 이용하면 클라이언트 사이드에서 이루어지는 라우팅을 간단하게 해준다.

---
# Virtual DOM

## virtual DOM이란 무엇인가
[\[동영상참고\]](https://www.youtube.com/watch?v=muc2ZF0QIO4)


## 왜 virtual DOM이 필요한가
앞서 위에서 말했듯이, 실제 전체 인터페이스를 다시 랜더링 하는 것은 성능 저하때문에 불가능 하기 때문에, 애플리케이션 상태가 달라지면 리액트는 UI의 현재 상태와 원하는 상태를 비교하고 DOM의 바뀐 부분만 최소한으로 수정하게 된다.

---
# Component
## component 정의

## component의 생성
component는 두 가지 방법으로 생성할 수 있는데, 하나는 클래스로 생성하는 것이고 하나는 함수로 생성하는 것이다. 딱히 복잡한 기능이 없고 값만 부모로부터 받는 경우에는 함수로 제작하는 것이 좋다.
### 클래스로 component 생성
	    this is example code

### 함수로 component 생성
	import React from 'react';
	import './Test.css';

	const Test = () => (
	    <div className="Test">
	        POSTS
	    </div>
	)
	export default Test;

아래에서 언급하게 될 상태가 없는 component의 경우 functional component로 만드는 것이 좋다. 보기에 깔끔하고, 컴포넌트의 로직을 컴포넌트 밖으로 옮기기 때문에, 테스트하기 편하다. 함수형 컴포넌트는 **this에 접근이 불가하고, lifeCycle API를 사용할 수 없다.** 오직 (부모로부터) 전달받는 props에 의존한다.

## Component의 메소드
### 일반적인 방식
	class MyComponent extends Component {
		constructor(props) {
			super();
			this.myMethod = this.myMethod.bind(this);
		}
		myMethod() { .. }
		render() { .. }
	}

위와 같이 일반적인 방식으로 Component의 메소드를 선언할 경우, constructor에서 bind를 해주어 this에 접근할 수 있도록 만들어줘야 한다.

### 화살표 함수를 이용한 방식
	class MyComponent extends Component {
		constructor(props) {
			super();
		}
		myMethod = () => {
			..
		}
		render() { .. }
	}

이렇게 화살표 함수로 메소드를 선언할 경우, 별도의 binding이 필요하지 않다.
> babel 플러그인 transform-class-properties 가 적용되어 있기 때문이며, create-react-app으로 만든 프로젝트에는 자동으로 적용되어 있다고 한다.


---

# 개발 환경 설정

## Node.js, npm, yarn
React에 필요한 도구인 webpack, babel이 node.js로 제작되었기 때문에, react를 사용하기 위해서는 node.js의 설치가 필요하다. (*node.js는 브라우저 밖의 환경에서 자바스크립트를 실행할 수 있도록 해주는 JavaScript Runtime이다.*)

### webpack

번들러 프로그램. 프로젝트에 필요한 여러 파일들(.js, .css)을 하나로 묶어주는 역할을 한다.

### npm, yarn

npm은 node package manager로 여러 패키지들의 설치, 버전관리 등을 돕는 프로그램이다. yarn은 npm보다 개선된 버전의 패키지 매니저이다.

* yarn 설치 방법 (별도로 정리)

		$ sudo apt-get install yarn -g


---

# create-react-app
create-react-app을 통해서 복잡한 의존성 패키지 설치(webpack, babel 등의 설정)과정 없이 쉽게 react application을 제작할 수 있다. [\[참고\]](https://velopert.com/2037)
> ES6문법을 사용하려면 webpack설정을 하고 babel로 컴파일 하는 방법을 사용하는데 create-react-app 패키지는 이 모든 과정을 자동으로 설정해줘서 react 진입장벽을 낮춰줍니다. 물론 나중에 config파일 설정도 `npm run eject`명령을 이용해서 가능합니다. [\[원글\]](https://qvil.github.io/react.js/reactjs-tutorial/)

## create-react-app installation

## react project 생성

     $ create-react-app [project-name]
     $ cd [project-name]
     $ yarn start

## 불필요한 파일 지우기


---
# JSX
> JSX is a statically-typed, object-oriented programming language designed to run on modern web browsers. Being developed at [DeNA](http://dena.com/intl/) as a research project, the language has following characteristics.

라고 JSX github페이지에 정의되어 있다.

## JSX 정의 [\[참고\]](http://blog.sonim1.com/175)
JSX는 JavaScript와 XML의 합성어로, 기존 자바스크립트의 확장 문법이다. UI를 트리 구조로 작성할 수 있는 간결하고 익숙한 구문을 제공하며, 자바스크립트의 의미를 바꾸지 않고 자바스크립트 코드 안에 XML을 넣을 수 있게 해준다. HTML과 유사한 형태를 띄고 있다. 하지만 자바스크립트라는 점 주의. JSX의 사용을 배제하고 리액트를 이용하는 것도 가능하지만, 그것은 react를 충분히 활용하는 것이 아니게 된다고 한다.

## 기초 문법 정리

JSX는 다음과 같은 몇 가지 문법 규칙을 가지고 있다. ~~이것 말고도 매우 많겠지만 중요한 것만 먼저 정리했다.~~

> 1. 모든 태그는 반드시 닫아주어야 한다.
> 2. 두 개 이상의 element는 반드시 다른 태그로 감싸주어야 한다. (return 문은 단일 값만 반환하기 때문, fragment라는 태그 사용)
> 3. 조건부 랜더링은 삼항연산자를 사용하여 간단하게 표현할 수 있다.

- fragment 태그

이것은 설명이다.

- 조건부 랜더링

이것도 설명이다.

---

# Props, State
## Props
컴포넌트의 구성 정보에 해당한다. 속성은 상위 컴포넌트로부터 받으며, 이를 받은 컴포넌트 내에서는 변경이 불가능하다.

### 속성 유효성 검사
컴포넌트를 조합하고 재사용하기 위해서는 컴포넌트에서 어떤 속성을 사용할 수 있고, 어떤 속성이 필수이며, 어떤 형식의 값을 받는지 등을 명시적으로 지정해 두는 것이 좋다. propTypes는 컴포넌트를 문서화하는 데 도움을 주는데, 다음과 같은 두 가지 장점이 있다.
> 1. 언제든지 컴포넌트를 열고 어떤 속성이 필요한지, 속성의 형식이 무엇인지 알 수 있음.
> 2. 문제가 발생한 경우 리액트가 콘솔에 오류 메시지를 출력해 어떤 속성이 잘못되거나 누락되었는지, 문제가 발생한 render 메서드는 무엇인지 알려줌.

원래는 react 라이브러리(? 프레임워크?) 내에 들어있어서 'react'에서 import 하면 됐는데, react 버전이 올라가면서 따로 'prop-types'로 빼냈다고 한다. 이거 때문에 오류가 나서 슬펐다. [[참고]](https://reactjs.org/docs/typechecking-with-proptypes.html)

    import React, { Component } from 'react';
    import PropTypes from 'prop-types';

    class Test extends Component {
	    render() { ... }
    };

    Test.propTypes = {
	    prop1: PropTypes.number,
	    prop2: PropTypes.func.isRequired	// 필수
    };
    export default Test;

유효성 검사기는 기본으로 제공되는 .array, .bool, .oneOfType([]), .arrayOf 등이 있지만 커스터마이징해서 적용할 수도 있다. 유효성 검사기를 함수로 만든 후에 propTypes를 지정해 줄 때 해당 함수 명을 쓰면 된다.

	let titlePropType = (props, propName, componentName) => {
		if(props[propName]) {
			..
		}
	};

	class Test extends Component {
		render() { .. }
	};

	Test.propTypes = {
		title: titlePropType
	};

	export default Test;

### 기본 속성값 지정하기


## State
상태는 컴포넌트의 생성자에 정의된 기본값에서 시작해 여러 차례 변경될 수 있다. 일반적으로 사용자 이벤트에 의해 변경된다. 컴포넌트는 자신의 상태를 내부적으로 관리하고, 상태가 변경될 때마다 컴포넌트가 다시 랜더링 된다.

---
# 컴포넌트 조합 전략
## 상태 저장 컴포넌트, 순수 컴포넌트

리액트 컴포넌트에서 상태는 선택적이다. 대부분의 리액트 애플리케이션에서 컴포넌트는 상태를 관리하는 컴포넌트와 상태 없이 데이터만 표시하는 컴포넌트 두 가지 유형으로 나뉜다.

- 상태 저장 컴포넌트: 상태를 관리
- 순수 컴포넌트: (내부 상태가 없고) 데이터를 표시하는 역할만 담당. 속성을 받아서 이를 뷰에 랜더링 하는 것이 전부이므로 재사용하거나 테스트하기 수월함.

상태 저장 컴포넌트는 일반적으로 컴포넌트 계층에서 상위를 차지하고, 다른 컴포넌트(상태 저장이나 순수)를 하나 이상 래핑한다. 앱의 컴포넌트는 대부분 상태 비저장(순수)으로 만드는 것이 좋다.

## 상태가 필요한 컴포넌트

---
# Component Styling

## 인라인 스타일링

리액트 컴포넌트에서는 인라인 스타일을 자바스크립트 객체로 지정한다. 표기법은 Camel 표기법을 따른다. 또한, 자동으로 적절한 단위를 지정하기 때문에 픽셀 단위를 따로 정해주지 않아도 된다.

    import react, { Component } from 'react';
    import { render } from 'react-dom';

    class Test extends Component {
	    render() {
		    let divStyle = {
			    backgroundColor: black,
			    padding: 5
			};
			return <div style={divStyle}>Hello, React!</div>
		}


## 컴포넌트와 스타일 관리
### scss
좀 더 개선된 CSS? 스타일을 위한 디렉토리를 따로 만들어서 scss 파일만 모으고, component와 scss 파일을 따로 분리해서 관리할 수 있다. [참고]/아직 링크 안달음.

### .css
모든 component와 css를 한 폴더에 죄다 몰아넣어도 되고(;) 각 컴포넌트 별로 폴더를 만들어서 .js, .css를 관리하는 방법도 있다. *두 파일이 멀리 떨어져 있으면 import할 때 경로 설정하기 복잡해지니까 같이 두는 듯.*

---

# 참고자료
* (책) 프로리액트: React.js를 이용한 모던 프런트엔드 구축
* https://velopert.com/ : 리액트 강의를 잘 정리해두셨다.
* https://blog.coderifleman.com/2015/06/23/learning-react-1/ : React.js에 대한 소개
