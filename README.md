# Breakout-Game-using-JS-Image-Processing
### JS 기반의 영상처리를 활용한 벽돌깨기 게임   
입니다.
<br>
<hr>

## 🔥 프로젝트 개요
프론트엔드 프로그래밍을 공부하며 JS를 이용한 이미지 디지털 영상처리 알고리즘에 대해 집중적으로 학습했다.   
영상처리를 최대한 활용하려 했고, 재미있는 요소를 추가하고자 간단한 게임과 접목시켜 프로젝트를 진행했다.   
<br>
   
## 🛠 프로젝트 환경
✅ **사용 언어**: HTML5 / CSS3 / JAVASCRIPT   
✅ **개발 환경**: Visual Studio Code   
✅ **개발 기간**: 21.03.25 – 21.03.30   
<br>
   
## 💻 화면 구성
💨 **home.html**   
<br>
<img src="https://user-images.githubusercontent.com/84164109/118426167-ae2f7f80-b705-11eb-9f91-974667186695.png">
<br><br>
💨 **choose.html**: 원하는 이미지 선택   
<br>
<img src="https://user-images.githubusercontent.com/84164109/118426218-c7d0c700-b705-11eb-87c2-d257413b21d6.png">
<br><br>
💨 **edit.html**: 선택한 이미지 편집   
<br>
<img src="https://user-images.githubusercontent.com/84164109/118427418-18492400-b708-11eb-91a1-e6fa9e43624f.png">
<br><br>
💨 **break.html**: 편집한 이미지로 벽돌깨기 게임   
<br>
<img src="https://user-images.githubusercontent.com/84164109/118426229-ce5f3e80-b705-11eb-939e-8204a09ed7bd.png">
<br><br>
   
## 🎬 시연 영상
> https://youtu.be/gYLwj4hH6UE
<br>
<img src="https://user-images.githubusercontent.com/84164109/118427766-f13f2200-b708-11eb-8231-909582527b29.png">
<br>

## 💦 보완할 점
영상처리 알고리즘 관련 함수들 정리하기   
마우스 이벤트 등등   
함께 올린 html 파일보고 공부!!   
<br>
   
## 📋 참고 자료
2D breakout game using pure JavaScript   
> https://developer.mozilla.org/ko/docs/Games/Tutorials/2D_Breakout_game_pure_JavaScript   
<br>
   
## 🍺 일기장
> https://mygummy2.tistory.com/36
<br>
   
