# for-len 함수
## 평균계산기 초기단계)
평균계산기를 계속해서 제작해보았지만 정작 for 반복문과 len함수를 사용해서 제작하지 않았었다.<br>
바로 코드를 한줄 적기보단 알고리즘을 세워서 큰 틀을 잡아보았다.<br>
<img width="525" height="399" alt="for_len사용 평균제작" src="https://github.com/user-attachments/assets/a46ac1c1-df7d-45aa-b6f8-5a2640809d84" /><br>
저번 재귀함수 때 if문에 사용했던 방식대로, if문에서 원하는 횟수에 도달하면 함수를 종료시키고, 그렇지않으면 num을 새로운 수로 초기화 및 sum 합계를 더하는 방식이다.<br>
당시에는 return문에는 무엇을 써야할지 몰라 남겨두었다.<br>
그 다음으로는 천천히, 문법에 맞지 않더라도 하나하나씩 필요한 변수와 구현하고 싶은 방식대로 빈공간을 채워나갔다.<br>
<img width="708" height="421" alt="for_len사용 평균제작(2)" src="https://github.com/user-attachments/assets/7a84de78-c1a4-4bfe-8941-5b1813802aa5" /><br>
문법에 맞지 않더라도 작성했더라고 해도 당연히 지금봐서는 정말 말도 안되는 코드라는 건 실행하지 않아도 알 수 있었다.<br>
숫자를 입력받을 변수 num을 처음에 입력받고, 들어온 숫자만큼 반복시키고 싶다는 마음에 len(num)을 range안에 넣어놓았고, return은 필요없다고 생각했다.<br>
<img width="496" height="575" alt="for_len사용 평균제작(3)" src="https://github.com/user-attachments/assets/fff24a82-956c-4c09-96a3-6a68944b1d8c" /><br>
이런저런 고민을 걸쳐서 위의 사진과 같은 결과가 되었었다.<br>

### 문제점 파악
여기서 문제점이 발생한다.<br>
**첫번째)** 지금 이 코드가 효율적인가? -> len을 쓸거였으면서 굳이 Count라는 함수를 만들어서 더할 필요가 없다. (C언어로 작성된 내장함수가 더 효율적)<br>
**두번째)** 코드가 제대로 작동하는가? -> 그것도 아니다.<br>
**세번째)** 머릿속으로 생각했던 대로 숫자를 계속 반복시킨다 하더라도, 계속 초기화되는 값에 마무리를 어떻게 알 수 있게 할 것인가 ?<br><br>
**결론) 지금 방식으로는 차라리 몇번 더할 것인지 미리 입력받고 그만큼 숫자를 더 해야 했을 것이다.<br>**
<img width="651" height="43" alt="찾은 문제점" src="https://github.com/user-attachments/assets/db37e325-7ad5-4ba9-8f8d-e02b43e9cfeb" /><br>
이를 전부 관통하는 한 줄을 생각해냈고, 모두 갈아엎은 뒤 새로 시작하기로 했다.<br>

## while문 변경
<img width="553" height="308" alt="while문(return)" src="https://github.com/user-attachments/assets/a06a17a4-ea79-42ff-b354-fa4a39434b8b" /><br>
첫번째로 작성한 while문, return에서 오류가 발생했다.<br>
저번에 재귀함수를 풀 때였는지, 3개를 갖고 평균계산기를 만들 때 였는지 그때도 이런 경험이 한번 있었다.<br>
바로 return문을 함수에 쓰지 않아서 발생하는 오류이다. (함수를 만드는 것이 아니라면, 바깥으로 반환할 필요가 없음)<br>
나는 함수를 종료하고 싶은 마음이였고, 지금보니 print만 써서 맺음을 하면 되는데, 당시에는 그럼 어떻게 종료하지 라는 생각으로 함수로 만들어버렸다.<br>
<img width="574" height="406" alt="while문 (return을 위한 함수제작)" src="https://github.com/user-attachments/assets/c36bc1cb-92e8-4f37-bd09-c88f83a96200" /><br>
<img width="514" height="154" alt="while문 결과" src="https://github.com/user-attachments/assets/23687e30-5823-4bea-a137-931f2a9b048f" /><br>
<br>
코드를 완성하고보니, 눈에 밟히는 점이 있었다.<br>
무한반복을 위해서 굳이 i=1, i>0 등의 조건을 넣어야할까? 다른 방법은 없나? 그리고 return num을 꼭 해야하나?<br>
또, -1입력보다 끝을 냇다고 할 수 있는 end 같은 텍스트를 넣는게 더 좋아보인다.<br>
검색해보니, while문에 True라고 작성하면 무한반복이 된다고 했으며, return num, sum, count를 위해 함수를 만들었지만, break문을 사용해도 함수를 종료할 수 있다고 한다.<br>

### 버그 발생
<img width="558" height="207" alt="while문 종료값 end(1)" src="https://github.com/user-attachments/assets/339510a7-2424-4e00-8446-342b43f5df6a" /><br>
너무 깔끔해져서 기분이 좋았다.. 라고 생각하기도 전에 버그가 발생한다.<br>
<img width="521" height="171" alt="while문 종료값 end 1차 버그" src="https://github.com/user-attachments/assets/3c92d4f3-36bb-423b-b7a1-aa9450bc2516" /><br>
입력한 값은 6개인데, 5, 32, -1만 들어가서 합은 36, 총 개수는 3개라고 뜬다는 것.<br>
왜 저런 합과 개수가 나오는 지도 몰랐고, 처음에는 대체 이게 무슨 버그인가 싶었지만, if문 안에 있는 input이 문제라는 것을 알고 수정했다.<br>
그렇게 나온 완성본이다.<br>
<img width="584" height="463" alt="while문 완성" src="https://github.com/user-attachments/assets/bb7f086b-9b8c-4b6b-a2de-95f8a116d0e5" /><br>

# 오늘의 감상평
결국 for문도 len도 사용하지 않고 다른방법으로 풀게 되었다..<br>
현직 개발자분들이 보시기엔 어떨지 모르겠지만, 지금의 나에겐 꽤나 어려운 문제였다.<br>
원하는 방식대로 풀지 못하게 되어서 기분이 사실은 좀 많이 찝찝하고 시간도 오래걸려서 더 그런 것 같다.<br>
그래도 break와 무한반복을 배웠으니 그걸로 만족하려고 합니다.<br>
하나라도 얻어갔으니 전보다는 나아진거니까요.<br>
<br>
+) 그래도 경험이 경험이라고, 이제는 어디가 덜 효율적인지도 스스로 판단할 수 있게 되었었네요.<br>
다른 방법도 찾아보게 되고, return문 오류가 떳을때에도 잘 찾는걸 보니 방향은 잘 가고 있었던 것 같습니다.<br>
