# 리스트 자료형

* 리스트

  변할수도 있는 데이터들을 나란히 묶어주는 자료형

  리스트는 대괄호

* 튜플

  변하면 안되는 데이터들을 묶어주는 자료형

  튜플은 소괄호

* **딕셔너리 자료형(중요!)**

  대응이 되는 데이터를 표현해주는 자료형

  "우리는 **Key** 를 통해 **Value**를 얻는다"

  **탐색의 기준, 키워드 = "Key"**

  **탐색의 기준에 대응되는 , 찾고자 하는 값 = "Value"**

  - 딕셔너리 : Code 표현

  ```
  {Key1:Value1, Key2:Value2,....}
  ```

  ​	key는 중복되서도, 변해서도 안된다.



# 문자열 실습 & 내장함수

* index(인덱스)

  문자열 하나하나에 번호를 매긴 것

* 문자열 길이 : len(문자열 변수)

  ex) print(len(str))

* 문자열 내에서 특정 문자의 증장 횟수 : 문자열 변수, count( ' 특정문자 ' )

  ex) print(str.count('a'))

* 문자열을 (특정기준으로) 나누기 : 문자열 변수.split()

  ex) print(str.split(" ")) -->  공백을 기준으로 나눈다.

# 리스트 실습 & 내장함수

* 리스트의 길이를 구해주는 함수 : len(리스트변수)

  ex)   li = [1,2,3] 

  ​		len(len(li))

* 리스트 원소 오름차순 정렬해주는 함수 : 변수.sort()

li = [3 ,1, "a" , 5]

* 리스트 내의 특정 원소 인덱스 반환해주는 함수 : . index(요소)

   ex) li.index("a")

* 리스트 내의 특정 원소릐 갯수 세기 : .count(요소)

  ex) li.count(2)

# 딕셔너리실습 & 내장함수

pairs = {'방탄' : 'DNA', '소히' : '산책'}

* 하나의 key-value 쌍을 추가하는 방법

  * **딕셔너리형 변수[key] = value**

    ex) pairs['스탠딩에그'] = '휴식'

    출력 => **paris = {'방탄' : 'DNA', '소히' : '산책', '스탠드에그' : '휴식'}**

  

* 특정 key-value 삭제하는 방법 : del 함수

  * **del 변수[key]**

    ex) del pairs['방탄']

    출력 => **paris = {'소히' : '산책', '스탠드에그' : '휴식'}**

* key로 value 얻기 : **변수.get(key)**

  ex) pairs.get('산책')

  출력=> **소히**





