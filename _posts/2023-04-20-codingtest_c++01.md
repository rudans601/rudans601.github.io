---
layout: single
title: "C++/python 자료구조 -리스트와 딕셔너리(순차 컨테이너와 연관 컨테이너),스택,큐,데크"
categories: codingtest_C++/python
tags: [c++,python,codingtjest]
author_profile: false
#search: false
---

# 리스트(순차 컨테이너)

## list() - 파이썬

### 요약

파이썬에선 리스트를 사용하면 스택을 사용할지, 큐를 사용할지 고민하지 않아도 되며, 스택과 큐에 사용 가능한 모든 연산을 함께 제공한다.

|      연산      | 시간 복잡도 |                             설명                             |
| :------------: | :---------: | :----------------------------------------------------------: |
|     len(a)     |    O(1)     |                 전체 요소의 개수를 리턴한다                  |
|      a[i]      |    O(1)     |                  인덱스 i의 요소를 가져온다                  |
|     a[i:j]     |    O(k)     | 인덱스 i부터 j-1까지 슬라이스의 길이만큼인 k개의 요소를 가죠온다. 이 경우 객체 k개에 대한 조회가 필요하므로 O(k)이다 |
|   elem in a    |    O(n)     | elem 요소가 존재하는지 확인한다. 처음부터 순차 탐색하므로 n만큼 시간이 소요된다 |
| a.count(elem)  |    O(n)     |                  elem요소의 개수를 리턴한다                  |
| a.index(elem)  |    O(n)     |                 elem요소의 인덱스를 리턴한다                 |
| a.append(elem) |    O(1)     |             리스트 마지막에 elem요소를 추가한다              |
|    a.pop()     |    O(1)     |        리스트 마지막 요소를 추출한다. 스택의 연산이다        |
|    a.pop(0)    |    O(n)     | 리스트 첫번째 요소를 추출한다. 큐의 연산이다. 이 경우 전체 복사가 필요하므로 O(n)이다. 나중에 다시 살펴보겠지만 큐의 연산을 주로 사용한다면 리스트보다는 O(1)이 가능한 데크를 권장한다. |
|    del a[i]    |    O(n)     |            i에 따라 다르다. 최악의 경우 O(n)이다.            |
|   a.sort( )    | O(n log n)  | 정렬한다. 팀소트를 사용하며 최선의 경우에도 O(n)에도 실행될 수 있다. |
| min(a), max(a) |    O(n)     | 최솟값/최댓값을 계산하기 위해서는 전체를 선형 탐색해야 한다. |
|  a.reverse( )  |    O(n)     | 뒤집는다. 리스트는 입력 순서가 유지되므로 뒤집게 되면 입력 순서가 반대로 된다. |

### 사용 방법

#### 리스트 생성

```python
a = list() #기본 선언방식
a = [ ] #간단하게
a = [1,2,3] #초기값을 지정해 선언 가능, 요소끼리 다른 자료형도 추가 가능
```

#### 리스트 요소 추가

* append( )

  리스트의 제일 뒤에 요소 추가

  ```py
  a.append(4) #[1,2,3,4]
  ```

* insert( )

  특정 위치의 인덱스를 지정해 요소 추가

  ```py
  a.insert(3,5) #3번째 인덱스에 5를 추가 -> [1,2,3,5,4]
  ```

#### 리스트 요소 찾기(슬라이싱)

파이썬 인덱스는 0부터 시작

```python
#a = [1,2,3,5,4]
a[3] #5 반환
a[1:3] #인덱스 1부터 3 이전까지 -> [2,3] 반환
a[:3] #처음부터 3 이전까지 -> [1,2,3] 반환
a[4:] #인덱스 4부터 마지막까지 -> 5 반환
a[1:4:2] #세번째 파라미터는 몇 칸씩 건너뛸지 여부이다 -> [2,5] 반환
```

#### 리스트 요소 삭제

* del

  특정 위치의 인덱스로 삭제하기

  ```py
  a = [1,2,3,5,4]
  del a[1] #인덱스 1에 있는 2 삭제 -> [1,3,5,4]
  ```

* remove( )

  값으로 삭제하기

  ```py
  a.remove(3) #값이 3인 요소 삭제 -> [1,5,4]
  ```