## 💎 중요 코드
✔ **이미지 선택하여 화면에 출력하기**
```Java Script

var inCanvas, inCtx; // 캔버스 관련 변수
var inFile; // 입력 파일 관련 변수

function drawImage() {
  // 캔버스 생성
  inCanvas = document.getElementById('inCanvas');
  inCtx = inCanvas.getContext('2d');

  // 이미지 지정되어 있는 경우
  var inImage = new Image(); // 빈 이미지 객체 생성
  inImage.src = ""; // 지정된 이미지 파일 이름
  
  // 이미지 파일 선택하는 경우
  inFile = document.getElementById('selectFile').files[0]; // 이미지 파일 선택
  var inImage = new Image(); // 빈 이미지 객체 생성
  inImage.src = inFile.name; // 이미지 파일 이름 가져오기

  // 캔버스에 이미지 띄우기
  inImage.onload = function() {
      // 캔버스 크기를 이미지 파일 크기로 설정
      inCanvas.width = inImage.width;
      inCanvas.height = inImage.height;
      // 이미지 띄우기
      inCtx.drawImage(inImage, 0, 0, inCanvas.width, inCanvas.height);
  }
}
```
✔ **세션 스토리지에 값 저장 및 가져오기**
```Java Script
// 값 저장하기
function selectImage() {
   var imageNum = num;
   sessionStorage.setItem("imageNum", imageNum); // setItem(key, value)
}

// 값 가져오기
var imageNum2 = sessionStorage.getItem("imageNum"); // getItem(key)
```
✔ **이미지 영상처리 후 출력하기**
```Java Script
var outCanvas, outCtx; // 캔버스 관련 변수
var inPaper, outPaper; // 캔버스에 픽셀값 출력할 종이
var inImageArray, outImageArray; // 픽셀값 저장할 배열
var inWidth, inHeight, outWidth, outHeight;
inWidth = outWidth = inCanvas.width;
inHeight = outHeight = inCanvas.height;

// 입,출력 3차원 배열
inImageArray = outImageArray = new Array(3);
for(var j=0; j<3; j++) {
   inImageArray[j] = new Array(inHeight);
   outImageArray[j] = new Array(outHeight);
   for(var i=0; i<inHeight; i++) {
      inImageArray[j][i] = new Array(inHeight);
      outImageArray[j][i] = new Array(outHeight);
   }
}

// 이미지가 띄워진 캔버스에서 픽셀값 가져와 입력 배열에 저장
var imageData = inCtx.getImageData(0,0,inWidth,inHeight);
var R, G, B, A;
for(var i=0; i<inHeight; i++) {
   for (var k=0; k<inWidth; k++) {
      pixel = (i*inWidth + k)*4; // 1픽셀 = 4byte
      R = imageData.data[pixel + 0];
      G = imageData.data[pixel + 1];
      B = imageData.data[pixel + 2];
      // A = imageData.data[pixel + 3];
      inImageArray[0][i][k] = String.fromCharCode(R);
      inImageArray[1][i][k] = String.fromCharCode(G);
      inImageArray[2][i][k] = String.fromCharCode(B);
   }
}

// 영상처리 알고리즘을 사용해 픽셀값 변경 후 출력 배열에 저장
for(var i=0; i<inHeight; i++) {
   for (var k=0; k<inWidth; k++) {
   // 픽셀값 문자 -> 숫자
   R = inImageArray[0][i][k].charCodeAt(0);
   G = inImageArray[1][i][k].charCodeAt(0);
   B = inImageArray[2][i][k].charCodeAt(0);
   
   // ** 여러가지 영상처리 적용 **
   
   // 픽셀값 숫자 -> 문자
   outImageArray[0][i][k] = String.fromCharCode(R);
   outImageArray[1][i][k] = String.fromCharCode(G);
   outImageArray[2][i][k] = String.fromCharCode(B);
   }
}

// 픽셀값 출력할 종이 생성
outPaper = outCtx.createImageData(outWidth, outHeight);
// 종이에 픽셀값 출력
for(var i=0; i<outHeight; i++) {
   for(var k=0; k<outWidth; k++) {
      R = outImageArray[0][i][k].charCodeAt(0);
      G = outImageArray[1][i][k].charCodeAt(0);
      B = outImageArray[2][i][k].charCodeAt(0);
      outPaper.data[(i*outWidth + k) * 4 + 0] = R;
      outPaper.data[(i*outWidth + k) * 4 + 1] = G;
      outPaper.data[(i*outWidth + k) * 4 + 2] = B;
      outPaper.data[(i*outWidth + k) * 4 + 3] = 255;
   }
}
// 출력 캔버스에 종이 붙이기
outCtx.putImageData(outPaper, 0, 0);
```
✔ **이미지 영상처리 후 출력하기**
```Java Script
// ** 벽돌 관련 변수 **
// 벽돌 개수
var brickRowCount = 8;
var brickColumnCount = 16;
// 벽돌 크기
var brickWidth = inWidth/brickRowCount; // 64px
var brickHeight = inHeight/brickColumnCount; // 32px
// 벽돌 사이 패딩
var brickPadding = 0;

// 벽돌 배열 생성
var bricks = [];
for(var c=0; c<brickColumnCount; c++) {
   bricks[c] = [];
   for(var r=0; r<brickRowCount; r++) {
      // 벽돌을 그릴 위치와 상태
      bricks[c][r] = { x: 0, y: 0, status: 1 };
   }
}

// 이미지 출력 배열 생성 후 픽셀값 저장하여 출력하기
m = brickColumnCount;
n = brickRowCount;

function makeOutArray(m, n) {
   outWidth = brickWidth;
   outHeight = brickHeight;

   // 출력 3차원 배열을 준비
   outImageArray = new Array(3);
   for(var j=0; j<3; j++) {
      outImageArray[j] = new Array(outHeight);
      for(var i=0; i<outHeight; i++) 
        outImageArray[j][i] = new Array(outWidth);
   }

   // 출력 배열에 픽셀값 저장
   for(var j=0; j<3; j++) {
      for(var i=0; i<outHeight; i++) 
        for (var k=0; k<outWidth; k++) 
            outImageArray[j][i][k] = inImageArray[j][outHeight*m+i][outWidth*n+k];
   }

   // 이미지 출력
   outPaper = ctx.createImageData(outWidth, outHeight);
   var R, G, B, A;
   for(var i=0; i<outHeight; i++) {
      for (var k=0; k<outWidth; k++) {
        R = outImageArray[0][i][k].charCodeAt(0);
        G = outImageArray[1][i][k].charCodeAt(0);
        B = outImageArray[2][i][k].charCodeAt(0);
        outPaper.data[(i*outWidth + k) * 4 + 0] = R;
        outPaper.data[(i*outWidth + k) * 4 + 1] = G;
        outPaper.data[(i*outWidth + k) * 4 + 2] = B;
        outPaper.data[(i*outWidth + k) * 4 + 3] = 255;
      }
   }
}

// 벽돌 위치에 맞게 이미지 출력하기
function drawBricks() {
   for(var c=0; c<brickColumnCount; c++) {
      for(var r=0; r<brickRowCount; r++) {
        // 상태: 1 그려짐
        if(bricks[c][r].status == 1) {
            // 벽돌 그릴 위치 조정
            var brickX = (r*(brickWidth+brickPadding))+brickOffsetLeft;
            var brickY = (c*(brickHeight+brickPadding))+brickOffsetTop;
            // 벽돌 그릴 위치를 배열에 저장
            bricks[c][r].x = brickX;
            bricks[c][r].y = brickY;
            // 이미지 출력
            makeOutArray(c, r);
            ctx.putImageData(outPaper,brickX,brickY);
        }
      }
   }
}
```
