- - - 
## Closure와 Event Handling
- Closure는 함수처럼 호출할 수 있는 객체
	- 주변의 변수를 캡쳐할 수 있으며 js의 클로저와 유사
	- Fn, FnMut, FnOnce 트레이트로 정의됨

## FnMut 트레이트
- 클로저가 내부 상태를 변경할 수 있음을 나타냄
- 즉, 클로저가 호출될 때 내부적으로 변경 가능한 상태를 가질 수 있음

## Closure 생성
```rust
// wasm-bindgen에서 js 이벤트 리스너와 같은 콜백을 설정할 때 사용되는 패턴
// 이 구문을 통해 Rust 클로저를 js 함수로 변환할 수 있음
Closure::<dyn FnMut()>::new(move || { ... })
```
- Closure::<dyn FnMut()>::new
	- Closure 타입은 Rust 클로저를 js의 콜백 함수로 변환
	- ::<dyn FnMut()>는 클로저가 FnMut 트레이트를 구현해야 한다는 것을 지정
	- FnMut()는 매개변수가 없고 반환값도 없는 클로저를 의미
- move || { ... }
	- move 키워드는 클로저가 사용하는 모든 변수를 클로저의 소유권으로 이동시킴
	- 이는 클로저가 원래의 스코프 밖에서 호출되더라도 변수들이 유효하게 유지되도록 함
	- || {...} 은 매개변수가 없고 반환값도 없는 클로저를 의미
	- || 는 클로저의 파라미터 목록을 나타냄
		- ~::new(move |event: MessageEvent| {...} )