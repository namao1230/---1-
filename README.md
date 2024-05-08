# 그래픽스 팀프로젝트 (1조)
------------------
조장 : 신현진 20210817

조원1 : 김종준 20171111

조원2 : 안현수 20210818

조원3 : 홍재영 20230970

--------------------
# 사용법 :

![처음화면](https://github.com/namao1230/-1-/assets/153504478/75a63b4b-4e5b-4456-873f-30e87222f1cd)
먼저 처음 실행을 하면 조원들 소개 가 있습니다 옆에 화살표를 누르시면 조원들의 모습과 소개가 나옵니다. 밑에는 버튼들이 있고 누르면 다른 페이지로 이동합니다.

![웹캠](https://github.com/namao1230/-1-/assets/153504478/22d7d415-1ec1-4406-9ca3-700d8c27deb2)
웹캠속 찾기를 누르시면 이러한 화면이 나오며 왼쪽상단위에 카메라 사용여부를 물어봅니다. 허용누르시면 웹캠이나오면서 얼굴에 트래킹이되게됩니다.

![이미지 삽입](https://github.com/namao1230/-1-/assets/153504478/d5b96927-2676-4f63-80ed-25fbbfb61e86)

사진속 인물찾아보기 누르시면 위와 같은 화면이 나오고 파일을 삽입하여 찾아보기를 누르면 트래킹된 화면과 누가 누구인지 옆에 적혀서 나오게 됩니다. 그리고 맞으면 맞다 아니면 아니다를 누르시면 됩니다.

![맞다](https://github.com/namao1230/-1-/assets/153504478/179e3f1a-e40c-4b91-8581-e3dd3314f798)
맞다를 누르시면 이사진이 나오면서 그렇게 끝입니다.

![아니다](https://github.com/namao1230/-1-/assets/153504478/b2001efc-1681-4db4-ae1d-eac8ab9cb22e)
아니다를 누르시면 이 동영상이나오며 끝이나게 됩니다.



------------------

# 파일마다 설명



# Design : 

버튼의 이미지를 저장한 폴더입니다.

# img : 

슬라이더의 화살표 등의 이미지를 저장한 폴더입니다.


# labeled_images : 

업로드한 사진에서 누구인지 찾기위해 저장해둔 사람들의 사진


# models : 

face-api 를 사용하기위한 model을 저장한 폴더


# test_images : 

업로드할 test 이미지를 저장해둔 폴더


# face-api.min.js, face-api.min1.js :

face-api 를 사용하기위한 min.js 파일


# index(No).html, index(Web).html, index(Yes).html, index.html, index2.html :

각각의 파일들은 버튼을 눌렀을때 이동하는 html을 구현해 놓은 것이고 각각 설명을 붙이자면

index.html : 초기화면 조원들의 설명이 있습니다.

index(Web).html: 웹테스트를 누르면 들어가지는 html 이고 웹캠을 통하여 얼굴이 트래킹 됩니다.

index2.html : 초기화면에서 누구인지 찾으러가는 버튼을 누르면 나오는 html로 안에 이미지를 삽입하면 각 얼굴이 누구인지 트래킹 되어서 나오게 됩니다. 

index(No).html : index2.html에서 아니요를 누르면 나오는 html로 동영상이 실행됩니다.

index(Yes).html : index2.html에서 맞아!를 누르면 나오는 html로 사진이 나오면서 끝입니다.

script.js : index.html의 세부설정을 작성해놓은 js 파일입니다.

script1.js : index2.html의 세부설정을 작성해놓은 js 파일입니다.

-----------------------
//index.html

    <!DOCTYPE html>
    <html lang="en">
    <head>
    <!-- Google Fonts를 가져오기 위한 preconnect 링크 -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <!-- 사용할 폰트 설정 -->
    <link href="https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap" rel="stylesheet">
    <!-- 문서 인코딩 및 뷰포트 설정 -->
    <meta charset='utf-8'>
    <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no">
    <!-- 문서 제목 설정 -->
    <title>조슈아 탐정사무소</title>
    <style>
        /* Google Fonts에서 Moirai One 폰트를 가져와서 사용합니다. */
        @import url('https://fonts.googleapis.com/css2?family=Moirai+One&display=swap');
    
        /* 모든 요소의 margin과 padding을 0으로 설정합니다. */
        * {margin:0;padding:0;}
    
        /* 섹션 요소에 스타일을 적용합니다. */
        .section {}
    
        /* slide로 시작하는 id를 가진 input 요소들을 숨깁니다. */
        .section input[id*="slide"] {display:none;}
    
        /* 슬라이드를 감싸는 요소에 스타일을 적용합니다. */
        .section .slide-wrap {max-width:1200px;margin:0 auto;}
    
        /* 슬라이드 목록에 스타일을 적용합니다. */
        .section .slidelist {white-space:nowrap;font-size:0;overflow:hidden;}
    
        /* 슬라이드 목록 내의 각 li 요소에 스타일을 적용합니다. */
        .section .slidelist > li {display:inline-block;vertical-align:middle;width:100%;transition:all .5s;}
    
        /* 슬라이드 목록 내의 a 태그에 스타일을 적용합니다. */
        .section .slidelist > li > a {display:block;position:relative;}
    
        /* 슬라이드 이미지에 스타일을 적용합니다. */
        .section .slidelist > li > a img {width:100%;}
    
        /* 슬라이드 컨트롤 라벨에 스타일을 적용합니다. */
        .section .slidelist label {position:absolute;z-index:10;top:50%;transform:translateY(-50%);padding:50px;cursor:pointer;}
    
        /* 왼쪽 화살표에 스타일을 적용합니다. */
        .section .slidelist .left {left:30px;background:url('./img/left.png') center center / 100% no-repeat;}
    
        /* 오른쪽 화살표에 스타일을 적용합니다. */
        .section .slidelist .right {right:30px;background:url('./img/right.png') center center / 100% no-repeat;}
    
        /* 슬라이드 텍스트 상자에 스타일을 적용합니다. */
        .section .slidelist .textbox {
            position:absolute;
            z-index:1;
            top:5%;
            left:60%;
            transform:translate(-50%,-50%);
            line-height:1.6;
            text-align:center;
            font-family: 'Do Hyeon', sans-serif; /* Do Hyeon 폰트를 사용합니다. */
        }
    
        /* 슬라이드 텍스트 h3에 스타일을 적용합니다. */
        .section .slidelist .textbox h3 {
            font-size:60px;
            color: #000;
            opacity:0;
            transform:translateY(30px);
            transition:all .5s;
        }
    
        /* 슬라이드 텍스트 p에 스타일을 적용합니다. */
        .section .slidelist .textbox p {
            font-size:40px;
            color:#000;
            opacity:5; /* 투명도를 5%로 설정합니다. */
            transform:translateY(30px);
            transition:all .5s;
        }
     /* 슬라이드 전환 애니메이션 설정 */
        .section input[id="slide01"]:checked ~ .slide-wrap .slidelist > li {transform:translateX(0%);}
        .section input[id="slide02"]:checked ~ .slide-wrap .slidelist > li {transform:translateX(-100%);}
        .section input[id="slide03"]:checked ~ .slide-wrap .slidelist > li {transform:translateX(-200%);}
        .section input[id="slide04"]:checked ~ .slide-wrap .slidelist > li {transform:translateX(-300%);}
    
        /* 각 슬라이드의 텍스트 페이드 인 설정 */
        .section input[id="slide01"]:checked ~ .slide-wrap li:nth-child(1) .textbox h3 {opacity:1;transform:translateY(0);transition-delay:.2s;}
        .section input[id="slide01"]:checked ~ .slide-wrap li:nth-child(1) .textbox p {opacity:1;transform:translateY(0);transition-delay:.4s;}
        .section input[id="slide02"]:checked ~ .slide-wrap li:nth-child(2) .textbox h3 {opacity:1;transform:translateY(0);transition-delay:.2s;}
        .section input[id="slide02"]:checked ~ .slide-wrap li:nth-child(2) .textbox p {opacity:1;transform:translateY(0);transition-delay:.4s;}
        .section input[id="slide03"]:checked ~ .slide-wrap li:nth-child(3) .textbox h3 {opacity:1;transform:translateY(0);transition-delay:.2s;}
        .section input[id="slide03"]:checked ~ .slide-wrap li:nth-child(3) .textbox p {opacity:1;transform:translateY(0);transition-delay:.4s;}
        .section input[id="slide04"]:checked ~ .slide-wrap li:nth-child(4) .textbox h3 {opacity:1;transform:translateY(0);transition-delay:.2s;}
        .section input[id="slide04"]:checked ~ .slide-wrap li:nth-child(4) .textbox p {opacity:1;transform:translateY(0);transition-delay:.4s;}
    
        /* 페이지의 배경 스타일 설정 */
        body {
            background: radial-gradient(circle at center, #ffffff 20%, #ffffff00 70%), radial-gradient(circle at center, #ffae00 20%, #ffffff00 70%);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    
        /* 버튼 공통 스타일 설정 */
        .btn, .btn1 {
            width: 340px;
            height: 73px;
            background-size: cover;
            background-repeat: no-repeat;
            padding: 0;
            border: none;
            cursor: pointer;
            transition: all 0.4s;
            position: fixed;
            transform: translateX(-50%);
        }
    
        /* 버튼 포커스 스타일 설정 */
        .btn:focus, .btn1:focus {
            outline: none;
        }
    
        /* 첫 번째 버튼 호버 및 클릭 스타일 설정 */
        .btn:hover, .btn1:hover {
            width: 340px;
            height: 73px;
            cursor: pointer;
            transition: all 0.4s;
            position: fixed;
            transform: translateX(-50%);
        }
    
        /* 첫 번째 버튼 위치 및 이미지 설정 */
        .btn {
            background-image: url('Design/photo1.png');
            bottom: 50px;
            left: 30%;
            transform: translateX(-50%);
        }
    
        /* 두 번째 버튼 포지션 설정 */
        .btn1 {
            background-image: url('Design/cam1.png');
            bottom: 50px;
            left: 70%;
            transform: translateX(-50%);
        }
        
        /* 배경 이미지 스타일 설정 */
        .background-image {
            position: absolute;
            top: 70px;
            left: 100px;
            width: 14.5%;
            height: 31.8%;
            object-fit: cover;
            z-index: -1;
        }
    </style>
    </head>
    <body>
    <!-- 섹션 내에 슬라이드를 표시하는 부분 -->
    <div class="section">
        <!-- 슬라이드 선택을 위한 라디오 버튼 -->
        <input type="radio" name="slide" id="slide01" checked>
        <input type="radio" name="slide" id="slide02">
        <input type="radio" name="slide" id="slide03">
        <input type="radio" name="slide" id="slide04">
        <!-- 슬라이드를 감싸는 부분 -->
        <div class="slide-wrap">
            <!-- 슬라이드 목록 -->
            <ul class="slidelist">
                <!-- 첫 번째 슬라이드 -->
                <li>
                    <!-- 슬라이드 내용과 이미지를 포함하는 링크 -->
                    <a>
                        <!-- 슬라이드 좌측 이동 버튼 레이블 -->
                        <label for="slide04" class="left"></label>
                        <!-- 슬라이드 텍스트 및 정보 -->
                        <div class="textbox">
                            <h3>신현진 명탐정</h3>
                            <p>탐정 신현진 20210817</p>
                        </div>
                        <!-- 슬라이드 이미지 -->
                        <img src="https://raw.githubusercontent.com/namao1230/-/master/%EC%8B%A0%ED%98%84%EC%A7%84%20%EC%BF%A0%ED%82%A4.png" alt="Slide 1">
                        <!-- 슬라이드 우측 이동 버튼 레이블 -->
                        <label for="slide02" class="right"></label>
                    </a>
                </li>
                <!-- 두 번째 슬라이드 -->
                <li>
                    <!-- 슬라이드 내용과 이미지를 포함하는 링크 -->
                    <a>
                        <!-- 슬라이드 좌측 이동 버튼 레이블 -->
                        <label for="slide01" class="left"></label>
                        <!-- 슬라이드 텍스트 및 정보 -->
                        <div class="textbox">
                            <h3>김종준 명탐정 조슈</h3>
                            <p>조수 김종준 20171111</p>
                        </div>
                        <!-- 슬라이드 이미지 -->
                        <img src="https://raw.githubusercontent.com/namao1230/-/master/%EA%B9%80%EC%A2%85%EC%A4%80%20%EC%BF%A0%ED%82%A4.png" alt="Slide 2" style="width: 750px; height: 900;">
                        <!-- 슬라이드 우측 이동 버튼 레이블 -->
                        <label for="slide03" class="right"></label>
                    </a>
                </li>
                <!-- 세 번째 슬라이드 -->
                <li>
                    <!-- 슬라이드 내용과 이미지를 포함하는 링크 -->
                    <a>
                        <!-- 슬라이드 좌측 이동 버튼 레이블 -->
                        <label for="slide02" class="left"></label>
                        <!-- 슬라이드 텍스트 및 정보 -->
                        <div class="textbox">
                            <h3>안현수 정답을 말해줘</h3>
                            <p>비서 안현수 20210818</p>
                        </div>
                        <!-- 슬라이드 이미지 -->
                        <img src="https://raw.githubusercontent.com/namao1230/-/master/%EC%95%88%ED%98%84%EC%88%98%20%EC%BF%A0%ED%82%A4.png" alt="Slide 3" style="width: 750px; height: 900;">
                        <!-- 슬라이드 우측 이동 버튼 레이블 -->
                        <label for="slide04" class="right"></label>
                    </a>
                </li>
                <!-- 네 번째 슬라이드 -->
                <li>
                    <!-- 슬라이드 내용과 이미지를 포함하는 링크 -->
                    <a>
                        <!-- 슬라이드 좌측 이동 버튼 레이블 -->
                        <label for="slide03" class="left"></label>
                        <!-- 슬라이드 텍스트 및 정보 -->
                        <div class="textbox">
                            <h3>널보면 재채기가 나올것같아</h3>
                            <p>괴도 홍재영 20230970</p>
                        </div>
                        <!-- 슬라이드 이미지 -->
                        <img src="https://raw.githubusercontent.com/namao1230/-/master/%ED%99%8D%EC%9E%AC%EC%98%81%20%EC%BF%A0%ED%82%A4.png" alt="Slide 4" style="width: 800px; height: 1100;">
                        <!-- 슬라이드 우측 이동 버튼 레이블 -->
                        <label for="slide01" class="right"></label>
                    </a>
                </li>
            </ul>
        </div>
    </div>
    
    <!-- 배경 이미지 -->
    <img src="https://raw.githubusercontent.com/namao1230/-/master/%ED%83%90%EC%A0%95%EC%82%AC%EB%AC%B4%EC%86%8C.png" alt="Background Image" class="background-image">
    
    <!-- 버튼 -->
    <button type="btn" class="btn btn-success me-1" onclick="location.href='index2.html'"></button>
    <button type="btn1" class="btn1 btn1-success me-1" onclick="location.href='index(Web).html'"></button>
    </body>
    </html>
-----------------------
//index2.html

    <!DOCTYPE html>
    <html lang="en">
    <head>
      <!-- Google Fonts 불러오기 -->
      <!-- 이 구문은 Google Fonts에서 제공하는 "도현" 폰트를 웹 페이지에 연결하기 위한 것입니다. -->
      <link rel="preconnect" href="https://fonts.googleapis.com">
      <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
      <link href="https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap" rel="stylesheet">
      
      <!-- 페이지의 기본 설정 -->
      <meta charset="UTF-8"> <!-- 문서의 문자 인코딩을 UTF-8로 설정 -->
      <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- 반응형 웹 디자인을 위한 뷰포트 설정 -->
      <meta http-equiv="X-UA-Compatible" content="ie=edge"> <!-- IE 브라우저 호환성 보장 -->
      <title>Face Recognition</title> <!-- 웹 페이지의 제목 설정 -->
      
      <!-- 외부 CSS 파일 연결 -->
      <!-- 이 구문은 동일한 폴더 내의 css.css 파일을 현재 HTML 문서에 연결하기 위한 것입니다. -->
      <link rel="stylesheet" href="css.css"> 
      
      <!-- 인라인 스타일 -->
      <style>
        /* 전체 body에 대한 스타일 설정 */
        /* 이 부분은 웹 페이지의 전체적인 레이아웃과 배경을 설정합니다. */
        body {
          margin: 0; /* 바깥 여백을 0으로 설정 */
          padding: 0; /* 안쪽 여백을 0으로 설정 */
          width: 100vw; /* 너비를 뷰포트 너비의 100%로 설정 */
          height: 100vh; /* 높이를 뷰포트 높이의 100%로 설정 */
          display: flex; /* Flexbox 레이아웃을 사용 */
          justify-content: center; /* 주 축(여기서는 수평 축)을 중심으로 자식 요소들을 정렬 */
          align-items: center; /* 교차 축(여기서는 수직 축)을 중심으로 자식 요소들을 정렬 */
          flex-direction: column; /* 자식 요소들을 수직 방향으로 정렬 */
          
          /* 배경 그라디언트 적용 */
          /* 이 부분은 body의 배경에 두 개의 원형 그라디언트를 중첩하여 적용하는 스타일입니다. */
          background: radial-gradient(circle at center, #ffffff 20%, #ffffff00 70%), radial-gradient(circle at center, #ffae00 20%, #ffffff00 70%);
        }
    
     /* 이미지 업로드 버튼 스타일 설정 */
    #uploadButton {
      cursor: pointer; /* 포인터 모양을 클릭 가능한 상태로 변경 */
      margin-top: 50px; /* 버튼의 상단 여백을 50px로 설정 */
    }
    
    /* 이미지 업로드 버튼 내 이미지 스타일 설정 */
    #uploadButton img {
      width: 100%; /* 이미지의 너비를 버튼 너비로 100% 설정 */
      height: 100%; /* 이미지의 높이를 버튼 높이로 100% 설정 */
    }
    
    /* 로고 이미지 스타일 설정 */
    #logo {
      position: absolute; /* 절대 위치를 사용하여 페이지 내에서 위치 지정 */
      top: 10px; /* 상단에서 10px 떨어진 곳에 위치 */
      left: 50%; /* 왼쪽에서부터 화면의 50% 지점에 위치 */
      transform: translateX(-50%); /* X축으로 -50%만큼 이동하여 중앙 정렬 */
      width: 20%; /* 로고 이미지 너비를 전체의 20%로 설정 */
      height: auto; /* 높이를 자동으로 설정하여 비율 유지 */
    }
    
    /* 이미지 업로드 input 태그 숨김 */
    #imageUpload {
      display: none; /* 업로드 버튼을 보이지 않게 설정 */
    }
    
    /* 이미지를 감싸는 컨테이너 스타일 설정 */
    #imageContainer {
      width: 400px; /* 컨테이너의 너비를 400px로 설정 */
      height: auto; /* 이미지의 원래 높이에 맞게 자동 조정 */
      margin-top: 20px; /* 컨테이너 상단의 여백을 20px로 설정 */
      position: relative; /* 위치를 상대적으로 설정, 내부 요소의 절대 위치 지정에 사용 */
    }
    
    /* 이미지 컨테이너 내 이미지 스타일 설정 */
    #imageContainer img {
      width: 100%; /* 컨테이너 내의 이미지 너비를 컨테이너 너비로 100% 설정 */
      height: auto; /* 이미지의 높이를 자동으로 설정하여 비율 유지 */
    }
    /* 캔버스 스타일 */
    canvas {
      position: absolute; /* 캔버스를 페이지의 절대적 위치에 배치합니다. */
      top: 0; /* 캔버스를 페이지의 상단에 정렬합니다. */
      left: 0; /* 캔버스를 페이지의 왼쪽에 정렬합니다. */
    }
    
    body{
        background-color: blanchedalmond; /* 배경색을 blanchedalmond로 설정합니다. */
        height: 100vh; /* body의 높이를 뷰포트 높이의 100%로 설정하여 전체 화면을 채웁니다. */
        display: flex; /* flexbox 레이아웃을 사용하여 자식 요소들을 정렬합니다. */
        justify-content: center; /* 가로 축에서 중앙 정렬합니다. */
        align-items: center; /* 세로 축에서 중앙 정렬합니다. */
    }
    
    .bts1 {
        font-size: 70px; /* 폰트 크기를 70px로 설정합니다. */
        padding: 15px; /* 주변 여백을 15px로 설정합니다. */
        background-color: blanchedalmond; /* 배경색을 blanchedalmond로 설정합니다. */
        color: black; /* 글자색을 검은색으로 설정합니다. */
        border: 3px solid black; /* 테두리를 검은색 실선으로, 두께는 3px로 설정합니다. */
        text-transform: uppercase; /* 텍스트를 대문자로 변환합니다. */
        font-family: "Do Hyeon", sans-serif; /* 폰트 패밀리를 "Do Hyeon"과 sans-serif로 설정합니다. */
        transition: all 0.4s; /* 모든 변화에 대해 0.4초 동안의 전환 효과를 적용합니다. */
        position: fixed; /* 요소의 위치를 고정시킵니다. */
        bottom: 50px; /* 하단에서 50px 떨어진 위치에 배치합니다. */
        left: 50%; /* 왼쪽에서 50% 떨어진 위치에 배치합니다. */
        transform: translateX(-50%); /* X축으로 -50% 만큼 이동시켜 가운데 정렬 효과를 줍니다. */
    }
    
    /* .bts1 클래스에 대한 기본 스타일 */
    .bts1 {
        position: fixed; /* 고정 위치 */
        bottom: 50px; /* 하단에서 50px */
        left: 10%; /* 왼쪽에서 10% */
        transform: translateX(-50%); /* X축 기준 중앙 정렬 */
    }
    
    /* .bts1 요소가 포커스될 때의 스타일 */
    .bts1:focus{
        outline: none; /* 포커스 아웃라인 제거 */
    }
    
    /* .bts1 요소에 마우스 호버 시의 스타일 */
    .bts1:hover{
        background-color: black; /* 배경색 검정 */
        color: white; /* 글자색 흰색 */
    }
    
    /* .bts2 클래스에 대한 기본 스타일 */
    .bts2 {
        font-size: 70px; /* 폰트 크기 */
        padding: 15px; /* 패딩 */
        background-color: blanchedalmond; /* 배경색 */
        color: black; /* 글자색 */
        border: 3px solid black; /* 테두리 */
        text-transform: uppercase; /* 대문자 변환 */
        font-family: "Do Hyeon", sans-serif; /* 폰트 스타일 */
        transition: all 0.4s; /* 전환 효과 */
        position: fixed; /* 고정 위치 */
        bottom: 50px; /* 하단에서 50px */
        left: 50%; /* 왼쪽에서 50% */
        transform: translateX(-50%); /* X축 기준 중앙 정렬 */
    }
    
    /* .bts2 요소가 포커스될 때의 스타일 */
    .bts2:focus{
        outline: none; /* 포커스 아웃라인 제거 */
    }
    
    /* .bts2 요소에 마우스 호버 시의 스타일 */
    .bts2:hover{
        background-color: black; /* 배경색 검정 */
        color: white; /* 글자색 흰색 */
    }
    
    /* .bts2 클래스의 위치 조정 */
    .bts2 {
        position: fixed; /* 고정 위치 */
        bottom: 50px; /* 하단에서 300px */
        left: 90%; /* 왼쪽에서 90% */
        transform: translateX(-50%); /* X축 기준 중앙 정렬 */
    }
    
    <!-- CSS를 이용해 이미지 호버 스타일 정의 -->
    <style>
      #uploadButton:hover img {
        content: url('Design/upload2.png'); /* 호버 시 이미지가 upload2.png로 변경됩니다 */
      }
    </style>
    </head>
    <body>
      <!-- 이미지 업로드 버튼: 이미지를 포함하는 레이블 정의 -->
      <label for="imageUpload" id="uploadButton">
        <img src="Design/upload.png" alt="Upload"> <!-- 업로드 버튼 이미지 -->
      </label>
      <!-- 파일 선택을 위한 input 요소 -->
      <input type="file" id="imageUpload">
    
      <!-- 로고 이미지 -->
      <img src="Design/logo.png" alt="Logo" id="logo">
    
      <!-- 업로드된 이미지를 표시할 컨테이너 -->
      <div id="imageContainer">
        <!-- 초기 상태에서는 내부가 비어 있음 -->
      </div>
    
      <!-- face-api.js와 사용자 정의 스크립트 로드 -->
      <script defer src="face-api.min.js"></script>
      <script defer src="script.js"></script>
    
      <script>
        // 이미지 및 로고 숨기기 함수
        function hideImages() {
          document.getElementById('imageContainer').style.display = 'none';
          document.getElementById('logo').style.display = 'none';
        }
    
        // 얼굴 인식 처리 후 이미지와 로고 숨김
        // setTimeout을 사용하여 예시로 3초 후 함수 호출
        setTimeout(hideImages, 3000); // 3초 후에 hideImages 함수 호출
      </script>
      <!-- '맞다!' 버튼: 클릭 시 index(yes).html로 이동 -->
      <button type="bts1" class="bts1 bts1-success me-1" onclick="location.href='index(yes).html'">맞다!</button>
      <!-- '아니다..' 버튼: 클릭 시 index(No).html로 이동 -->
      <button type="bts2" class="bts2 bts2-success me-1" onclick="location.href='index(No).html'">아니다..</button>
    </body>
    </html>


-----------------------
소감 : 

# 신현진(20210817) : 

이번 face-api는 평소에도 많이사용하지만 실제로 만들어본적이 없는 것이였기 때문에 색다른 경험이였습니다. 실제로 코드 작성하는 방법도 편하게 api로 공유되어 있어서 편하게 사용을 했습니다.. 하지만 기본틀이 되는 코드를 제공해 줌에도 불구하고 코드를 살짝 수정하는 일은 결코 쉽지 않았습니다. 코드를 수정하니 트래킹 캔버스가 고장이나거나, 아예 웹캠이 켜지지않거나, 이미지를 불러올수 없다거나 등 다양한 어려움이 닥쳐왔습니다. 하지만 조원들이 손에 불이날 정도로 열심히 찾아준 덕분에 성공적으로 프로젝트를 마무리 할수있었습니다. 그리고 이번 프로젝트로 face-api 만 사용하면 심심할까 css도 같이 사용하여 html을 꾸몄는데 생각보다 재미도 있었고 조원들과 수정하면서 많은 아이디어와 적용하는 방법도 그렇게 어렵지 않아서 매우 재미있게 이번 팀프로젝트를 했던거 같습니다. 마지막으로 이번에 프로젝트에서 처음 조장을 맡게되어 부담감이 없지않게 있었습니다. 하지만 조원들끼리 모여서 토의하고 사진도 찍고 서로의 코드를 공유하면서 문제점을 체크하며 조장이란 무거운 자리이지만 그만큼 받쳐주는 팀원들이 있기에 조장은 무너지지않는다는것을 배웠습니다.


-------------------
# 김종준(20171111) : 

팀 프로젝트를 진행하면서 얼굴 인식 시스템 개발을 함께 진행하는 것은 매우 흥미로웠습니다. 프로젝트를 통해 얼굴 인식 기술의 가능성과 중요성을 깊이 이해할 수 있었고, 팀원들과의 협업을 통해 문제를 해결하고 새로운 아이디어를공유하는 과정에서 큰 성취감을 느낄 수 있었습니다. AI 기술을 사용해본 경험은 정말 감동적이었습니다. 우리가 API를 사용해 개발한 얼굴 인식 시스템은 인간의 얼굴을 식별하고 분석하는 과정에서 놀라운 성능을 보여주었습니다. 이러한 기술을 사용하면서 우리는 미래의 중심이 될 AI 기술의 가능성과 파급력을 몸소 느낄 수 있었습니다. 이를 통해 AI 기술의 무한한 가능성에 대한 열정과 도전을 경험할 수 있었습니다. 또한, 팀원들과의 협업 능력과 기술적 역량을 향상시킬 수 있었고, 저에게 더 큰 도전과 성취를 꿈꾸게 해주었고, 미래에는 더욱 발전된 AI 기술을 통해 사회에 긍정적인 영향을 끼칠 수 있기를 간절히 바랍니다.

-----------------------
# 안현수(20210818) : 

처음 팀 프로젝트를 했을 때부터 지금까지 쭉 같은 팀원으로 팀프로젝트를 진행하다가 새로운 조원인 홍재영 학우가 팀에 합류하여 4명에서 처음으로 같이 시작하게 되었습니다. 처음에 시행할 때 이미지 삽입이 안돼서 애를 먹었는데, 주변 학우의 도움으로 문제를 해결하였습니다. 같이 사진을 찍고 그냥 이대로 올리려 했지만 팀원들이 한번 만드는거 스토리가 있고 팀색깔을 넣어 만들어보고 싶다고 하여서 생각했던 것보다 거창해진 프로젝트 활동이 되었던 것 같습니다. 

-----------------------
# 홍재영(20230970) : 

Face-API를 활용하여 얼굴을 인식하는 시스템을 제작하는 과정은 흥미로웠습니다. 얼굴을 등록하는 과정에서는 개인의 특징을 정확히 파악하고 저장하는 것이 중요했습니다. 인식하는 과정에서는 사진이나 영상으로부터 얼굴을 식별하는 기능을 구현하는 것이 흥미로웠습니다. 개인별 인식과 단체 인식 모두를 고려하여 시스템을 설계하는 것은 도전적이었지만, 그 결과를 보는 것은 보람차고 기쁘게 느껴집니다. 이 시스템은 다양한 분야에서 활용될 수 있어서 미래에더 많은 발전 가능성을 가지고 있다고 생각합니다.

-------------------


