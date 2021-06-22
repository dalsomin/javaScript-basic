문장의 끝은 세미콜론(;)을 생략하지 않는다.
문장 끝 세미콜론(;)을 생략하지 않는다. 세미콜론 생략하면 자바스크립트 구문분석기가 세미콜론을 자동으로 삽입해주는데 의도하지 않았던 코드(전혀 다른 코드)로 해석되어 예기치 못한 동작이 발생할 수 있다. 그리고 자바스크립트 구문분석기가 세미콜론의 위치를 계산하고 삽입하는데 추가 비용이 발생한다.

▶ 해결책
문장의 끝은 세미콜론을 사용한다.
변수와 함수는 선언 전에 사용하지 않는다 (ES5)
ES5 이하 버전에서 블록 구문을 사용하지만, 블록 유효범위를 제공하지 않는다. 블록 내에서 var 키워드를 사용해 변수를 선언되면, 선언된 위치에 상관없이 함수 스코프 내 어느 곳에서든 사용할 수 있다. var 키워드를 사용해 선언한 변수, function 키워드를 사용해 선언한 함수는 자바스크립트가 실행되고 컴파일될 때 호이스팅(끌어올림)이 되기 때문이다. 이로 인해 코드 가독성이 떨어지며 오류를 찾기 힘들다.

▶ 해결책
함수는 사용하기 전에 선언하고, 변수는 var 키워드와 함께 상단에 선언한다.
// Bad
doSomething();

function doSomething() {
  foo1 = foo2;
  ...
  var foo1 = 'value1';
  foo3 = foo4;
  ...
  var foo3;
  ...
  var foo4 = 'value4';
  var foo2;
}

// Good
function doSomething() {
  var foo1 = 'value1';
  var foo4 = 'value4';
  var foo3 = foo4;
  var foo2;
  ...
  foo1 = foo2;
}

doSomething();
배열 순회 시 매번 array.length속성을 참조하지 않는다 (Legacy)
for문은 주어진 조건 표현식이 true로 평가되는 동안 실행을 반복한다. 매 순회 시 조건 표현식을 다시 평가한다. 100번의 순회가 있었다면 100번의 평가가 수행된다. for문에서 반복 횟수만큼 매번 array.length속성을 참조하는 것은 비효율적이다. (최신 브라우저에서는 array.length를 캐시하지 않아도 성능에 큰 차이가 없지만 IE10 이하의 구형 브라우저에서는 성능 차이가 크다.)

▶ 해결책
IE10 이하의 구형 브라우저에서 for문 사용 시 배열 길이는 캐시하여 사용한다.
// Bad
for (var i = 0; i < array.length; i += 1) {
  ...
}

// Good
var len = array.length;

for (var i = 0; i < len; i += 1) {
  ...
}