5.  //pages - 서비스 페이지
    //components - 공통으로 쓰이는 녀석들
    //layouts - 페이지들간의 공통 레이아웃
    이렇게 일단 해놓았지만 폴더구조는 자유다.얽매이지 말자
    했던 알고리즘/패턴에 얽매이지 말자.보통 회사다니면서 시간 없으니 얽매이는 경우 많지만 따로 시간 내서라도 새로운 걸 해보자
    훅스되고 나서는 컨테이너 컴포넌트는 굳이 쓸 필요X

    1.폴더 먼저
    Login

- index.tsx
- styles.tsx
  SignUp
- index.tsx
- styles.tsx

라우터 설정
npm i react-router react-router-dom
npm i -D @types/react-router @types/react-router-dom

<Redirect exact to='/' path='/login'> : /로 이동시 login으로 보내버림
SPA에서 실제 서버가 인식하는 경로는 /밖에 없다(localhost:3000처럼)
따라서 localhost:3000/login을 쳐도 실제로는 localhost:3000이 서버에 인식되는 건데
localhost:3000/login처럼 가짜주소로 이동가능한 이유는 historyApi가 해줌
여기서는 devServer에 설정한 historyApiFallback : true enable this feature

Run:
npm run dev

6.Code Splitting

- Only import needed Components, not All Components for Fast Rendering
- 대상 : 필요한 페이지만 + 서버사이드 렌더링 필요없는 애들(텍스트 에디터 같은 애들)
  npm i @loadable/component @types/loadable\_\_component
- style : css in js (emotion or styled-components) => emotion is less complicated at configure more than styled-components
- css in js => 컴포넌트에 미리 css를 입혀놓는것 (html태그를 사용해서 정의해놓기에)
- npm i@ emotion-react ...etc
- styled-components사용시 componentes를 좀 더 큰 범위로 잡을수록 변수명 덜 써도 되기에 편하다

8.  리팩토링 / 커스텀 훅 => 코드를 다 완성하고 중복을 제거하거나 리팩토링이 낫다.실수할 수 있거나 구조가 변경될 수 있기에

useCallback안의 변수를 deps안에 넣어주기(안에서 쓰지만, useCallback밖에서 선언된 변수를 넣어줘야) -> useCallback이 함수를 캐싱하기에
함수형 컴포넌트에서 함수가 매번 생성되기에, 클래스 컴포넌트에서는 매번 재생성되지는 않는다

setPassWord같은 함수는 한 번 선언되고 더 이상 바뀌지 않으므로 deps에 넣어줄 필욘ㄴ

함수 매번 새로 생기면 리렌더링이 발생, 리렌더링 일어난다고 화면을 다시 그리는 건 아니다.
다만 버츄얼 돔 의해 계산과정을 거치고(화면이 이때 깜빡거림) 이 과정통해 변경된 거 없으면 화면 다시 그리지 않기에
렌더링 다시 일어난다고 성능많이 떨어지지는 않는다

10. customHook

ts가 인라인 콜백의 매개변수/변수/함수 리턴은 타입 추론을 잘함(타입 선언 안해도 알아서 유추)
함수의 매개변수는 타입추론을 잘 못하므로 타입 잘 써줘여
함수 매개변수에 제너릭을 잘 써보자
이거 코드 다시 보기
<T=any>=> give a default value to Generic
Use ts => 가독성 감소, 안정성 증가

11. thunk / saga => 컴포넌트에서 비동기 코드가 분리됨(컴포넌트에 비동기 로직이 안 남아있는 게 장점)
    프론트 서버 : webpack-dev-server (port:3090)
    백 서버 : 3095(port)
    => 둘이 포트 다르면 요청을 또 보냄(api한 번 호출에, 실제는 2번을 호출함)
    원래 주소 다르면 api호출 안됨(cors)
    - sol : attach Proxy through Webpack-dev-server or Saying to Backend

promise , try-catch + finally
error.response => 에러 관련 정보가 정확히 들어가 있다.

네트워크 탭 headers => 요소를 다 공부하자

네트워크 탭에서 비밀번호 보이는 것 문제 없나? https만 적용하면 해커에서 털릴 일 없다

proxy: {'/api/' : {target:'http://localhost:3095',changeOrigin:true}}

api.post('/api/users',data)
//3095(Front)가 3095에게 요청

api.post(http://localhost:3095/api/users,data)
// 3090(Front)이 3095에게 요청
// 요청과 응답이 서로 다른 origin일때 , cors + options발생

//error.response.data
