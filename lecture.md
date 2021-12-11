2강
npm i react react-dom typescript
npm i -D eslint prettier eslint-plugin-prettier eslint-config-prettier

.prettierrc
.eslintrc

tsconfig.json

esModuleInterop:true:
왼쪽을 오른쪽과 같이 쓸수 있게 함
import \* as React from 'react' => import React from 'react

.의 의미 => 리눅스에서 숨김파일이라는 뜻

pacakage-lock.json=>해당 패키지가 다른 패키지의 어떤 버전 정보를 정확히 참조하는지 확인 가능

babel
css/html/img파일을 js로 바꿀수 있다.

해당 프로잭트는
ts=>babel=>js로 변환하도록 구성
ts=>js로 바로 안 가는 이유? , babel이 img,css,html을 js로 바꿔서 쓰려고

3
webpack.config.ts => node런타임에서 실행(보통은 백엔드에서 실행)
style/css-loader -> css를 js파일로 변환해줌

npm i webpack @babel/core @babel-loader @babel/preset-env
@babel/preset-react -D

npm i -D @types/webpack @types/node @babel/preset-typescript

npm i -D style-loader css-loader

브라우저가 인식하는 최종파일은
html/css/js이다.
ts는 js로, scss/styled-components는 css로 결국 변환되야 브라우저가 인식가능

ts->webpack이 babel을 통해 js파일로 변환

결국 검색엔진이 서버에 들어와서 우리 페이지 검색시에는 index.html을 먼저 검색한다
따라서 성능관련해서 index.html이 중요한 역할을 한다
따라서 공통으로 쓰는 중요한 css는 index.html에 두고, 나머지 css를 다른 곳에

웹팩 실행 명령 =>npm i webpack후 npx webpack(global로 설치 안하고 사용시)

npm i ts-node

tsconfig-for-webpack-config.json
=> 웹팩이 webpack.config.ts를 인식하기 위해 필요한 파일
(공식문서 보고 확인)

scripts : {
build : "cross-env TS_NODE_PROJECT = \"tsconfig-for-webpack-config.json\" webpack"
}
실행=>npm rub build
cross-env 안 붙이면 리눅스 환경(맥)에서만 저게 실행되고, 윈도우에서는 에러뜸

4. hot reloading
   npm i webpack-dev-server -D (hot reloading + proxy server역할 : cors문제 해결해줌 + histroyApiFallback)
   npm i webpack-cli @types/webpack-dev-server

- 라이브러리 만들거 아니면 dependenciy / dev-dep

npm i @pmmmwh/react-refresh-webpack-plugin
npm i react-refresh
npm i fork-ts-checker-webpack-plugin
(ts컴파일과 webpack실행을 동시에 시키도록 하는 역할,
ts검사할때 보통은 blocking해서 실행됨-하나하고 웹팩실행시키는 방식)

외울 필요 없고, 한 번 해놓고 이거 계속 쓰면 된다

devServer : {
historyApiFallback : true // react router
port:3090, // Front server , BackendServer라면 3095로 규칙
publickPath :'/dist/'
}

scripts : {
dev : "cross-env TS_NODE_PROJECT = \"tsconfig-for-webpack-config.json\" webpack-server --env development "
}
//"cross-env TS_NODE_PROJECT = \"tsconfig-for-webpack-config.json\" => ts쓰려고 붙인 것
