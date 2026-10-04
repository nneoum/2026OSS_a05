# Assignment 2-3. Simple CRUD Service UI with JavaScript

## Deployment

Vercel URL:  
https://2026-oss-a05.vercel.app/js_dynamic.html
https://2026-oss-a05.vercel.app/crud.html
https://2026-oss-a05.vercel.app/


## Key Learning

1. JavaScript Array를 데이터 저장소처럼 사용하고, 배열을 바꾼 뒤 화면을 다시 그리는 구조를 익힘
2. push, find, filter로 Create / Update / Delete를 구현하는 방법
3. 입력값 검사(Validation)를 Create와 Update에 공통으로 적용하는 방법

## CRUD Service

- 주제: 도서 관리
- 필드: id, title, author, category, price, year
- Create: Add 버튼 클릭 시 validation 통과하면 books 배열에 push 후 화면 갱신
- Read: loading() 함수가 books 배열을 순회하며 li를 만들어 화면에 출력. 페이지 최초 실행, 추가, 수정, 삭제 후에 호출
- Update: 수정 버튼 클릭 시 입력창에 기존 값을 채우고 editId에 해당 id 저장. 저장 시 find로 해당 객체를 찾아 값을 덮어씀
- Delete: confirm으로 확인 후 filter로 해당 id를 제외한 배열을 books에 다시 대입

Validation: 필수 입력값 확인, 저자 2자 이상, 가격 1 이상 숫자, 연도 1900~2026 범위

## JavaScript

- querySelector(): 입력창과 버튼 요소 선택
- addEventListener(): 로드, 클릭 이벤트 등록
- createElement(), appendChild(): li, button 요소 생성 후 화면에 추가
- Array: push(), find(), filter(), forEach()
- loading(): 화면을 비우고 배열 내용을 다시 출력하는 함수

## AI / Search Usage

Tool - Claude

Purpose - Array의 find, filter가 콜백 함수를 받아 배열을 처음부터 끝까지 자동으로 순회한다는 점과 사용법을 이해하기 위해 사용

Used - filter로 삭제 대상 id만 제외한 새 배열을 만들고, find로 수정할 객체를 찾는 코드에 적용. 오류 원인(confirm 오타, textContent 오타 등) 확인에도 사용

What I Learned - filter는 콜백이 true를 반환한 요소만 모아 새 배열을 반환하고, find는 조건에 맞는 첫 번째 요소 자체를 반환함. 콜백의 매개변수(b)는 순회 중인 현재 요소이고, 바깥 forEach의 book은 삭제 버튼이 속한 항목이라는 점을 구분하게 됨

## Problem & Solution

- 문제: 삭제 버튼이 동작하지 않음 / 해결: confirm 함수명 오타였음
- 문제: 수정 버튼 클릭 시 값이 채워지지 않음 / 해결: 입력창이 아니라 book 객체에서 값을 가져와야 했음
- 문제: 수정 후 저장해도 항목이 중복 추가됨 / 해결: editId가 null인지 아닌지로 Create와 Update를 분기
- 문제: 수정 중에 항목 삭제 시 -> 신규 등록이 안되는 오류가 있었음 -> editId == book.id 이면 (수정중인거를 삭제하면) editId = null 로 초기화해서 신규등록할때 editId 가 수정모드가 아니라서 등록되게 됨

## Reflection
- 처음에는 li 를 통해서 화면에만 띄우는 방식으로 만들었다가 다시 array 로 바꾸느라 조금 복잡한 과정을 거쳤다. filter와 find 가 배열을 처음부터 자동으로 순회한다는 점이 forEach 와 작동박식이 같아서 쉽게 이해했다. 또한 editId 를 다루면서 관리했는데 서버를 이용해서 저장한다면 더 쉽지 않을까 하는 생각을 했다.