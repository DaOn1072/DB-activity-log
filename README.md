<h2> 📃 DB 학습 활동 기록 📃 </h2>

단순히 문제를 풀기 위해 SQL문을 작성하는 것이 아닌, 데이터가 주어졌을 때 그 안에 얼마나 가치있는 정보값을 가져올 수 있는지 고민합니다. </br>
</br>
해당 프로젝트는 데이터를 직접 입렵하였으며, 한정된 데이터 안에서 가치 있는 정보를 가져오도록 작업했습니다.
<br>
</br>
<p align="center">
  <img src="https://github.com/user-attachments/assets/b1e8086d-d9da-4ff1-bead-2782452e14e2" alt="1 페이지" />
</p>
<p align="center">데이터를 한눈에 볼 수 있도록 모아둔 메인 화면</p>



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

<h2></h2>