* pop( )

  스택의 팝 연산과 비슷하다. 인덱스를 작성하지 않으면 가장 마지막 요소를 반환 후 삭제하고, 인덱스를 작성하면 그 인덱스 값을 리턴하고 삭제된다.

  ```py
  a = [1,2,3,5,4]
  a.pop() #마지막 인덱스를 반환하고 삭제 -> 4 반환 후 [1,2,3,5]
  a.pop(3) #인덱스 3을 반환하고 삭제 -> 5 반환 후 [1,2,3]
  ```

  

## 순차컨테이너-c++

### 요약

#### 순차 컨테이너 종류

* vector

  가변 크기 배열

  장점 : 빠른 접근 지원(인덱스)

  단점 : 끝 이외에서 요소를 삽입하거나 삭제하면 느려짐

* deque

  끝이 양쪽인 큐

  장점 : 빠른 접근 지원(인덱스), 처음 또는 끝에서 삽입/삭제가 빠르다

  단점 : 가운데에 요소를 추가하거나 이동하면 느려짐

* list

  이중 연결 리스트

  장점 : 모든 지점에서 삽입/삭제가 빠르다

  단점 : 양방향 순차 접근만 지원함

* forward_list

  단일 연결 리스트

  장점 : 모든 지점에서 삽입/삭제가 빠르다

  단점 : 단방향 순차 접근만 지원함, size연산이 없다

* array

  고정 크기 배열

  장점 : 빠른 접근 지원(인덱스), 내장 배열보다 안전하고 사용하기 쉬움

  단점 : 요소를 추가하거나 제거할 수 없다, 배열 크기를 변경할 수 없음

* string

  문자를 담는 특별한 컨테이너, vector와 비슷

  장점 : 빠른 접근 지원(인덱스), 끝에서 삽입 삭제 빠름

  단점 : 끝 이외에서 요소를 삽입하거나 삭제하면 느려짐



### 사용 방법

#### 사용할 순차 컨테이너 결정하기

사용할 컨테이너를 선택할 때 다음 원칙을 고려해볼 수 있다.

* 다른 컨테이너를 사용할 이유가 없으면 vector를 사용한다
* 프로그램에 크기가 작은 요소가 많고 공간에 대한 부담이 중요하다면 list나 forward_list는 사용하지 않는다
* 프로그램에서 인덱스로 요소를 접근해야 한다면 vector나 deque를 사용한다
* 프로그램에서 컨테이너 가운데에 요소를 삽입하거나 삭제해야 하면 list나 forward_list를 사용한다
* 프로그램에서 처음과 끝에서만 요소를 삽입하거나 삭제하고 가운데에서는 하지 않는다면 deque를 사용한다.
* 프로그램에서 입력을 읽는 동안에만 컨테이너 가운데에 요소를 삽입하고 그 이후에는 요소에 임의 접근해야 한다면
  * 먼저 실제로 컨테이너 가운데에 요소를 추가해야 하는지 결정한다. 입력을 마쳤을 때 컨테이너 내용을 재정렬하기 위해 vector에 추가한 다음 sort 함수를 호출하는 것이 더 쉽다
  * 반드시 가운데에 삽입해야 하면 입력하는 동안에는 list사용을 고려한다. 입력을 마치면 list를 복사해 vector에 넣는다

#### 헤더

일반적으로 각 컨테이너는 해당 타입과 같은 이름인 헤더 파일에 정의한다. deque는 deque 헤더, list는 list 헤더에 정의하는 식이다. 

#### 순차 컨테이너 생성

컨테이너종류 <타입> 이름 순으로 선언, 크기와 요소 값으로 초기화 할 수도 있다.

```c++
vector <const char*> articles = {"a", "an", "the"};
list<string> authors = {"Milton","Shakespeare","Austen"};
list<int> num; //빈 공간도 가능
array<int,42> ia1 // int를 42개 담는 array, 기본 초기화
//크기와 요소 초기값으로 초기화 할 수도 있다.
vector<int> ivec(10,-1); //int 요소 10개, 각각은 -1로 초기화한다.
forward_list<int> ivec(10); //int 요소 10개, 각각은 0으로 기본 초기화한다.
```

#### 반복자

반복자는 순차, 연관 컨테이너 위치를 나타내는 변수의 일종이다.

반복자는 const_iterator와 그냥 iterator가 있다. 컨테이너가 const이면 반복자도 const적용되고 const가 아니면 반복자의 const에 따른다

