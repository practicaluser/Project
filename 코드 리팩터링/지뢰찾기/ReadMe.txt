개선점
시계, 깃발,지뢰 아이콘 추가
모든 칸에 입력하지 않을 시 생성 불가
지뢰 개수가 전체 칸에서 -4개를 넘어가지 않도록 조절
현재 깃발 개수를 화면에 출력
물음표 기능 삭제
게임 종료 시 자동으로 새로고침해서 새로 게임 시작하게 만듦

배운것 들

1 입력창에 값을 입력하지 않을 경우 탐지하기
-if (!rowValue || !cellValue || !mineValue)

2 오류
-함수 선언문과 함수 표현식의 차이를 이해하지 못해서 오류가 났다.
button.addEventListener("click", start);
const start = () => {
  console.log(rowa);
}
-함수 선언문은 스크립트의 맨 위로 호이스팅되어 실행 컨텍스트에 미리 등록되기 때문에 코드 어디에서든 접근할 수 있다. function 형태
-함수 표현식을 만들 때는 위치에 신경써야 한다.

3 입력 값에 따른 테이블 만들기 

4 지뢰찾기 표 만들기
-html에서 table>tbody
-script에서 const table = document.querySelector('#table');
const tbody = document.createElement('tbody'); table.appendChild(tbody);

5 input 평균 길이
-<input placeholder="가로 줄" id="row" size="5"/>

6 자바스크립트로 클릭시 타일 3*3 선택하기
const tile = e.target; 
const tileLeft = tile.previousSibling;  
const tileRight = tile.nextSibling; 
const tileParentRight = tile.parentNode.nextSibling;  
const tileParentLeft = tile.parentNode.previousSibling;

if (tileParentRight !== null) {
   const tileDown = tileParentRight.querySelector('.' + tileClass);
   const tileDownLeft = tileDown.previousSibling;
   const tileDownRight = tileDown.nextSibling;
}

if (tileParentLeft !== null) {
   const tileUp = tileParentLeft.querySelector('.' + tileClass);
   const tileUpLeft = tileUp.previousSibling;
   const tileUpRight = tileUp.nextSibling;
 }

7 Node와 Element의 차이 
https://hianna.tistory.com/711

8 화면에 특정 문자 출력하기
-innerHTML

9 오류해결
td.addEventListener('contextmenu',rightClick);

function rightClick(e) {
            e.preventDefault();
            const image = document.createElement('img');
            image.src = "깃발.png";
            image.classList.add("flag");
            td.appendChild(image);
}
-td is not defined 오류가 나온다.
-해결책  e.target.appendChild(image);

10 오른쪽 마우스 클릭시 깃발생성하고 한번 더 클릭 시 깃발이 사라지게 한다.
appendchild를 제거하고 추가하는 방식으로 구현하려고 했는데 잘 안됐다(해당 변수를 찾을 수 없다고 나옴)
innerHTML으로 내용을 붙였다 지웠다 하는 방식으로 구현, 칸 안에 있는 깃발을 오른쪽으로 클릭하면 깃발이 추가로 생성되서 오른쪽 클릭의 위치를 잘못 클릭하는 경우가 많아서, 위치를 변수를 만들어서 고정시켰다.


11 주의
tile.classList.add('opened'); O
tile.classList.add = 'opened'; X

12 승리조건
if (flagCount === 0 && mineFlaged == mineValue) {
                    alert('승리했습니다.');
}
mineValue가 '1'이런 문자열 형태여서 ===로 하면 안된다.

12-2 깃발을 모두 지뢰 자리에 꽂았을 때 승리하는 로직
function rightClick(e) {
            e.preventDefault();
            const element = e.target;
            const tdElement = element.closest('td'); 
            const existingFlags = tdElement.querySelectorAll('img.flag');
            const mineLocationElement = tdElement.querySelector('.mineLocation');
            if (flagCount > 0 && existingFlags.length === 0) {
                const flagImg = '<img src="깃발.png" class="flag">';   
                if (mineLocationElement) {
                    mineLocationElement.insertAdjacentHTML('beforeend', flagImg);
                    mineFlaged++;
                } else {
                    tdElement.innerHTML += flagImg;
                }      
                a.push(tdElement);
                flagCount--;
            } else if (a.includes(tdElement) && existingFlags.length === 1) {
                if (mineLocationElement) {
                    mineFlaged--;
                }
                existingFlags.forEach(flag => flag.remove());
                flagCount++;
            } 
            leftFlagNumber.innerHTML = `<img src="깃발.png" class="leftFlag">: ${flagCount}개`;

            if (flagCount === 0 && mineFlaged == mineValue) {
                setTimeout(() => {
                    alert('승리했습니다.');
                    document.location.reload();
                },500);
                
            }
          }

개발자도구 실행하는 도중에는 오른쪽 마우스를 금지해도 오른쪽 마우스가 실행된다.





















