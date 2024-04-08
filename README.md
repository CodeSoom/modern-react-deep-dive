# 모던 리액트 딥 다이브 문제 모음

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

