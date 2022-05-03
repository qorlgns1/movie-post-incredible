# [영화 포스터](https://qorlgns1.github.io/movie-post-incredible/) 만들어보기

## 피드백 기록

1. 기존에 영화 설명하는 쪽 폰트사이즈를 10px로 잡았는데 너무 작다. 다음에는 더 크게 해야한다.
2. width가 줄어들면 height도 줄어들 수 있도록 하려고 vw를 사용했는데 이것은 위험한 방법이라고 피드백 받았다.  
   다음에는 패딩탑으로 height를 주는 방법 또는 aspect-ratio 를 사용해서 height를 조절해보자.
3. Ratings를 보여줄 때 css class로 평점이 유동적으로 변경될 수 있어야 한다.

```html
<div class="star star_50">2.5점</div>
```

```css
/* 기존 코드 */
/* .star::before {
  content: "";
  inset: 0;
  position: absolute;
  width: 80%;
  background-image: url(../images/star.png);
  background-position: 0% 0%;
  background-repeat: no-repeat;
  background-size: cover;
}

.star::after {
  content: "";
  inset: 0;
  left: -57px;
  position: absolute;
  width: 80%;
  background-image: url(../images/star.png);
  background-position: 100% 100%;
  background-repeat: no-repeat;
  background-size: cover;
} */

/* 개선 코드 */

/* 현재 내가 만든 레이아웃이 너무 작아서 star 이미지 크기의 4/1로 width를 잡았다.
하지만 일반적으로 레티나 디스플레이를 지원하는경우 해상도를 2배로 잡고 이미지를 제작하는데
사용할 때는 1/2 크기의 width와 height가 필요하게된다.

나의 경우 .star의 height는 이미지 height의 1/8로 잡았다.
왜냐하면 별점이미지에서 반만 보여줘야하기 떄문에..!

사용자에게 접근성을 높이기 위해 html에 컨텐츠박스에 2.5점이 담겨있는데, 
.star::before가 들어오면서 컨텐츠박스에 담긴 텍스트를 밀어내게 된다.
이것을 overflow:hidden을 줘서 숨겨준다. 

기존 생각으로는 ir기법을 사용할 때 blind와 같은 클래스를 사용해서 텍스트를 날려주는 방법만 생각했는데(물론 컨텐츠박스 뿐만 아니라 다 날라가겠지만..) 이런식으로도 작업을 하니 새롭게 느껴졌다.

*/

.star {
  width: 120px;
  height: 24px;
  overflow: hidden;
}

.star::before {
  content: "";
  display: block;
  background-position: left bottom;
  width: 60%;
}

.star,
.star::before {
  background-image: url(../images/star.png);
  background-size: 120px 48px;
  height: 24px;
}

/* 이렇게 html에 클래스를 줘서 작업할 수 있도록 하는게 좋은 방법이다.
별점이 변경될 경우 css를 따로 건드리지 않아도 된다.
*/
.star_20::before {
  width: 20%;
}

.star_40::before {
  width: 40%;
}

.star_60::before {
  width: 60%;
}

.star_80::before {
  width: 80%;
}

.star_100::before {
  width: 100%;
}
```

4. Genre, Ratings, Cates 는 공통클래스로 레이웃을 잡고 각각의 새로운 클래스를 추가해서 각자 맞는 레이아웃을 잡아준다.

5. Cates에서 캐릭터 이미지가 있는데 hover됬을 때 크기를 크기 보이고 싶은 경우 scale을 사용하면 좋다.
   나중에 [CSS 팀소개 웹페이지](https://www.youtube.com/watch?v=rF0h1SA6zZw&ab_channel=%EB%B9%94%EC%BA%A0%ED%94%84CSS) 강의를 참고해보자
