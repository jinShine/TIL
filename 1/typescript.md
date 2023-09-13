# TypeScript



[TypeScript 공식문서](https://www.typescriptlang.org/ko/)



간단히 REPL을 쓰고 싶다면 ts-node를 실행하면 된다.

{% hint style="info" %}
**REPL**\
\
REPL은 Read-Eval-Print-Loop의 약자로 애플리케이션 실행 상태에서 사용자가 입력한 명령어(소스코드)를 읽고(Read) 명령어를 평가(Eval)하고 결과를 출력(Print)한 다음 다시 입력을 기다리는 상태로 돌아가는 과정을 반복(Loop)합니다.\
\
REPL은 주로 개발자들이 소스 코드 실행 결과를 빨리 확인해야 하는 경우 사용합니다.
{% endhint %}





**타입지정**

```typescript
let name: string;
let age: number;

name = '홍길동';
age = 13;

name = 13;
age = '홍길동';

let human: {
  name: string;
  age: number;
};

human = { name: '홍길동', age: 13 };
```

복잡한 오브젝트의 타입을 재사용하기 위해 타입을 정의할 수 있다.

* [타입 정의하기 (Defining Types)](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%A0%95%EC%9D%98%ED%95%98%EA%B8%B0-defining-types)

```typescript
type Human = {
  name: string;
  age: number;
};

let boy: Human;

boy = { name: '홍길동', age: 13 };

interface Person {
  name: string;
  age: number;
};

let girl: Person;

girl = { name: '홍길동', age: 13 };

function add(x: number, y: number): number {
  return x + y;
}

add(1, 2)

add('Hello', 'World')

function sub(x: number, y: number): string {
  return x - y;
}
```

* [타입 별칭과 인터페이스의 차이점](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%ED%83%80%EC%9E%85-%EB%B3%84%EC%B9%AD%EA%B3%BC-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

```typescript
// 인터페이스
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear()
bear.name
bear.honey

//////////////////////////////////////////////////

// 타입
type Animal = {
  name: string
}

type Bear = Animal & {
  honey: Boolean
}

const bear = getBear();
bear.name;
bear.honey;
```



**Union 타입**

유니언은 타입이 여러 타입 중 하나일 수 있음을 선언하는 방법

```typescript
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type OddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

매개 변수를 제한하거나 할 때 매우 유용하게 쓸 수 있다. Union으로 타입을 잡아주면 자동 완성이 매우 강력하다.

```typescript
type Category = 'food' | 'toy' | 'bag';

function fetchProducts({ category }: { category: Category }) {
  console.log(`Fetch ${category}`);
}
```

레거시 환경 또는 코드 때문에 안 쓸 수가 없다. ReactNode 같은 게 대표적이다.

* [React Types](https://github.com/facebook/react/blob/main/packages/shared/ReactTypes.js)

```tsx
let target: string | number;

target = '홍길동';
target = 13;
target = null;
target = undefined;

let targetName: string | undefined;
targetName = '홍길동';
targetName = undefined;
```



**배열 타입**

```typescript
let numbers: number[];
let counts: Array<number>;

numbers = [1, 2, 3];
```



**튜플 타입**

```typescript
let anythings: any[];
anythings = ['hp', 256];

let pair: [string, number];
pair = ['hp', 256];
```



[**타입 추론**](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes.html#%ED%83%80%EC%9E%85-%EC%B6%94%EB%A1%A0-types-by-inference)

JavaScript가 동작하는 방식을 이해함으로써 TypeScript는 JavaScript 코드를 받아들이면서 타입을 가지는 타입 시스템을 구축할 수 있습니다. 이는 코드에서 타입을 명시하기 위해 추가로 문자를 사용할 필요가 없는 타입 시스템을 제공합니다.

```tsx
const name: string = '홍길동';

const name = '홍길동';
```



[**옵셔널 파라미터**](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters)

함수 매개변수(parameters)에서 사용되곤 한다. 하지만 이보다는 물음표 기호(?)를 써서 [Optional Parameter](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters)로 처리하는 걸 추천한다.

```tsx
function greeting(name?: string): string {
  return `Hello, ${name || 'world'}`;
}
```

기본값을 잡아주면 더 좋다.

```tsx
function greeting(name: string = 'world'): string {
  return `Hello, ${name}`;
}
```

매개변수가 오브젝트일 때도 활용할 수 있다.

```tsx
function greeting({ name, age }: {
  name: string;
  age?: number;  
}): string {
  return age ? `${name} (${age})` : name;
}
```

→ 이렇게 쓰면 ts-node에선 아쉽게도 해석 불가하다.

아래처럼 한 줄로 붙여서 쓰거나, type 등으로 따로 잡아주면 된다.

```tsx
function greeting({ name, age }: { name: string; age?: number; }): string {
  return age ? `${name} (${age})` : name;
}
```

```tsx
type Human = {
  name: string;
  age?: number;
};

function greeting({ name, age }: Human): string {
  return age ? `${name} (${age})` : name;
}

greeting()

greeting({ name: '홍길동' })

greeting({ name: '홍길동', age: 13 })
```



### Intersection Type

* [교집합](https://www.typescriptlang.org/ko/docs/handbook/typescript-in-5-minutes-func.html#%EA%B5%90%EC%A7%91%ED%95%A9)

유니언과 더불어 TypeScript은 교집합까지 가지고 있습니다:

```
type Combined = { a: number } & { b: string };type Conflicting = { a: number } & { a: string };
```

`Combined` 은 마치 하나의 객체 리터럴 타입으로 작성된 것 처럼 `a` 와 `b` 두 개의 속성을 가지고 있습니다. 교집합과 유니언은 재귀적인 케이스에서 충돌을 일으켜서 `Conflicting.a: number & string` 입니다.



* [Intersection Types](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)

타입을 확장하는 간단한 방법.

```tsx
type Human = {
  name: string;
  age: number;
};

type Creature = {
  hp: number;
  mp: number;
};

type Person = Human & Creature;

let person: Person;

person = { name: '홍길동', age: 13, hp: 256, mp: 16 };
```



#### Generics, Utility Types

* [Generics](https://www.typescriptlang.org/docs/handbook/2/generics.html)
* [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)



{% hint style="info" %}
**더 알아보기**\
\
\
**공식문서**

* [https://www.typescriptlang.org/docs/handbook/intro.html](https://www.typescriptlang.org/docs/handbook/intro.html)

\
**더 좋은 타입스크립트 프로그래머로 만드는 11가지 팁**

* [https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer](https://velog.io/@lky5697/11-tips-that-help-you-become-a-better-typescript-programmer)
{% endhint %}

