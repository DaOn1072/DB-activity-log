<h2> 📃 DB 학습 활동 기록 📃 </h2>

단순히 문제를 풀기 위해 SQL문을 작성하는 것이 아닌, 데이터가 주어졌을 때 그 안에 얼마나 가치있는 정보값을 가져올 수 있는지 고민합니다. </br>
</br>
해당 프로젝트는 데이터를 직접 입렵하고, 한정된 데이터 안에서 필요한 정보가 무엇인지 쿼리문 작성 후 풀었습니다. 
<br>
</br>
<table>
  <tr>
    <td>
      <table>
        <tr>
          <th>개체(Entity)</th>
          <th>관계(Relationship)</th>
        </tr>
        <tr><td>student(snum, sname, year, QPA)</td><td>enrol(snum, cnum, grade)</td></tr>
        <tr><td>professor(pnum, pname, ppos, pphone)</td><td>lecture(pnum, cnum, time, room)</td></tr>
        <tr><td>department(dnum,dname, dphone, dloc)</td><td>advise(snum, pnum)</td></tr>
        <tr><td>course(cnum, cname, hrs, credit</td><td>major(snum, dnum)</td></tr>
        <tr><td></td><td>belong(pnum, dnum)</td></tr>
      </table>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/c8242a44-4ae4-4a2a-8161-03098276004c" alt="설명" width="800" />
    </td>
  </tr>
</table>




<h2></h2>

<h3> ❕ 데이터 입력 설정 ❕ </h3>
</br>
<details>
<summary>📝 DEPARTMENT(학과) </summary>
  <h2></h2>
<div markdown="1">

- 스마트it과(3), 식품영양과(3), 유아교육과(3), 섬유패디과(2), 문예창작과(2) 총 5개의 학과를 선정하므로 5개의 카디널리티가 생성된다.
- dloc 설정 시 앞 2자리의 건물번호, 뒤 3자리 호실번호로 설정한다.
- dnum과 PROFESSOR의 belong은 같은 값이 들어간다.

</div>
</details>

<details>
<summary>📝 COURSE(강의) </summary>
  <h2></h2>
<div markdown="1">

- 각 학년마다 3과목이 개설되고 각 학년마다 2개의 반으로 구성된다. 
  </br></br>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 3년제 학과: 3학년 * 3과목 * 2반 = 18과목</BR>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 2년제 학과: 2학년 * 3과목 * 2반 = 12과목</BR>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 18 * 3 + 12 * 2 = 78이므로, 총 78개의 카디널리티가 생성된다.
    <h2></h2>
- cnum 설정시 1, 2번째자리 개설 번호, 3번째 수강학년 번호, 4번째 해당 학기의 과목번호, 5번째 A, B 각 반을 나타내는 1, 2로 설정한다.
- hrs와 credit은 해당 강의 시간과 학점이 다른 경우가 있으므로 따로 구분해 생성한다.
</div>
</details>

<details>
<summary>📝 PROFESSOR(학과) </summary>
  <h2></h2>
<div markdown="1">

- 3년제 학과의 교수는 9명, 2년제 학과의 교수는 6명| 3 * 9 + 2 * 6 = 39이므로 총 39개의 카디널리티가 생성된다.
- PROFESSOR의 ppos 설정 시 1번째자리 직급 (정교수 1, 부교수 2, 조교수3, 전임강사 4) 2번째 호부 (1~9),
  </br>  전임강사는 실제 데이터베이스에 표현하지 않을 것으로 설정한다.
  </br>
- dphone 설정 시 학과 전화번호가 0으로 끝나므로 앞 3자리는 학과번호와 같되, 교수번호 마지막 자리에 1에서 9까지의 숫자를 할당한다.
  </br> 단, 2년제일 경우 1에서 6을 할당한다.
- 3년제 학과의 교수는 9명, 2년제 학과의 교수는 6명이지만 각 반 수는 6, 4이다.
  </br> 즉, 모든 교수가 다 지도교수로 들어가는 것은 아니며, 지도교수가 아닐 경우 강의전담교수라는 것에 유의한다.

</div>
</details>

<details>
<summary>📝 STUDENT(학생) </summary>
  <h2></h2>
<div markdown="1">

- 한 반에 3명씩 들어가므로
  </br></br>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 3년제 학과: 3학년 * 2반 * 3명 = 18명</BR>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 2년제 학과: 2학년 * 2반 * 3명 = 12명</BR>
  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 18 * 3 + 12 * 2 = 78이므로 총 78개의 카디널리티가 생성된다.
    <h2></h2>
- STUDENT의 qpa는 학점의 소수 둘째자리까지 표현하도록 한다.

</div>
</details>

<details>
<summary>❗ 요구사항 </summary>
<div markdown="1">

- 학생은 한 명의 지도교수를 가진다.
- 학생은 한 학과에 속한다.
- 학생은 여러 강의를 들을 수 있고 여러 학생이 강의를 듣는다.
- 교수는 여러 과목을 수업할 수 있다.
- 교수는 한 학과에 속한다.

</div>
</details>

<h2></h2>

<h3> 🖥 SQL 쿼리문 작성 🖥 </h3>

[테이블 생성 SQL](https://github.com/DaOn1072/DB-activity-log/blob/main/%ED%85%8C%EC%9D%B4%EB%B8%94%20%EC%83%9D%EC%84%B1%20SQL%EB%AC%B8.txt) 각 테이블의 값 설정입니다.

<h2></h2>

<details>
<summary>1. 절대평가 기준으로 학점을 부여했을 때 재수강이 가능한 학생명, 강의명, 학번, 성적을 보이시오. (C 미만부터) </summary>
<div markdown="1">
</br>

- [1번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/1%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 학생이 등록한 과목을 알아야하기 때문에 학생 테이블의 키본키 학번과 등록 테이블의 외래키 학번을 조인합니다.
- 과목의 성적을 알기 위해서 과목 테이블의 기본키와 과목번호와 등록 테이블의 외래키 과목번호를 조인합니다.
- 성적이 70점 미만인 것을 찾으면, 어떤 학생이 무슨 과목에서 70점 미만으로 C 아래 성적을 받았는지 알 수 있습니다.

</div>
</details>
</br>

<details>
<summary>2. 안식년에 들어간 교수를 대신해 지도교수를 맡아줄 수 있는 지도교수가 아닌 교수의 이름과 교수번호를 보이시오. </summary>
<div markdown="1">
</br>

- [2번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/2%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 교수의 소속 학과를 알기 위해서 테이블의 학과번호와 교수 테이블의 belong 값을 조인합니다.
- SUBSTR(ppos, 1, 1)을 수행하여 앞에 숫자 직급이 3이하인 것을 찾습니다. 같은 방법으로 호봉 6 이상을 찾습니다.
- 지도교수를 제외하기 위해 NOT EXISTS를 사용하여 지도교수가 아니면서 직급과 호봉의 조건을 만족하는 교수님을 구합니다.

</div>
</details>
</br>

<details>
<summary>3. 스마트IT과에서 학과 평균 학점보다 높은 학점인 학생을 보이시오. </summary>
<div markdown="1">
</br>

- [3번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/3%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 학과 번호 중, 해당 학과번호인 것만 검색합니다.
- HAVING 절을 사용하여 학점의 검색 조건을 추가하여, 해당 평균 학점보다 높은 학점만 검색하도록 합니다.

</div>
</details>

</br>
<details>
<summary>4. 수석 학생을 알기위해, 각 학과에서 학년별 가장 학점이 높은 학생을 보이시오. </summary>
<div markdown="1">
</br>

- [4번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/4%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 같은 값끼리 그룹화될 수 있기 위해 학년과 학과번호를 GROUP BY 합니다.
- SELECT와 GROUP BY에 sname을 추가하게 될 경우 높은 학점과 관련 없이 모든 학생의 학점이 보이지 않으므로, 전체 질의에서 조건을 추가한다.
- 학과와 학년, 학점을 괄호로 묶지 않으면 각각의 데이터로 취급합니다.

</div>
</details>
</br>

<details>
<summary>5. 학점이 2.5이하이며 평균 점수가 75이하일 경우 상담을 진행해야 하므로, 일정 수준 이하인 학생을 보이시오. </summary>
<div markdown="1">
</br>

- [5번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/5%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 전공 학과를 알기 위해서 학과 테이블의 학과번호와 학생 테이블의 major를 조인합니다.
- 학생 테이블의 기본키 학번과 등록 테이블의 외래키 학번을 조인하여 학생이 등록한 과목을 알아냅니다.
- AVG 함수로 평균 점수를 구한 후, ROUND 함수를 사용하여 소수점 첫째 자리까지만 보이도록 합니다.
</div>
</details>
</br>

<details>
<summary>6. 스마트IT과의 웹페이지저작 수업이 공사로 인해 강의실을 변경해야 하므로, 옮길 수 있는 빈 강의실을 보이시오. </summary>
<div markdown="1">
</br>

- [6번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/6%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 학과의 수업은 해당 학과 건물에서만 진행하므로, 다른 학과의 강의실 번호는 필요하지 않습니다.
- 부속 질의를 통해 LIKE 연산자를 사용해 '웹페이지저작'이라는 이름의 과목을 찾고, 해당 과목의 강의 시간을 구합니다.
- NOT IN 연산자를 사용해 구한 시간은 해당 강의시간에 수업이 없으므로, 강의실이 비었음을 알 수 있습니다.
</div>
</details>
</br>

<details>
<summary>7. 스마트IT과에서 수요일 회의시간에 수업이 있어 불참하는 교수, 강의명, 강의시간을 보이시오.</summary>
<div markdown="1">
</br>

- [7번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/7%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- DISTINCT를 사용하여 교수명과  수업명의 중복을 없앱니다.
- time의 경우 앞의 숫자가 요일, 뒤에 숫자가 시작과 끝 시간을 알리므로 같은 요일이라도 뒤에 시간이 달라 중복으로 보지 않습니다.
- SUBSTR을 사용하여 time의 첫 번째 데이터 요일 숫자만 보이도록 합니다.
- time의 앞자리는 1에서 5까지 요일을 뜻하므로, 수요일을 의미하는 3으로 시작하는 time을 구합니다.
</div>
</details>
</br>

<details>
<summary>8. 성적이 상위 0.5%에 속하는 학생과 학점, 학과, 지도교수를 보이시오. </summary>
<div markdown="1">
</br>

- [8번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/8%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

</div>
</details>
</br>

<details>
<summary>9. 3년제 학과의 2학년 지도교수에게 공지전달을 위해, 해당하는 지도교수들의 학과명, 교수명, 전화번호를 보이시오.</summary>
<div markdown="1">
</br>

- [9번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/9%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- 학과번호와 교수 테이블의 belong 데이터 값을 조인합니다.
- 지도교수는 학생과 지도로 이어져있기 때문에 교수번호와 학생 테이블의 adivse 데이터 값을 조인합니다.
- year=2로 2학년 학생의 지도를 맡은 교수를 검색합니다.
- IN 연산자를 사용해 학과번호가 3년제만 있는 테이블의 학과번호와 맞는지 확인하여 2년제를 제외합니다.
</div>
</details>
</br>

<details>
<summary>10. 전과하려는 학과의 평균 학점보다 높아야 전과가 가능합니다. 만약 2년제 학과 학생들이 식품영양과로 전과한다 했을 때, 전과가 가능한 1학년 학생들을 보이시오.</summary>
<div markdown="1">
</br>

- [10번 쿼리문 답](https://github.com/DaOn1072/DB-activity-log/blob/main/%EC%BF%BC%EB%A6%AC%EB%AC%B8/10%EB%B2%88%20%EC%BF%BC%EB%A6%AC%EB%AC%B8)
<h2></h2>

- NOt IN 연산자를 사용해 1학년인 학생 중 2년제 학과에 다니는 학생을 찾습니다.
- 학과 테이블에서 이름이 식품영양과인 학과번호를 구합니다.
- 학과번호의 학점 평균을 AVG 함수를 이용하여 구한 후, 해당 평균 학점보다 높은 학생을 찾습니다.
</div>
</details>
