# BC_Basic_01
## 전화번호부 등록하기

<br/>

### 전화번호 입력받기

```
function solution(telno) {
```
telno는 -가 붙은 형태로 입력되어짐.
<br/>
Ex) 010-7388-8752
```
const tel = telno.replace(/[-]/ig,"");
```
정규표현식을 이요하여 telno의 -를 모두 제거.
<br/>


### 전화번호 필터링하기
```
const map = {
        "010": "휴대폰",
        "011": "휴대폰", "016": "휴대폰", "017": "휴대폰", "018": "휴대폰", "019": "휴대폰",
        "031": "경기", "032": "인천", "033": "강원",
        "041": "충청", "042": "대전", "044": "세종",
        "051": "부산", "052": "울산", "053": "대구",
        "054": "경북", "055": "경남",
        "061": "전남", "062": "광주", "063": "전북",
        "064": "제주"
    };
    const top = tel.substring(0, 3);
    const ext = tel.substring(tel.length - 4);
```
앞 세자리를 top으로, 뒤 네자리를 ext으로 선언
<br/>
```
if(top === '001' || top === '002') {
        if (tel.length<11 || tel.length>15) return ["국제전화", "X"];
        return ["국제전화", "O"];
    }

    if (tel.length > 11 || tel.length < 9) return failure;
    else if (tel[0] !== '0') return failure;


    if (tel[1] === '2') {
        if (tel.length !== 10) return ["서울", "X"];
        if (ext[0] === ext[1] && ext[1] === ext[2] && ext[2] === ext[3]) return ["서울", "X"];
        return ["서울", "O"];
    }
    else if (tel[1] === '1') {
        if (!map[top]) return failure;
        if (tel[2] !== '0') return ["휴대폰", "X"];
        if (tel.length === 11 && parseInt(tel[3]) % 2 === 0) return ["휴대폰", "O"];
        return ["휴대폰", "X"];
    }
    else if (map[top]) {
        if (tel.length === 10 && tel[3] === '0') return [map[top], "X"];
        return [map[top], "O"];
    }
```
### 국제전화
001/002의 경우 국제전화이며, 11자릿수 미만이거나, 15자릿수 초과인 경우 등록불가.
<br/>
### 일반전화
9자릿수 미만이거나, 11자릿수 초과인 경우 전국 기준 등록불가, 앞자리가 0으로 시작하지 않는 경우 전국 기준 등록불가
<br/>
### 휴대전화
두번째 자릿수가 1인 경우 중, map객체에 저장되지 않은 번호는 전국 기준 등록불가, 세번째 자릿수가 0이 아닌 경우 휴대폰 기준 등록불가,
<br/>
11자릿수이며 네번째 자릿수가 짝수인 경우 휴대폰 기준 등록가능, 아무것도 해당 안되는 경우, 휴대폰 기준 등록불가
<br/>
### 저장된 번호
10자릿수이며, 4번째 번호가 0인 경우는 map객체에서 해당하는 지역 기준 등록불가
<br/>
그 이외에는 map객체에서 해당하는 지역 기준 등록가능
