# Breakout-Game-using-JS-Image-Processing
JS 기반의 영상처리를 활용한 벽돌깨기 게임   
   

## 🔥 프로젝트 개요
프론트엔드 프로그래밍을 공부하며 JS를 이용한 이미지 디지털 영상처리 알고리즘에 대해 집중적으로 학습했다.   
영상처리를 최대한 활용하려 했고, 재미있는 요소를 추가하고자 간단한 게임과 접목시켜 프로젝트를 진행했다.   
   

## 🛠 프로젝트 환경
✅ 사용 언어: HTML5 / CSS3 / JAVASCRIPT   
✅ 개발 환경: Visual Studio Code   
✅ 제작 기간: 21.03.25 – 21.03.30   
   
   
## 💻 화면 구성
(1) choose.html   
: 원하는 이미지 선택   
(2) edit.html   
: 선택한 이미지 편집   
(3) break.html   
: 편집한 이미지로 벽돌깨기 게임   
   

## 💎 구현 방법
✔ 이미지 선택하여 화면에 출력하기
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
✔ 세션 스토리지에 값 저장 및 가져오기
```Java Script
// 값 저장하기
function selectImage() {
   var imageNum = num;
   sessionStorage.setItem("imageNum", imageNum); // setItem(key, value)
}

// 값 가져오기
var imageNum2 = sessionStorage.getItem("imageNum"); // getItem(key)
```
✔ 이미지 영상처리 후 출력하기
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