```c++
list<string> a = {"Milton","Shakespeare","Austen"};

list<string>::iterator it5; //it5는 list<string>타입의 반복자이다.
list<string>::iterator it6 = a.begin(); //list a의 시작점을 반환한다.
auto it7 = a.cend(); //auto를 사용해도 된다
```

#### 대입/swap

컨테이너의 종류와 요소 타입이 같으면 대입이 가능하다.

```c++
c1 = c2; //c1 내용을 c2 요소로 복사한다.
list<string> list2 (authors); //authors는 list2와 컨테이너 종류와 요소 타입이 같다.
```

##### assign

assign은 컨테이너의 두 요소의 타입이 달라도 변환이 가능하면 복사가 가능하다.

```c++
list<string> names;
vector<const char*> oldstyle;
names = oldstyle; //오류 : 컨테이너 타입이 일치하지 않는다
names.assign(oldstyle.cbegin(), oldstyle.cend()); //타입이 변환 가능하므로 복사, 단 반복자 두개로 범위를 지정해야 함
```



swap는 두 컨테이너의 요소를 교체하는 것이다. 교체는 요소를 복사하는 것보다 훨씬 더 빠르다(상수 시간 보장)

```c++
vector<int> c1(10); //요소가 10개인 vector
vector<int> c2(24); //요소가 24개인 vector
swap(c1,c2); //이걸 주로 사용하는걸 추천
c1.swap(c2); //이 방식도 가능
```

#### 크기/상등,관계연산자

size( )함수는 요소의 개수를 반환한다.

empty( )함수는 크기가 0이면 true, 크기가 1이면 false를 반환한다. forward_list에서는 지원하지 않는다

Max_size는 해당 타입 컨테이너에서 담을 수 있는 요소 수보다 크거나 같은 수를 반환한다.

```c++
bool tof = c1.empty();
```

상등연산자(==, !=)와 관계연산자(>,<,>=,<=)도 지원한다. 단, 반드시 컨테이너 타입과 요소 타입이 같아야 한다. 그리고 클래스 객체가 요소인 경우 객체끼리 연산이 정의 돼있어야 가능하다.

#### 요소 추가

* push_back( )은 array와 forward_list를 제외한 모든 순차 컨테이너에서 끝에 요소를 추가한다. size가 1 증가한다.

  ```c++
  vector<string> container;
  string word = "hi";
  container.push_back(word);
  ```

* push_front( )는 list, forward_list,deque 컨테이너에서 처음에 새 요소를 추가한다.

  ```c++
  list<int> ilist; 
    ilist.push_front("aa");
  ```

* insert( )는 원소 0개 이상을 컨테이너 내 어느 위치든 추가할 수 있다. 반복자로 나타내는 위치 앞에 요소를 삽입한다. vector, deque, list, string에서 지원하고 forward_list에서는 이 멤버의 특수화 버전을 제공한다. insert는 첫번째 반복자를 리턴한다.

  ```c++
  slist.insert(iter, "Hello!"); //iter 바로 앞에 "Hello!"를 삽입한다.
  slite.insert(iter,10,1); //반복자 iter앞에 값이 1인 요소를 10개 추가한다.
  slite.insert(iter1,iter2,iter3); //반복자 iter1로 나타내는 요소 앞에 반복자 iter2와 iter3로 나타내는 범위의 요소를 참조하는 반복자를 반환한다.
  slite.insert(iter,{0,1,2,3,4}); //iter 앞에 중괄호로 둘러싼 값을 삽입한다.
  //반복자에 slite.begin() 등등을 넣어도 된다.
  ```

* 클래스 객체 요소 추가 함수 (emplace_front, emplace, emplace_back)

  ```c++
  //인자가 3개인 Sales_data 클래스의 생성자를 사용해 c 끝에 Sales_data 객체 생성
  c.emplace_back("978-0590353403", 25, 15.99);
  //활용법
  c.push_back(Sales_data("978-0590353403", 25, 15.99));
  ```

#### 요소 접근

```c++
//기존 방식 : 첨자 사용(string, vector, deque, array에만 유효)
c[1];
//반복자 방식 : 반복자에 역참조 연산자를 쓰면 반복자가 가리키고 있는 값을 반환한다.
auto val = *c.begin(), val2 = c.front();
auto last = c.end();
auto val3 = *(--last); //가장 마지막 요소를 가져오려면 end()에서 반환한 반복자를 감소 후 역참조 해야 한다. *(--(c.end()))

//요소 접근 후 변경할려면 auto만 선언하지 말고 auto 참조자로 선언 해야 한다
auto &v = c.back();
v = 1024;
```

