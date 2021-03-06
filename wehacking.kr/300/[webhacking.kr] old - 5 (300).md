
<img width="275" alt="스크린샷 2020-01-08 오후 10 10 34" src="https://user-images.githubusercontent.com/54495632/71982554-13e53f00-3268-11ea-883a-f6369757df73.png">


5번!

<img width="410" alt="스크린샷 2020-01-08 오후 10 10 42" src="https://user-images.githubusercontent.com/54495632/71980803-468d3880-3264-11ea-8bd2-cc2979a14fc0.png">

첫 화면에 들어가면 login 과 join 버튼만 나와있다.

<img width="237" alt="스크린샷 2020-01-08 오후 10 10 48" src="https://user-images.githubusercontent.com/54495632/71980811-5147cd80-3264-11ea-8f2a-74974a5dd3de.png">

<img width="237" alt="스크린샷 2020-01-08 오후 10 10 48" src="https://user-images.githubusercontent.com/54495632/71981012-cd421580-3264-11ea-898a-a8b12d9aad33.png">

login 창이 보인다. 여러 SQL injection을 시도해보았지만 잘 먹히지 않고 혹시 싶어 소스코드를 확인해보았다.

<img width="328" alt="스크린샷 2020-01-08 오후 10 11 13" src="https://user-images.githubusercontent.com/54495632/71981053-e77bf380-3264-11ea-97b7-5d20b6f9b06b.png">

딱히.. 특별한 부분은 없었다.

<img width="447" alt="스크린샷 2020-01-08 오후 10 12 01" src="https://user-images.githubusercontent.com/54495632/71981075-f367b580-3264-11ea-998a-285960f8eb8b.png">

첫 화면으로 돌아가 join을 누르니 접근 자체가 거부당했다.

<img width="448" alt="스크린샷 2020-01-08 오후 10 12 47" src="https://user-images.githubusercontent.com/54495632/71981119-09757600-3265-11ea-88cb-8a1d0238bf7a.png">

첫 화면에서 소스코드를 확인 했다.

move 함수에서 login 일 때 URL mem/login.php 로 접속하는 것을 보아

mem/join.php 도 존재하지 않을까 싶어 시도했다.

<img width="724" alt="스크린샷 2020-01-08 오후 10 13 48" src="https://user-images.githubusercontent.com/54495632/71981225-3fb2f580-3265-11ea-8815-e13a421d2da1.png">

bye라는 출력문자와 함께 접근이 불가능하다...

어쩔 수 없이 소스코드를 열었다.

<img width="435" alt="스크린샷 2020-01-08 오후 10 17 41" src="https://user-images.githubusercontent.com/54495632/71981264-6113e180-3265-11ea-93a2-78dcf2fa484f.png">

...여러 개의 l 문자로 복호화 시킨 소스코드 같다... 이 것을 해석하면 되는 더러운 문제이다.

eval 함수는 텍스트로 된 코드를 실행시킬 수 있는 함수이고 사용 시 동적으로 소스코드를

실행시킬 수 있다고 한다. 해당 코드를 분석하게 되면,

if (eval(document.cookie).indexOf(oldzombie) == -1) {
    alert('bye');
    throw "stop";
}
if (eval(document.URL).indexOf(mode=1) == -1) {
    alert('access_denied');
    throw "stop";
} 

else{
}

다음과 같은 해석된 코드를 얻을 수 있다.

editThisCookie를 이용하여 쿠키에 oldzombie를 만들어 주고 

기존의 URL 에 mode=1을 추가하게 되면 join 페이지에 접근할 수 있다.

<img width="985" alt="스크린샷 2020-01-08 오후 10 31 15" src="https://user-images.githubusercontent.com/54495632/71982090-30cd4280-3267-11ea-8de4-257a096f77e6.png">

<img width="244" alt="스크린샷 2020-01-08 오후 10 31 36" src="https://user-images.githubusercontent.com/54495632/71982113-3cb90480-3267-11ea-95f1-b1c263b2d59a.png">

<img width="450" alt="스크린샷 2020-01-08 오후 10 31 25" src="https://user-images.githubusercontent.com/54495632/71982120-42aee580-3267-11ea-94bd-d6758b0d8b88.png">

admin 아이디가 원래 있었다.

<img width="239" alt="스크린샷 2020-01-08 오후 10 32 19" src="https://user-images.githubusercontent.com/54495632/71982156-4f333e00-3267-11ea-9eb1-04e5fcd5d51f.png">

<img width="227" alt="스크린샷 2020-01-08 오후 10 32 22" src="https://user-images.githubusercontent.com/54495632/71982164-52c6c500-3267-11ea-83ff-7d9f36f9cabe.png">

<img width="269" alt="스크린샷 2020-01-08 오후 10 32 28" src="https://user-images.githubusercontent.com/54495632/71982176-53f7f200-3267-11ea-8942-6ac9cc5a685f.png">

아무 아이디를 만들어 로그인을 했는데 admin으로 로그인을 해야 최종적으로 풀리는 문제인

것 같다.. SQL injection을 다시 시도해봤지만 불가능했고 '공백'admin 이런 형식으로

아이디를 생성하고 다시 로그인을 시도했다.

<img width="451" alt="스크린샷 2020-01-08 오후 10 37 36" src="https://user-images.githubusercontent.com/54495632/71982404-b81ab600-3267-11ea-8133-808088d5f4a4.png">

<img width="334" alt="스크린샷 2020-01-08 오후 10 37 42" src="https://user-images.githubusercontent.com/54495632/71982407-ba7d1000-3267-11ea-94d4-e8ab6f3d11bb.png">



