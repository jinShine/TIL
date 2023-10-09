# ESLint

### Parcel

{% hint style="info" %}
[Parcel 공식문서](https://parceljs.org/)
{% endhint %}

Parcel은 새 프로젝트 시작부터 반복 작업과 디버깅, 프로덕션 배포까지 모든 개발 과정을 간편하게 시작할 수 있다. 더 이상 설정에 신경 쓰거나 모범 사례를 따라잡기 위해 시간을 낭비할 필요 없이 바로 작동한다!

개발 경험에서 차이를 느낄 수 있는 웹 애플리케이션 번들러다.

**Zero Configuration**

* 특별한 설정 없이 바로 사용 가능한 빌드 도구. 내부적으로 SWC를 사용해 기존 도구보다 빠르다(ES Module을 적극 활용하는 Vite도 엄청나게 빠름).
* 참고:
  * [https://github.com/ahastudio/til/tree/main/parcel](https://github.com/ahastudio/til/tree/main/parcel)
  * [https://github.com/ahastudio/til/tree/main/vite](https://github.com/ahastudio/til/tree/main/vite)

설정이 필요 없다고 했지만, 다음 두가지 작업은 하는 게 좋다.

`package.json` 파일에 source 속성 추가.

```json
"source": "./index.html",
```

[parcel-reporter-static-files-copy](https://github.com/elwin013/parcel-reporter-static-files-copy) 패키지 설치 후 `.parcelrc` 파일 작성.\
이렇게 하면 static 폴더의 파일을 정적 파일로 Serving할 수 있다(이미지 등 Assets).

```json
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

빌드 + 정적 서버 실행

```bash
npx parcel build

npx servor ./dist
```

* [servor](https://github.com/lukejacksonn/servor)

### ESLint

{% hint style="info" %}
[**ESLint 공식문서**](https://eslint.org/)

* [린트](https://ko.wikipedia.org/wiki/%EB%A6%B0%ED%8A%B8\_\(%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4\))
* [정적 프로그램 분석](https://ko.wikipedia.org/wiki/%EC%A0%95%EC%A0%81\_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8\_%EB%B6%84%EC%84%9D)
* [Coding\_conventions](https://en.wikipedia.org/wiki/Coding\_conventions)
{% endhint %}

무엇을 위해서?

* 스타일 통일
* 베스트 프랙티스 추천 → 최신 트렌드를 학습하는데 활용할 수 있다.

[VS Code ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

`.vscode/settings.json`파일을 추가해 JS/TS 파일을 저장할 때마다 ESLint를 실행하고 문제점을 고치게 설정할 수 있다.

```json
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```

아샬이 쓰는 VS Code 기본 세팅:

* [VS Code 기본 세팅](https://github.com/ahastudio/CodingLife/blob/main/20211008/react/.vscode/settings.json)
* [Trailing Spaces](https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces)