#### 요소 삭제

* pop_front( )

  처음 요소를 제거한다.

  ```c++
  ilist.pop_front();
  ```

* pop_back( )

  마지막 요소를 제거한다

  ```c++
  ilist.pop_back();
  ```

* erase( )

  반복자로 지정한 요소 하나 또는 반복자 쌍으로 표시한 요소 범위를 제거할 수 있다. 제거 한 요소 바로 다음 위치를 참조하는 반복자를 반환한다.

  ```c++
  //하나씩 삭제
  list<int> lst = {0,1,2,3,4,5,6,7,8,9};
  auto it = lst.begin(); //시작 지점을 반복자로
  while(it != lst.end())
    if(*it % 2) //그 요소가 홀수이면
      it = lst.erase(it); //이 요소를 삭제한다
  	else
      ++it; //반복자를 증가시킨다
  
  //여러개 삭제
  elem1 = slist.erase(elem1, elem2); //elem1, elem2 둘 다 반복자
  ```

  

* clear( )

  컨테이너 내 모든 요소를 삭제한다

#### 

#### forward_list 연산

forward_list에 있는 추가 연산자는 insert, emplace, erase를 사용하지 않는다. 대신 아래의 연산자를 사용한다. 

* insert_after( )

  반복자가 가리키는 요소 다음에 요소를 추가한다.

  ```c++
  forward_list<int> flst = {0,1,2,3,4,5,6,7,8,9};
  auto prev = flst.before_begin(); //처음 요소보다 더 앞을 가리키는 반복자
  flst.insert_after(prev,10); //제일 앞에 10을 추가한다.
  
  prev = flst.before_begin(); 
  flst.insert_after(prev,5,10); //제일 앞에 10을 5개 추가
  
  prev = flst.before_begin(); 
  flst.insert_after(prev,flst.begin(),flst.end()); //제일 처음부터 끝까지 복사 후 제일 앞에 추가
  
  prev = flst.before_begin(); 
  flst.insert_after(prev,{11,12}); //제일 앞에 11, 12 추가
  ```

  

* emplace_after( )

  반복자가 가리키는 요소 다음에 요소를 생성한다. 새 요소에 대한 반복자를 반환한다.

  ```c++
  emplace_after(prev,Sales_data("a","b")); //Sales_data객체를 prev 바로 뒤에 객체를 추가한다.
  ```

  

* erase_after( )

  반복자가 가리키는 요소 다음 요소를 삭제한다.

  ```c++
  flst.erase_after(prev); //제일 앞의 요소 삭제
  flst.erase-after(prev,flst.end()) //제일 앞부터 제일 뒤까지 요소 삭제
  ```

추가적인 연산자

* Before_begin( ),cbefore_begin( )

  목록 처음 요소 바로 앞의 존재하지 않는 요소를 나타내는 반복자. 이 반복자는 역참조하면 안된다. 반복자를 반환한다.

# 딕셔너리(연관 컨테이너)

## 딕셔너리 - 파이썬

딕셔너리는 키/값 구조로 이루어진 컨테이너이다. 딕셔너리는 문자를 포함해 다양한 타입을 키로 사용할 수 있다. 숫자, 문자, 집합까지 가능하다.

### 요약

|      연산      | 시간복잡도 |                설명                 |
| :------------: | :--------: | :---------------------------------: |
|     len(a)     |    O(1)    |       요소의 개수를 리턴한다        |
|     a[key]     |    O(1)    |     키를 조회하여 값을 리턴한다     |
| a[key] = value |    O(1)    |          키/값을 삽입한다           |
|    key in a    |    O(1)    | 딕셔너리에 키가 존재하는지 확인한다 |

### 사용 방법

#### 딕셔너리 선언

```python
a = dict() #기본적인 선언
a = {} #더 간단하게 선언
a = {'key' : 'value1', 'key2':'value2'}
```

#### 딕셔너리 찾기

```python
a['key1'] #value 출력
a['key2'] = 'value3' #key2에 value3값 저장
```

존재하지 않는 키를 조회할 경우 KeyError가 발생한다.

