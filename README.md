# 한국표준산업분류(KSIC) 자동 분류 모델
기간 : 23.01.19 ~  
요약 : 지정상품과 한국표준산업분류 1 대 N 매칭을 위한 다중 분류 모델  
***
### 느낀점   
데이터와 도메인에 대한 이해가 없으면 그 뒤 모든 프로세스가 힘들어진다는것을 깨달았다...😂  
그리고 역시 실무에서는 내가 배운 이론들이 잘 적용되지 않으며 어느정도 타협이 필요하다는것..😂  
분석 외적으로는 내가 만든 모델에 대해 다른 사람들에게 쉽게 설명하는 것 또한 매우 어려운 일이라는것..😂  
아직 끝나진 않았지만, 매우 좋은 경험인것 같다.
***
### 과제
회사 현장실습 간 상표 출원을 위해 정의된 지정상품(50000여개)를 산업 분류 내 최소단위인 세세분류(1200여개)와 1 대 N 매칭을 시킬 수 있는 방안을 찾는 과제가 주어짐.   
이에 관련 논문을 참고하여 임베딩을 활용한 자동분류모델의 방식을 확인. 이를 차용하여 모델 구축.
***
### REFERENCE
> * 오교중, 최호진, 안현각. _"기계학습 기반 단문에서의 문장 분류 방법을 이용한 한국표준산업분류,"한국정보과학회 언어공학연구회:학술대회논문집(한글 및 한국어 정보처리)_(2020):394-398. [링크](https://koreascience.kr/article/CFKO202030060861862.pub?&lang=ko&orgId=sighlt)  
> * 임정우, 문현석, 이찬희, 우찬균, 임희석. _딥러닝 기법을 활용한 산업/직업 자동코딩 시스템.한국융합학회논문지_,(2021).12(4),23-30.
[링크](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE10659726)  
> * 김성훈. _"사용자 정의 분류체계에 따른 딥러닝 기반의 특허문서 자동분류."_ 국내박사학위논문 한성대학교 대학원, (2022). 서울
[링크](http://www.riss.kr/search/detail/DetailView.do?p_mat_type=be54d9b8bc7cdb09&control_no=7933f6ed6ac8df7effe0bdc3ef48d419)
***
# Process
### Data(예시)
* 지정상품  :  분류 대상(Input) 

| 명칭 | 분류번호 |
| :---: | :----: |
| 맥주 | 10 |
| 소주 | 11 |
| ... | ... |    

* 산업분류 : 분류 결과(Output)  

| 대분류 | 중분류 | 소분류 | 세분류 | 세세분류 |
| :---: | :----: | :---: | :----: | :---: |
| A(농업) | 01(농업) | 011(작물재배) | 0111(곡물 및 작물) | 01111(곡물 재배) |
|  |  |  |  | 01112(작물 재배) |
|  |  |  | 0112(향신용 작물) | 01121(과실 작물 재배) |
|  |  |  |  | 01122(고수 재배) |
| F(제조업) | 29(전기장비 제조) | 291(조명장치 제조) | 2911(전구 및 램프 제조) | 29111(전구 제조업) |
| ... | ... |  ... | ... | ... |   

* 색인어 : 모델 학습을 위해 KSIC 해설서 내 세세분류 별 색인어를 직접 크롤링하여 만든 데이터셋
<img src="https://velog.velcdn.com/images/pong_jin/post/b0a20f45-1182-43e5-a4bd-7c55780da9fd/image.PNG" width="200" height="300">
| 색인어 | 세세분류명 | 세세분류코드 |
| :---: | :----: |:----: |
| 맥주 | 알코올 음료 제조 | 27130 |
| 증류식 소주 | 알코올 음료 제조 | 27130 |
| ... | ... | ... |   

***

