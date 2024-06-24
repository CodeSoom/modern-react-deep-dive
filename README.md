# 모던 리액트 딥 다이브 문제 모음

## 1장

1. 다음 코드에서 버튼을 클릭했을 때 화면에 어떻게 보이는지, 리액트에서 동등 비교하는 방법과 함께 설명해 주세요.

```jsx
import { memo, useState } from 'react'

const Counter = memo((props) => {
  return (
    <>
      count: {props.state.count}
    </>
  )
});

const state = { count: 0 };

function App() {
  const [, setState] = useState(0);
  
  const handleClick = () => {
    state.count += 1;
    setState((prev) => prev + 1);
  }

  return (
    <div>
      <Counter state={state} />
      <button type="button" onClick={handleClick}>버튼</button>
    </div>
  );
}
```

2. 함수 선언문과 화살표 함수의 차이는 무엇인가요?
3. 좋은 함수란 무엇일까요?
4. 클로저란 무엇이고 동작 원리에 대해서 설명해 주세요.
5. 자바스크립트의 비동기가 동작하는 원리에 대해서 설명해 주세요.
6. 다음 코드들의 출력문이 어떻게 되는지 작성해 주세요.

```js
const array = [1, undefined, null, NaN, 5, 6, 7];
const [, a = 2, b = 3, c = 4, ...d, e] = array;
console.log(a, b, c, d, e);
```

```js
const object = {
  a: 1,
  b: 2,
  c: null,
  f: 'efg',
  g: 'hij'
};
const key = 'a';

const {
  [key]: foo,
  b,
  c = 4,
  d = 5,
  ...rest
} = object;
console.log(foo, b, c, d, rest);
```

7. any대신에 unknown을 써야하는 이유는 무엇인가요?
8. 다음 코드는 잘 동작하나요? 그 이유는 무엇인가요?

```ts
type Car = { name: string }
type Truck = Car & { power: number }

function horn(car: Car) {
  console.log(`${car.name}이 경적을 울립니다 빵빵!`);
}

const truck: Truck = {
  name: '비싼차',
  power: 100,
};

horn(truck);
```

## 2장

1. 다음 코드를 트랜스파일했을 때 출력이 어떻게 되는지 작성해
   주세요.(pseudocode로 작성해도 됩니다.)

```jsx
function Input(props) {
  return (
    <input type="text" onChange={props.onChange}/>
  )
}

const Component = (props) => {
  const handleChange = (event) => {
    console.log(event.target.value);
  }

  return (
    <div required value="hi">
      <Input onChange={handleChange} />
    </div>
  );
}
```

2. 브라우저가 웹사이트를 요청 하고 화면을 그리는 과정을 설명해 주세요.
3. 가상 DOM에 대한 일반적인 오해는, 일반적인 DOM을 관리하는 브라우저보다 빠르다는 것입니다. 이것이 오해인 이유를 설명해 주세요.
4. 리액트가 렌더링 되는 과정에 대해서 설명해 주세요.
5. 클래스형 컴포넌트를 공부해야 하는 이유는 무엇인가요?
6. 무조건 메모이제이션을 하는게 좋을까요? 아니면 필요한 곳에만 메모이제이션을 하는게 좋을까요?

## 3장

2. 함수형 컴포넌트가 매번 실행되더라도 useState가 이전의 값을 정확하게 꺼내 쓸 수 있는 이유는 무엇인가요?
3. useEffect의 클린업 함수와 생명주기 메서드의 언마운트 개념과 차이는 무엇인가요?
4. 다음 두 가지 코드의 실행 차이는 무엇인가요?

```javascript
// 1번
function Component() {
  console.log('렌더링됨');
}

// 2번
function Component() {
  useEffect(() => {
    console.log('렌더링됨');
  });
}
```

5. useEffect를 사용할 때 주의할 점은 무엇인가요?
6. 다음 코드의 위험성은 무엇인가요?

```jsx
const fetchInfo = async () => {
  // ... 생략
  return {
    data: ['something'],
  };
}

function Component({id}) {
  const [info, setInfo] = useState();

  useEffect(() => {
    fetchInfo(id)
      .then(setInfo)
      .catch((result) => {
        // DoSomething
      });
  }, [id]);

  return (
    <div>{info}</div>
  )
}
```

7. 다음과 같이 사용하지 않고 useRef를 써야만 하는 이유는 무엇인가요?

```jsx
let value = 0;

function Component() {
  const handleClick = () => {
    value += 1;
  }

  return (
    // ... 생략
  )
}
```

8. useContext가 상태 관리를 위한 API가 아닌 이유는 무엇인가요?
9. useEffect 대신에 useLayoutEffect를 대신 사용해야 하는 상황은 어떤 상황인가요?
10. 사용자 정의 훅과 고차 컴포넌트 중 무엇을 써야 할까요?

## 4장 서버 사이드 렌더링

1. SPA가 인기를 끌었던 이유는 무엇인가요?
2. 서버 사이드 렌더링이 다시 인기를 끌게된 이유는 무엇인가요?
3. 서버 사이드 렌더링의 장점과 단점에 대해서 설명해 주세요.
4. Next.js에서 페이지 이동 시에 a태그 대신 Link를 사용하고 window.location.push 대신에 router.push를 사용해야 하는 이유는 무엇인가요?

## 5장 리액트와 상태 관리 라이브러리

1. 상태 관리는 왜 필요할까요?
2. Flux패턴이란 무엇이고 왜 사용해야 할까요?
3. 지역 상태의 한계는 무엇일까요?
4. 어떤 기준으로 상태 관리 라이브러리를 고르는게 좋을까요?

## 6장 리액트 개발 도구로 디버깅하기

1. 컴포넌트를 기명 함수로 선언하는 것이 좋은 이유는 무엇인가요?
2. 만약 기명 함수를 사용할 수 없는 경우, 어떤 다른 방법이 있나요?
3. 리액트 개발 도구를 활용해서 무엇을 디버깅할 수 있나요? 또 작성한 리액트 애플리케이션에서 어떠한 정보를 파악할 수 있나요?