#### 딕셔너리 활용

키/값은 for 반복문으로도 조회가 가능하다 item()메소드를 사용하면 된다

```python
for k,v in a.items():
  print(k,v)
```

#### 딕셔너리 삭제

딕셔너리 삭제는 del을 이용한다. 키값을 입력해야 한다.

```python
del a['key1']
```

### 딕셔너리 모듈(추가기능)

* defaultdict 객체

  존재하지 않는 키를 조회할 경우, 여러 메세지를 출력하는 대신 디폴트 값을 기준으로 해당 키에 대한 딕셔너리 아이템을 생성해준다

  ```python
  a = collections.defaultdict(int)
  a['A'] = 5
  a['B'] = 4 #a 딕셔너리에 'A'/5값과 'B'/4값 추가
  ```

* Counter 객체

  아이템에 대한 개수를 계산해 딕셔너리로 리턴한다. 숫자가 키값이 되고 값은 개수로 만들어진다.

  ```python
  a = [1,2,3,4,5,5,5,6,6]
  b = collections.Counter(a)
  b # Counter({5:3, 6:2, 1:1, 2:1, 3:1, 4:1 })
  ```

  Counter 객체에서 빈도수가 가장 높은 요소는 most_common()을 사용하면 된다.

  ```python
  b.most_common(2) #[(5,3),(6,2)]
  ```

  

* OrderedDict 객체

파이썬 3.6 버전에서는 딕셔너리에 값을 차례대로 입력 해도 그 순서대로 저장된다는 보장이 없었다 그래서 orderedDict객체를 사용하면 입력 순서가 유지되는데 파이썬 3.7버전부터는 자체적으로 인덱슬르 이용하여 입력 순서가 유지되도록 개선됐다. 

원래 해시테이블은 입력 순서에 관여하지 않는 자료형인 망큼, 무턱대고 딕셔너리로 입력 순서를 기대하는 것은 매우 위험하며 권장하지도 않는 방법이다.

```python
collections.OrderedDict({'banana' : 3, 'apple' : 4, 'pear' : 1, 'orange' : 2})
```



## 연관 컨테이너 - C++

연관 컨테이너도 파이썬의 딕셔너리 처럼 키-값 쌍을 가지고 있다 연관 컨테이너는 map과 set이 있다. map에서 키는 색인 역할을 하고 값은 그 색인에 연관된 데이터를 나타내고, set은 키만 담는다. 그러므로 지정한 키가 존재하는지 여부를 조회할 경우에만 효율적이다.

### 연관 컨테이너 종류

(1)각 컨테이너는 set또는 map이고

(2)키가 유일해야 하거나 다중 키를 허용하며 (multi)

(3)요소는 순서대로 또는 순서 없이 저장한다.(unordered)

map과 multimap은 map헤더에서 정의하고 set과 multiset타입은 set헤더에서 정의하며, 순서 없는 컨테이너는 unordered_map과 unordered_set 헤더에서 정의한다. 

* 요소를 키 순서로 정렬

  |   이름   |              설명               |
  | :------: | :-----------------------------: |
  |   map    | 연관 배열이며 키-값 쌍을 담는다 |
  |   set    |       키가 값인 컨테이너        |
  | multimap | 키가 여러번 나타날 수 있는 map  |
  | multiset | 키가 여러번 나타날 수 있는 set  |

* 키 순서 없음

  |        이름        |                   설명                   |
  | :----------------: | :--------------------------------------: |
  |   unordered_map    |      해시 함수를 사용해 구성한 map       |
  |   unordered_set    |      해시 함수를 사용해 구성한 set       |
  | unordered_multimap | 해시 map이며 키는 여러 번 나타날 수 있다 |
  | unordered_multiset | 해시 set이며 키는 여러번 나타날 수 있다  |

#### 연관 컨테이너 정의

* map

  ```c++
  map<string,size_t> word_count; //string을 size_t에 연관짓는 빈 map
  
  //map<string,string> authors = {
  //{"Joyce", "James"}, {"Austen", "Jane"},{"Dickens","Charles"}}; 주석 제거
  string word;
  while(cin >> word)
    ++word_count[word]; //해당 단어에 대한 횟수를 가져와 증가 시킨다
  
  for( const auto &w : word_count)
    cout << w.first << " occurs " << w.second << ((w.second > 1) ? "times" : "time") << endl; //w.first와 w.second는 pair타입의 키다. 이후 설명
  ```

