# 이상 (Anomaly)

Relation 처리 과정에서 불필요한 데이터 중복으로 인해 발생하는 부작용.<br/>
Relation 안에 너무 많은 속성을 표현하려고 한 것이 원인!

※Relation : 주로 Table과 같은 의미로 사용(데이터의 집합), 튜플(Tuple)과 속성(Attribute)로 구성.

### 이상(Anomaly) 현상에 의해서..

- 현실세계의 실제 값과 DB에 저장된 값이 일치하지 않는 문제 발생.
- 중복된 데이터에 대해 데이터 불일치 현상이 발생할 우려...
- 전체적인 무결성이 저하한다.

## 예시를 보며 이해하는 3가지 이상(Anomaly) 현상.

|   학번   |  이름  | 과목ID |   과목명   | 교수명 |
| :------: | :----: | :----: | :--------: | ------ |
| 20220001 | 이규현 |   A1   |  운영체제  | 홍지만 |
| 20220002 | 이도하 |   A2   |  자료구조  | 김익수 |
| 20220003 | 최다인 |   A2   |  자료구조  | 김익수 |
| 20220004 | 함인규 |   B1   | 컴퓨터비전 | 송현주 |

### **삽입 이상**

**자료를 삽입할 때 의도하지 않은 불필요한 자료까지 삽입해야만하는 구조에 의해 발생하는 현상**<br/>
새로운 학생이 생성되어서 테이블에 튜플을 추가하려고 하는데, 주목하고자 하는 학생에 대한 정보 외에도 불필요하게 과목에 대한 정보까지 추가해야하는 구조..!<br/>
만약 과목에 대한 속성을 비울 수 없다면, "미수강" 이라는 불필요한 값까지 넣어야해! (정말 이상해..)

### **갱신 이상**

**중복된 데이터 중 일부만 수정되어 데이터 모순이 일어나는 이상**<br/>
도하하고 다인이는 자료구조를 수강 중, 근데 자료구조 교수님이 김호수로 개명을 했어<br/>
도하 튜플에서만 교수명이 김호수로 변경되었다면 다인이 튜플에서는 교수명이 김익수로 그대로 남아있음! (정말 이상해..)

### **삭제 이상**

**어떤 정보를 삭제하면, 유용한 다른 정보까지 삭제되어버리는 이상**<br/>
인규가 자퇴를 한대. 테이블에서 인규 튜플이 삭제되어야하는 상황<br/>
인규에 대한 정보만 지워지면 되는데 컴퓨터비전과 송현주교수님에 대한 정보까지 사라져버리고 말아! (정말 이상해..)

### 이상 현상 방지 방법

**정규화를 사용한다!** (정규화에 대해선 나중에 알아보도록 하자.)

## Reference

- https://kosaf04pyh.tistory.com/294
- https://deep-deep-deep.tistory.com/161
- https://developer-talk.tistory.com/256
- https://1000hg.tistory.com/22
