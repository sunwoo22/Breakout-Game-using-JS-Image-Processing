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
✔ 화면에 이미지 띄우기
```Java Script
// 캔버스 관련 변수
var inCanvas, inCtx;
// 입력 파일 관련 변수
var inFile;

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