* set

  ```c++
  //입력에서 각 단어가 나타내는 횟수를 센다
  map<string, size_t> word_count;
  set<string> exclude = {"The", "But", "And" , "Or", "An", "A", "the", "but", "and", "or", "an", "a"};
  string word;
  while(cin >> word)
  {
    if(exclude.find(word) == exclude.end()) //find는 반복자를 반환하는데 word 단어가 exclude에 있으면 그 반복자를 반환하고, 없으면 끝 지난 반복자를 반환한다.
      ++word_count[word];
  }
  ```

* multimap

  ```c++
  multimap<int,string> mmap(ivec.cbegin(),ivec.cend()); //mmap에 키값이 중복인 map 만들기
  ```

  

* multiset

  ```c++
  multiset<int> mset(ivec.cbegin(),ivec.cend());
  ```

  

#### pair타입

연관 컨테이너에 사용하는 타입 중 하나로, pair는 두 데이터 멤버를 담는다. 두 타입은 같지 않아도 된다

연관컨테이너에 반복자를 역참조하면 

```c++
pair<string, string> anon; //두 string을 담는다
pair<string, vector<int>> line; //string과 vector<int>를 담는다
pair<string, string> author = {"James","Joyce"}; //초기값 지정
author.first; //James
author.second //Joyce
```

##### pair 객체를 생성하는 함수

```c++
pair<string, int> process(vector<string> &v)
{
  if(v.empty())
    return {v.back(), v.back().size()}; //목록 초기화
  else
    return pair<string, int>(); //반환 값을 명시적으로 생성한다.
}
//또는 두 인자를 사용해 적절한 타입의 pair를 새로 생성하도록 make_pair를 사용할 수 있다.
if(v.empty())
    return make_pair(v.back(), v.back().size()); //타입은 auto처럼 자동 추론
```

#### 연관 컨테이너 반복자

연관 컨테이너의 반복자를 역참조할 수 있다.

```c++
auto map_it = word_count.begin(); //word_count map에 대한 반복자
cout << map_it->first; //이 요소에 대한 키를 출력한다
cout << " " << map_it->second; //해당 요소의 값을 출력한다
map_it->first = "new key"; //오류 : 키 값은 const라 바꿀 수 없다
++map_it->second; //좋음 : 반복자로 값을 바꿀 수 있다
```



#### 연관 컨테이너 요소 추가(insert)

map과 set에 요소 하나 또는 요소 범위를 추가한다. 일반 map과 set은 유일키를 담으므로 이미 존재하는 요소를 삽입하는 것은 아무 영향이 없다

* Map

  ```c++
  word_count.insert({word,1});
  word_count.insert(make_pair(word,1));
  word_count.insert(pair<string,size_t>(word,1));
  word_count.insert(map<string,size_t)::value_type(word,1));
  ```

* set

  ```c++
  vector<int> ivec = {2,4,6,8,2,4,6,8}; //ivec에는 요소가 8개다
  set<int> set2;
  set2.insert(ivec.cbegin(), ivec.cend()); //set2에는 요소가 4개가 추가됐다. 2,4,6,8
  set2.insert({1,3,5,7,1,3,5,7}); //set2에 1,3,5,7 요소가 추가 돼 8개이다.
  ```

반환값 second가 true이면 추가 성공, false이면 추가 실패

#### 연관 컨테이너 요소 삭제(erase)

```c++
set2.erase(3); //set2에서 키가 3인 요소를 모두 제거하고 제거한 요소 수를 나타내는 size_type을 반환한다.
set2.erase(iset); //iset반복자가 가리키는 요소를 제거한다.
set2.erase(iset1,iset2); //iset1와 iset2가 가리키는 범위의 요소들을 제거한다
```

반환값이 0이면 삭제하지 못한 것이고 1이면 삭제 된 것이다.

#### 연관 컨테이너 첨자 연산

```c++
word_count["Anna"] = 1;
```



#### 순서 없는 연관 컨테이너

# 데크

## deque - 파이썬

* append( )

  마지막에 원소를 추가한다

* appendleft( )

  첫번째에 원소를 추가한다

* pop( )

  마지막 원소를 제거하고 그 값을 반환한다.

* popleft( )

  첫번째 원소를 제거하고 그 값을 반환한다.
