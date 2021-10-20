## 이미지 영상처리를 활용한 벽돌깨기 게임
<br>

**사용언어**
https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=HTML5&logoColor=white
https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=CSS3&logoColor=white
https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=JavaScript&logoColor=white

**개발환경**
https://img.shields.io/badge/VisualStudioCode-007ACC?style=flat&logo=VisualStudioCode&logoColor=white

**개발기간**  21.03.25 - 21.03.30 
<br>

ㄴhome.html   
ㄴchoose.html   
ㄴedit.html   
ㄴimages   
    ㄴimagefiles.png   
(ㄴmyImage.png)   
<br>


사용시 변경할 부분
<br>

#### home.html

- 이미지 (line 181-187)   
img src="directory/file"

- 링크 (line 191-196)   
a href="link"

#### choose.html

- 이미지 이름 (line 222)   
inImage.src = "directory/file" + num + ".png"; // ".jpg"   
num: 1부터 차례대로 매김   
size: 이후 벽돌깨기 게임을 위해 512*512 사이즈로 설정하는 것이 좋음

- 이미지 개수 (line 236)   
max = 개수

#### edit.html
- 선택한 이미지 이름 (line 720)
inImage.src = "directory/file" + num + ".png"; // ".jpg" 

- 이미지 저장 (line 1618)   
imageName: 다운로드되는 이미지의 이름
(브라우저 다운로드 디렉토리 경로를 소스파일과 같은 위치로 설정)


#### break.html
- 다운로드한 이미지 이름 (line 155)   
edit.html 에서 다운로드한 이미지 이름과 동일해야 함
