# node-school
> 전국 초, 등, 고등학교 및 병설유치원 정보 파싱 모듈

전국 교육청 학생 서비스 페이지(stu.xxx.go.kr)를 파싱하여 이번 달 **학사일정**과 **급식표**를 Json 형태의 데이터로 제공합니다.

## 설치하기
 - npm 업로드 예정
 - 본 소스코드의 school.js, src/meal.js, src/notice.js, data/data.js 파일을 사용할 프로그램 폴더에 추가합니다.

## 사용 예시

#### 비동기 함수 방식

```javascript
/* 모듈 불러오기 */
const School = require('../school.js') 

/* 객체 생성 */
const school = new School()

/* 아래 예제는 경기도의 광명경영회계고등학교를 기준으로 함 */
school.init(school.eduType.high, school.region.gyeonggi, 'J100000488')

/* 비동기 함수 방식 예제 */
const sampleAsync = async function() {
  console.log('[이번 달 급식 정보 - Async]\n')
  console.log(await school.getMeal())

  console.log('\n\n\n')

  console.log('[이번 달 학사일정 - Async]\n')
  console.log(await school.getNotice())
}

sampleAsync()

```

#### 프라미스 방식

```javascript
/* 모듈 불러오기 */
const School = require('../school.js') 

/* 객체 생성 */
const school = new School()

/* 아래 예제는 경기도의 광명경영회계고등학교를 기준으로 함 */
school.init(school.eduType.high, school.region.gyeonggi, 'J100000488')

/* 프라미스 방식 예제 */
const samplePromise = function() {
  school.getMeal().then(result => {
    console.log('[이번 달 급식 정보 - Promise]\n')
    console.log(result)
    return school.getNotice()
  }).then(result => {
    console.log('\n\n\n')
    console.log('[이번 달 학사일정 - Promise]\n')
    console.log(result)
  })
}

samplePromise()

```

#### 반환되는 json 데이터 형식
``` javascript
// 급식 데이터
{
    '1': '[중식][중식]\n발아현미밥\n미역국5.6.9....',
    '2': '[중식]\n얼갈이된장무침5.6.\n칼슘찹쌀....',
    '3': '[중식]\n투움바파스타(주식)1.2.5.6.9.13.15.\n....',
    '4': '',
    '5': '',
    ...
    'month': 5,
    'day': 3,
    'today': '[중식]\n투움바파스타(주식)1.2.5.6.9.13.15.\n....'
}


// 학사일정
{
    '1': '',
    '2': '',
    '3': '',
    '4': '개교기념일',
    '5': ''
    '6': ''
    '7': '대체공휴일',
    ...
    'month': 5
}
```
## 사용 방법

### School 인스턴스 생성
`school.js` 모듈을 불러와서 인스턴스를 생성합니다. <br>
생성 후 반드시 init()를 호출하여 원하는 학교로 초기화합니다.
```javascript
const School = require('./school.js')
const school = new School()

/* 
* @param type: 학교 유형(초, 중, 고, 병설유치원) 
* @param region: 교육청 관할 지역
* @param schoolCode: 학교 고유 코드
*/
school.init(type, region, schoolCode)
```

#### 학교 종류

 학교 종류는 생성한 인스턴스의 `eduType` 에서 선택할 수 있습니다.
```javascript
const School = require('./school.js')
const school = new School()

/* 출력: 4 */
console.log(school.eduType.high)
```
- 병설유치원: `kindergarden` [1]
- 초등학교: `elementary` [2]
- 중학교: `middle` [3]
- 고등학교: `high` [4]

#### 교육청 지역

 지역은 생성한 인스턴스의 `region` 에서 선택할 수 있습니다. 
```javascript
const School = require('./school.js')
const school = new School()

/* 출력: stu.sen.go.kr */
console.log(school.region.seoul)
```
- 서울: `seoul`  [stu.sen.go.kr]
- 인천: `incheon`  [stu.ice.go.kr]
- 부산: `busan` [stu.pen.go.kr]
- 광주: `gwangju` [stu.gen.go.kr]
- 대전: `daejeon` [stu.dge.go.kr]
- 대구: `deagu` [stu.dge.go.kr]
- 세종: `sejong` [stu.sje.go.kr]
- 울산: `ulsan` [stu.use.go.kr]
- 경기: `gyeonggi` [stu.goe.go.kr]
- 강원: `kangwon` [stu.kwe.go.kr]
- 충북: `chungbuk` [stu.cbe.go.kr]
- 충남: `chungnam` [stu.cne.go.kr]
- 경북: `gyeongbuk` [stu.gbe.go.kr]
- 경남: `gyeongnam` [stu.gne.go.kr]
- 전북: `jeonbuk` [stu.jbe.go.kr]
- 전남: `jeonnam` [stu.jne.go.kr]
- 제주: `jeju` [stu.jje.go.kr]

#### 학교 코드

학교 고유 코드는 [여기](https://www.meatwatch.go.kr/biz/bm/sel/schoolListPopup.do)에서 학교명으로 검색할 수 있습니다.
 학교 코드는 `X000000000` 형식의 10자리 문자열입니다.

## 문제 신고
교육청 홈페이지의 리뉴얼 등의 문제로 파싱이 불가능 할 수 있습니다. [이슈](https://github.com/leegeunhyeok/node-school/issues)를 남겨주시면 최대한 빠르게 수정하여 반영하도록 하겠습니다.

## 라이센스
[MIT](https://github.com/agemor/school-api/blob/master/LICENSE)


## 알림
본 프로젝트는 [School API](https://github.com/agemor/school-api)를 참고하여 Node.js 전용으로 새로 포팅한 프로젝트입니다.
