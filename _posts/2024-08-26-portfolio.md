
안녕하세요! BE/Infra 개발자 곽지혁입니다.

(자기소개)

<br>
✔️ 다양한 협업 경험을 통해 어떤 환경에서도 빠르게 적응합니다.

✔️ (추가 ...)


## 📌 Profile

### 🔗 Contacts
- Email: kwlgur0416@gmail.com
- GitHub: [Hyukji](https://github.com/hyukji)
- Blog: [늦었지만 빠른때](https://hyukji.tistory.com/)

### 🎓 Education

- Samsung Software Academy For Youth (SSAFY)
    - 2024.01 ~ 

- 대구경북과학기술원 (DGIST)
    - 기초학부 공학 학사, 컴퓨터 트랙
    - 2018.02 - 2024.02
    - GPA: 3.65/4.3

### 📚 Stacks
- BE : `SpringBoot`, `JPA`, `QueryDsl`, `Mysql`, `MongoDB`, `node.js`, 
- Infra : `AWS(EC2, S3)`, `Nginx`, `Jenkins`, `Docker-compose`, `Docker`
- FE : `Vue.js`
- Data : `Python`, `PyTorch`, `NumPy`, `pandas`, `Matplotlib`

### 🌐 Language Skills
- OPIC IM1 (2024.03)

## 📖 Projects


<details markdown="1">
<summary class="h3-title">
&nbsp; 온라인 알고리즘 스터디를 위한 웹사이트 개발 
</summary>

> 2024.7 - 2023.8
> 
> Samsung Software Academy For Youth 

#### 프로젝트 개요

- 문제 제기
    - 스터디의 일정 및 문서 관리의 비효율성.
    - 코드 공동 작성의 부재로 인한 피드백 한계.
    - 구두 설명으로 인한 이해의 어려움.

- 역할
    
    - Infra 구축 및 DB 설계
        - Nginx을 이용한 ssl 인증, 프록시 설정
        - Jenkins를 활용한 ci/cd 구축
    
        [이미지]

    - 폴더 구조 및 스터디 템플릿
        - `재귀 구조`를 이용한 폴더 구조 구현
        - 최적화 
            - `N+1` 문제 해결
                - queryDsl 및 fetchJoin을 이용해 N+1 문제 해결
            - Redis를 이용한 캐시 활용.
                - 스터디의 전체 폴더 구조의 경우 추가, 수정, 삭제 보다 조회가 더 많이 호출됨.
                - nGrinder를 이용한 성능 테스트를 통해 23초에서 1초로 성능 향상
    
    - Java, Python 코드 실행

        - 실행 언어의 확장성을 고려해 `팩토리 패턴`을 활용.

            <details>
                <summary>팩토리 패턴 적용 코드</summary>

                #### CodeExecutorFactory

                ```java

                    @Component
                    public class CodeExecutorFactory {

                        private final Map<Language, CodeExecutor> executors;

                        public CodeExecutorFactory(List<CodeExecutor> executorList) {
                            executors = executorList.stream()
                                    .collect(Collectors.toMap(CodeExecutor::getLanguage, Function.identity()));
                        }

                        public CodeExecutor getExecutor(Language language) { return executors.get(language); }
                    }

                ```

                #### CodeExecutor

                ```java

                    public interface CodeExecutor {

                        String executeCode(String code, String input);

                        File createCodeFile(String code, String hostPath) throws IOException;

                        Language getLanguage();

                        default String readProcessOutput(InputStream inputStream) throws IOException { ... }

                    }

                ```
                
            </details>


        - Container를 활용한 코드 실행 구현
            
            - 코드 실행 api 요청마다 컨테이너 생성 및 삭제.

            - 가상화 기술의 활용 이유 : 검증되지 않은 코드를 서버에서 직접 실행하는 것은 보안적인 취약점이 존재할 수 있다고 판단. 

            - 컨테이너는 매번 생성하고 삭제하는 것은 부하가 없나? 있지... 어떡하지 결국 pooling이 답인가? k8s? 어떻게 하지?

            - 코드 실행과 관련한 자원 관리
                - Container에 할당할 메모리, cpu를 설정
                - 무한 루프와 같은 경우를 대비해 컨테이너 시간이 10초를 넘어가지 않도록 설정
                - 세마포어를 이용한 컨테이너 개수 제한


#### 기술 및 라이브러리

- BE & DB: `SpringBoot`, `JPA`, `QueryDsl`, `Mysql`, `Redis`
- Infra: `Nginx`, `ec2`, `Jenkins`, `Docker`, `Dokcer-compose`
- Etc : `WebRTC`


#### 관련 자료



</details>



<details markdown="1">
<summary class="h3-title">
&nbsp; RealWorld  
</summary>

> 2023.8 - 2023.10
> 
> SpringBoot Project

#### 프로젝트 개요

- SpringSecurity
- Test 작성
- CQRS 패턴 적용


#### 기술 및 라이브러리
- BE : SpringBoot, Mysql, JPA, QueryDsl

#### 관련 자료
[GitHub](https://github.com/realworld-spring/spring-boot)

</details>

<details markdown="1">
<summary class="h3-title">
&nbsp; 어절 단위 청취 기능을 탑재한 IOS 어플리케이션 개발  
</summary>

> 2023.1 - 2023.4
> 
> 1인 개발 프로젝트

#### 프로젝트 개요
- 문제 제기 및 솔루션
    - 어학 공부 중 부족한 부분을 이해하기 위해 여러 번 반복 청취가 필요함.
    - 쉐도잉 학습 시 기존 플레이어의 초 단위 이동 및 AB 구간 반복 기능에 불편함 존재.
    - **어절 단위로 오디오를 구분**해 보다 편리하고 정확한 위치 이동을 제공하는 어플리케이션 개발

- 결과

    -  어절 단위 청취 기능
        - 오디오 파일 생성 시, 오디오 파장 분석 및 어절 단위 구분
        - 어절 단위로 이동 및 반복 기능

        [이미지]

    - 오디오 파일 관리 기능
        - wifi & usb 를 이용한 오디오 파일 업로드 기능
        - 폴더 구조를 이용한 파일 관리

        [이미지]

    - 프로젝트 과정을 블로그에 기록하여 공유.

#### 관련 자료
[GitHub](https://github.com/hyukji/ListenApp) 

[Blog](https://hyukji.tistory.com/category/IOS/%EA%B0%9C%EB%B0%9C%EC%9D%BC%EC%A7%80)

</details>



<details markdown="1">
<summary class="h3-title">
&nbsp; 소스코드 유사도 분석 알고리즘 및 이를 이용한 교육 보조 프로그램 
</summary>

> 2020.03 - 2020.12 
> 
> Undergraduate Group Research Program (UGRP) - DGIST

#### 프로젝트 개요
- 문제 제기 및 솔루션
    - 코딩을 처음 배우는 학생들의 코드는 길이가 짧아 구조적 유사성은 적합한 표절 기준이 아님
    - 코딩 스타일을 기준으로 표절도를 검사하되 학습 과정에 따른 코딩 스타일의 가변성을 고려함
    - 이 알고리즘을 적용한 코딩 교육 사이트를 만들고자 함
- 결과
    - 코딩 스타일 기반의 소스코드 유사도 계산 알고리즘 연구 (Python, tokenizer)
        - 변수명, 클래스명, 연산자 주위 공백 등을 기준으로 코딩 스타일 vector를 생성
        - 지금까지 작성해온 코딩 스타일과 현재의 코딩 스타일을 비교하여 표절도를 계산함
        - 코딩 스타일에 급격한 변화가 있을 경우 높은 표절도를 가짐
    - 코드 표절 검사 기능을 활용한 코딩 교육 사이트 (MEVN stack)
        - 로그인 및 회원가입
        - 강좌 및 과제 등록
        - 개인 학습현황
        - 실습 과제를 위한 실시간 Python interpreter
            - 샌드박스 및 에디터 화면 분할 기능
            - 화면
                ![editor](https://user-images.githubusercontent.com/52347271/230982511-6f7663ba-234a-4570-bc8e-0cea3ecfaf0f.jpg)
            
#### 역할
 - 팀 구성: 4인
 - 알고리즘 연구
    - 연산자 및 괄호 주위 공백, 평균 함수 길이 등의 코딩 스타일 vector 추출
    - 표절도 계산식 정립
    - K-means Clustering을 이용한 군집 내 편차 계산
 - 사이트 개발
    - Docker와 Socket을 사용한 실시간 Python interpreter 구현
    - 강의 캘린더 및 일정 조율 기능
    - AWS EC2 서버 및 MongoDB Atlas 관리


#### 기술 및 라이브러리
- Data Analysis: `Python`, `tokenizer`, `pandas`, `NumPy`
- Web Development: `Vue.js`, `Node.js`, `AWS EC2(Ubuntu)`, `MongoDB`, `GitHub`, `Vuetify`
- Extra: `Docker`, `Socket.io`

#### 관련 자료
[GitHub](https://url.kr/nsvhta)

</details>



## 💻 Work Experiences

<details markdown="1">
<summary class="h3-title">
&nbsp; 올인원주식회사 인턴십
</summary>

> 2021.01 - 2021.03
> 
> 사용자의 영어 수준을 평가하는 알고리즘 개선

#### 역할

- 사용자의 영어 수준을 평가하는 알고리즘 개선

    - 기존 알고리즘 

        - 사용자의 임시 수준을 설정하고, 그에 맞는 문제를 제공.
        - 제공된 문제의 정답 여부에 맞춰 임시 수준이 변동.

    - 문제 제기 및 솔루션

        - 문제 난이도의 부적확성

            - 사용자의 수준에 맞춘 정답률 계산 시, 같은 난이도의 문제라도 정답률 분포에 큰 차이가 발생.
            - 사용자의 수준별 정답률을 바탕으로 문제 난이도를 재배치하여 알고리즘의 정확도를 향상시킴.

        - 후반부 문제에 대한 과도한 의존성
            - 기존 알고리즘이 후반부 문제의 정답 여부에 지나치게 의존함.
            - 임시 수준 변동에 가중치를 부여하여, 후반부 문제로 갈수록 가중치를 줄임으로써 문제를 해결함.

#### 성과

- 특허 출원
    - 빅데이터 기반 학습자 맞춤형 외국어 레벨 측정 시스템 (출원번호: 1020210035794)
    - 맞춤형 외국어 문제선정 시스템 (출원 번호: 1020210035829)

</details>


## 🏆 Awards
- [삼성 청년 SW아카데미 성적우수상](/assets/pdf/awards/sec-team.pdf)  - *삼성전자 주식회사 (2024)*
- [2023 Dean's List](/assets/pdf/awards/dean.pdf) *- DGIST (2023)*


## 📃 Certificates
- [SW Certificate Professional]() - *삼성전자 주식회사 (2024)*
