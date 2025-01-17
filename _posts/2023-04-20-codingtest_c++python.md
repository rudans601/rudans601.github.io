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

# 스택

## vector-c++

스택은 후입 선출 스택은 보통 vector를 쓴다

vector 라이브러리를 포함해야 한다

```c++
#include <iostream>
#include <vector>
using namespace std;
int main()
{
  vector<int> p; //빈 벡터 생성
  vector<int> v = {12,23,34,45,56,67}; //벡터에 초기 값 설정 후 초기화
  v.push_back(78); //78 요소를 뒤에다 추가 : 시간 복잡도 O(1)
  for(int a:v) //범위 for나 일반 for 사용
  {
      cout << a << endl;
  }
  cout << "------" << endl;
  v.pop_back(); //제일 뒤 요소 반환 후 삭제: 시간복잡도 O(1)
  for(auto b = v.begin();b != v.end();b++) //일반 for는 반복자를 사용해도 됨
  {
      cout << *b << endl; //반복자를 역참조 해서 값 확인
  }
}
```

* push_back("값") : 제일 뒤에 원소 추가
* pop_back() : 제일 뒤의 원소 제거
* front( ) : 제일 앞의 원소 반환
* back() : 제일 뒤의 원소 반환
* reverse(n) : n개의 원소를 저장할 위치(공간)를 예약c 합니다
* resize(n) : 크기를 n으로 변경한다
* size() : 원소의 개수를 리턴한다
* capacity() : 할당된 공간의 크기를 리턴한다

# 큐

## Queue - c++

큐는 선입선출, queue를 사용한다

queue 라이브러리를 포함해야 한다

```c++
#include <iostream>
#include <queue>
using namespace std;

int main()
{
  queue<int> temp; //빈 큐 선언
  temp.push(1); //큐에 원소 추가
  temp.push(2);
  temp.push(3);
  
  int k = temp.size();
  for(int i = 0;i < k;i++)
  {
    cout << temp.front() << '\n'; //제일 앞의 원소를 반환
    temp.pop(); //제일 앞 원소 삭제
  }
}
```

* push("값") : 큐에 원소를 추가
* pop( ) : 제일 앞의 원소를 삭제
* front( ) : 큐 제일 앞에 있는 원소를 반환
* back() : 큐 제일 뒤에 있는 원소를 반환
* empty( ) : 큐가 비어 있으면 true, 아니면 false를 반환
* size( ) : 큐 사이즈를 반환

# 데크

## deque - c++

데크는 양쪽에서 끝나는 큐이다. 양쪽에서 삽입과 삭제가 가능하다

```c++
#include <iostream>
#include <deque>
using namespace std;

int main()
{
  deque<int> dq;
  
  dq.push_back(4); //4추가
}
```

* push_front("숫자") : 제일 앞에 '숫자'를 원소로 추가함

* push_back("숫자") : 제일 뒤에 '숫자'를 원소로 추가함

* pop_front( ) : 첫번째 원소를 제거함

* pop_back( ) : 마지막 원소를 제거함

* clear( ): 모든 원소 삭제

* front( ) : 첫번째 원소 참조

* back( ) : 마지막 원소 참조

  

## deque - 파이썬

* append( )

  마지막에 원소를 추가한다

* appendleft( )

  첫번째에 원소를 추가한다

* pop( )

  마지막 원소를 제거하고 그 값을 반환한다.

* popleft( )

  첫번째 원소를 제거하고 그 값을 반환한다.

# 이진 트리

## 이진트리 - c++ - map으로 구현

선언

```c++
map<char, pair<char,char>> tree; //부모노드, 자식노드 2개로 구성
```

구현(원소 추가)

```c++
tree['A'] = make_pair('B','C'); //부모 A 노드 안에 자식노드 B,C추가
tree['B'] = make_pair('.','.'); //부모 B 노드 안에 자식이 없으므로 .추가
```

이렇게 노드 개수만큼 Map에 저장하는 것을 반복해주면 이진트리가 완성된다

출력

```c++
for( const auto &w : tree)
        cout << w.first << w.second.first << w.second.second << endl; //부모노드, 자식노드1, 자식노드2 출력
```

노드를 수정하고 싶으면

```c++
tree['B'].first = 'D'; //부모 B노드의 첫번째 자식에 D를 추가 하고 싶으면 이렇게
```

노드를 map으로 추가했다가 삭제하고 싶으면 

```c++
tree.erase("B"); //부모 노드(key)가 B인 맵을 지운다.
```

A노드의 왼쪽 자식을 알고 싶으면

```c++
tree['A'].first;
```

오른쪽 자식을 알고 싶으면

```c++
tree['A'].second;
```

이렇게 해주면 된다



전위순회, 중위순회, 후위순회 하는 방법

```c++
#include <iostream>
#include <map>
using namespace std;

void preorder(map<char,pair<char, char>>& m,char node);
void inorder(map<char,pair<char, char>>& m,char node);
void postorder(map<char,pair<char, char>>& m,char node);
int main()
{
    int N;
    char pa, ch1, ch2, pa2;
    map<char, pair<char, char>> tree;
    cin >> N;
    for(int i = 0;i < N;i++)
    {
        cin >> pa >> ch1 >> ch2;
        tree[pa] = make_pair(ch1,ch2);
        if(i == 0)
            pa2 = pa;
    }
    
    preorder(tree, pa2);
    cout << endl;
    inorder(tree, pa2);
    cout << endl;
    postorder(tree, pa2);
    cout << endl;
}

void preorder(map<char,pair<char, char>>& m,char node) {
    cout << node; 
    if (m[node].first != '.')
    {
        preorder(m,m[node].first);
    }
    if (m[node].second != '.')
    { 
        preorder(m,m[node].second);
    }
}
void inorder(map<char,pair<char, char>>& m,char node) {
    if (m[node].first != '.')
    { 
        inorder(m,m[node].first);
    }
    cout << node; 
    if (m[node].second != '.')
    { 
        inorder(m,m[node].second);
    }
}
void postorder(map<char,pair<char, char>>& m,char node) {
    if (m[node].first != '.')
    { 
        postorder(m,m[node].first);
    }
    if (m[node].second != '.')
    { 
        postorder(m,m[node].second);
    }
    cout << node;
}
```

이진트리 삽입연산

https://blockdmask.tistory.com/79

## 이진트리

```c++
#include <iostream>

struct Node
{
    int data;        //데이터
    Node* left;        //왼쪽 자식노드
    Node* right;        //오른쪽 자식노드
};

class BinaryTreeLinkedList
{
public:
    BinaryTreeLinkedList();                //생성자
    ~BinaryTreeLinkedList();            //소멸자
    
    Node* CreateNode();                //노드 생성
    bool GetData(Node* node, int& data);        //값 반환
    bool SetData(Node* node, int data);        //값 지정

    bool GetLeftNode(Node* parent, Node** node);    //노드의 왼쪽 자식노드 반환
    bool GetRightNode(Node* parent, Node** node);    //노드의 오른쪽 자식노드 반환

    bool SetLeftNode(Node* parent, Node* child);    //노드의 왼쪽 자식노드 지정
    bool SetRightNode(Node* parent, Node* child);    //노드의 오른쪽 자식노드 지정

    void PreorderPrint(Node* node);            //전위 순회
    void InorderPrint(Node* node);            //중위 순회
    void PostorderPrint(Node* node);        //후위 순회

    void RemoveNode(Node* node);            //노드 제거
};

BinaryTreeLinkedList::BinaryTreeLinkedList() //생성자
{
    printf("생성자\n");
}

BinaryTreeLinkedList::~BinaryTreeLinkedList() //소멸자
{
    printf("소멸자\n");
}

Node* BinaryTreeLinkedList::CreateNode() //노드 생성
{
    Node* newNode = new Node;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

bool BinaryTreeLinkedList::GetData(Node* node, int& data) //값 반환
{
    if (node == NULL)
        return false;

    data = node->data;
    printf("GetData : %d\n", data);
    return true;
}

bool BinaryTreeLinkedList::SetData(Node* node, int data) //값 지정
{
    if (node == NULL)
        return false;

    node->data = data;
    printf("SetData : %d\n", node->data);
    return true;
}

bool BinaryTreeLinkedList::GetLeftNode(Node* parent, Node** node) //노드의 왼쪽 자식 노드 반환
{
    if (parent == NULL || parent->left == NULL)
    {
        *node = NULL;
        return false;
    }

    *node = parent->left;
    printf("GetLeftNode : %d\n", (*node)->data);
    return true;
}

bool BinaryTreeLinkedList::GetRightNode(Node* parent, Node** node) //노드의 오른쪽 자식 노드 반환
{
    if (parent == NULL || parent->right == NULL)
    {
        *node = NULL;
        return false;
    }

    *node = parent->right;
    printf("GetRightNode : %d\n", (*node)->data);
    return true;
}

bool BinaryTreeLinkedList::SetLeftNode(Node* parent, Node* child) //노드의 왼쪽 자식 노드 지정
{
    if (parent == NULL || child == NULL)
        return false;

    if (parent->left != NULL)                //이미 왼쪽 자식노드가 있으면
        RemoveNode(parent->left);            //왼쪽 자식노드를 지워준다.

    parent->left = child;
    printf("Set %d Node's LeftData : %d\n", parent->data, child->data);
    return true;
}

bool BinaryTreeLinkedList::SetRightNode(Node* parent, Node* child) //노드의 오른쪽 자식 노드 지정
{
    if (parent == NULL || child == NULL)
        return false;

    if (parent->right != NULL)                //이미 오른쪽 자식노드가 있으면
        RemoveNode(parent->right);            //오른쪽 자식 노드를 지워준다.

    parent->right = child;
    printf("Set %d Node's RightData : %d\n", parent->data, child->data);
    return true;
}

void BinaryTreeLinkedList::PreorderPrint(Node* node) //전위 순회
{
    if (node == NULL)
        return;

    printf("Pre : %d\n", node->data);
    PreorderPrint(node->left);
    PreorderPrint(node->right);
}

void BinaryTreeLinkedList::InorderPrint(Node* node) //중위 순회
{
    if (node == NULL)
        return;

    InorderPrint(node->left);
    printf("In : %d\n", node->data);
    InorderPrint(node->right);
}

void BinaryTreeLinkedList::PostorderPrint(Node* node) //후위 순회
{
    if (node == NULL)
        return;

    PostorderPrint(node->left);
    PostorderPrint(node->right);
    printf("Post : %d\n", node->data);
}

void BinaryTreeLinkedList::RemoveNode(Node* node) //노드 제거
{
    if (node == NULL)
        return;

    RemoveNode(node->left);                    //지우는 방식은 후위 순회방식으로
    RemoveNode(node->right);
    printf("Delete : %d\n", node->data);
    delete node;
}

//메인
int main()
{
    BinaryTreeLinkedList* ListBinaryTree = new BinaryTreeLinkedList();

    Node* tempANode = ListBinaryTree->CreateNode();
    Node* tempBNode = ListBinaryTree->CreateNode();
    Node* tempCNode = ListBinaryTree->CreateNode();
    Node* tempDNode = ListBinaryTree->CreateNode();
    Node* tempENode = ListBinaryTree->CreateNode();
    Node* tempFNode; //임시로 데이터를 가져오기 위한 구조체 포인터

    ListBinaryTree->SetData(tempANode, 1);
    ListBinaryTree->SetData(tempBNode, 2);
    ListBinaryTree->SetData(tempCNode, 3);
    ListBinaryTree->SetData(tempDNode, 4);
    ListBinaryTree->SetData(tempENode, 5);

    printf("\n");
    ListBinaryTree->SetLeftNode(tempANode, tempBNode);
    ListBinaryTree->SetRightNode(tempANode, tempCNode);
    ListBinaryTree->SetData(tempANode->left, 20);        //왼쪽 자식 노드 값 변경

    printf("\n"); //.
    ListBinaryTree->GetRightNode(tempANode, &tempFNode);    //오른쪽 자식 노드 가져와서
    ListBinaryTree->SetData(tempFNode, 30);            //그 노드의 값 변경

    printf("\n");
    ListBinaryTree->GetLeftNode(tempANode, &tempFNode);
    ListBinaryTree->SetLeftNode(tempFNode, tempDNode);
    ListBinaryTree->SetRightNode(tempFNode, tempENode);

    printf("\n");

    int data; //임시로 데이터를 가져오기 위한 변수
    ListBinaryTree->GetData(tempANode, data);
    ListBinaryTree->GetData(tempBNode, data);
    ListBinaryTree->GetData(tempCNode, data);
    ListBinaryTree->GetData(tempDNode, data);
    ListBinaryTree->GetData(tempENode, data);
    ListBinaryTree->GetData(tempFNode, data);

    printf("\n");
    ListBinaryTree->PreorderPrint(tempANode);
    printf("\n");
    ListBinaryTree->InorderPrint(tempANode);
    printf("\n");
    ListBinaryTree->PostorderPrint(tempANode);

    printf("\n");
    ListBinaryTree->RemoveNode(tempANode);
    delete ListBinaryTree;
}
```



## 이진 탐색 트리

```c++
#include<iostream>
using namespace std;

struct Node {
	int data;
	//부모 노드
	Node* parent;
	//왼쪽 자식 노드
	Node* leftChild;
	//오른쪽 자식 노드
	Node* rightChild;
};

class binarySearchTree {
private:
	Node* root;
public:
	binarySearchTree() {
		root = nullptr;
	}
	void insert(int elem);
	Node* find(int elem);
	void swap(Node* a, Node* b);
	void erase(int elem);
	void erase(Node* elem);
	void print(Node* node);
	Node* getRoot();

};
/// <summary>
/// BST에 새로운 원소 삽입
/// </summary>
/// <param name="elem(삽입할 원소)"></param>
void binarySearchTree::insert(int elem) {
	//새로 삽입할 노드
	Node* addNode = new Node;
	//맨처음 삽입이라면 루트에 넣어주기
	if (root == nullptr) {
		addNode->data = elem;
		addNode->parent = nullptr;
		addNode->leftChild = nullptr;
		addNode->rightChild = nullptr;
		root = addNode;
		return;
	}

	//현재 노드를 가리키는 노드(초기값 root노드)
	Node* curNode = root;
	while (1) {
		//인풋값이 현재 curNode가 가리키는 노드의 데이터값보다 작다면
		while (curNode->data > elem) {
			//curNode의 왼쪽자식이없다면 
			if (curNode->leftChild == nullptr) {
				//curNode의 왼쪽자식노드값 설정해주고 부모 자식값 다시설정
				addNode->data = elem;
				addNode->parent = curNode;
				addNode->leftChild = nullptr;
				addNode->rightChild = nullptr;
				curNode->leftChild = addNode;
				return;
			}
			//왼쪽 자식이 존재하면
			else {
				//curNode가 자신의 왼쪽 자식노드를 참조하게함
				curNode = curNode->leftChild;
			}
		}
		//인풋값이 curNode가 가리키는 노드의 데이터값보다 같거나 크면 
		while (curNode->data <= elem) {
			//오른쪽자식값이 없다면 해당 자식노드에 추가
			if (curNode->rightChild == nullptr) {
				addNode->data = elem;
				addNode->parent = curNode;
				addNode->leftChild = nullptr;
				addNode->rightChild = nullptr;
				curNode->rightChild = addNode;
				return;
			}
			//오른쪽 자식 존재하면 오른쪽 자식 노드 참조하게함
			else {
				curNode = curNode->rightChild;
			}
		}
	}

}

/// <summary>
/// 입력값을 찾는 함수
/// </summary>
/// <param name="elem(찾을 원소)"></param>
/// <returns>"원소 찾았다면 해당 원소 가리키는 포인터, 못 찾았다면 nullptr"</returns>
Node* binarySearchTree::find(int elem) {
	Node* curNode = root;
	//트리가 비어있다면 nullptr반환
	if (curNode == nullptr) {
		return nullptr;
	}
	while (1) {
		//현재 찾는값이 curNode가 가리키는 데이터값보다 작으면
		while (curNode->data > elem) {
			//왼쪽 자식노드로 
			curNode = curNode->leftChild;
		}
		//찾는 값이 curNode가 가리키는 데이터값보다 같거나 크면
		while (curNode->data <= elem) {
			//elem값을 찾았다면 해당 노드 반환
			if (curNode->data == elem) {
				return curNode;
			}
			//못찾았다면 오른쪽 노드로
			curNode = curNode->rightChild;
		}
		//curNode가 nullptr이라면 존재하지 않으므로
		if (curNode == nullptr) return nullptr;
	}
}

/// <summary>
/// 매개변수로 들어온 노드 두개 바꿔주는 함수
/// </summary>
/// <param name="a(노드 1)"></param>
/// <param name="b(노드 2)"></param>
void binarySearchTree::swap(Node* a, Node* b) {
	//swap용 임시 노드
	Node* tmp = new Node;
	//a의 부모 노드의 왼쪽자식이 a라면
	if (a->parent->leftChild == a) {
		//b로 연결
		a->parent->leftChild = b;
	}
	//a의 부모 노드의 오른쪽 자식이 b라면
	else {
		a->parent->rightChild = b;
	}

	//b의 부모 노드의 왼쪽 자식이 b라면
	if (b->parent->leftChild == b) {
		b->parent->leftChild = a;
	}
	//b의 부모 노드의 오른쪽 자식이 a라면
	else {
		b->parent->rightChild = a;
	}

	tmp->data = b->data;
	b->data = a->data;
	a->data = tmp->data;

	tmp->parent = b->parent;
	b->parent = a->parent;
	a->parent = tmp->parent;

	tmp->leftChild = b->leftChild;
	b->leftChild = a->leftChild;
	a->leftChild = tmp->leftChild;

	tmp->rightChild = b->rightChild;
	b->rightChild = a->rightChild;
	a->rightChild = tmp->rightChild;

	delete(tmp);
}

/// <summary>
/// BST에서 매개변수값 제거하는 함수
/// </summary>
/// <param name="elem(지울 원소)"></param>
void binarySearchTree::erase(int elem) {
	Node* delNode = find(elem);
	//BST에 해당 원소 없다면 바로 종료
	if (delNode == nullptr) {
		return;
	}
	//해당 원소가 리프 노드라면 
	if (delNode->leftChild == nullptr && delNode->rightChild == nullptr) {
		//해당 원소의 부모노드에서 해당 원소 제거
		if (delNode->parent->leftChild == delNode) delNode->parent->leftChild = nullptr;
		else delNode->parent->rightChild = nullptr;
	}
	//해당원소가 오른쪽 자식만 있을 때
	else if (delNode->leftChild == nullptr) {
		//만약 del노드가 del의 부모노드의 왼쪽자식이라면
		if (delNode->parent->leftChild == delNode) {
			delNode->parent->leftChild = delNode->rightChild;
		}
		//del노드가 부모노드의 오른쪽자식이라면
		else {
			delNode->parent->rightChild = delNode->rightChild;
		}
		//해당원소의 오른쪽자식의 부모노드를 해당원소의 부모노드로 설정
		delNode->rightChild->parent = delNode->parent;
	}
	//해당원소가 왼쪽 자식만 있을 때
	else if (delNode->rightChild == nullptr) {
		//del노드가 부모 노드의 왼쪽자식이라면
		if (delNode->parent->leftChild == delNode) {
			//부모노드의 왼쪽 자식을 해당원소의 왼쪽 자식으로 설정
			delNode->parent->leftChild = delNode->leftChild;
		}
		else {
			delNode->parent->rightChild = delNode->leftChild;
		}
		//해당원소의 왼쪽자식의 부모노드를 해당원소의 부모노드로 설정
		delNode->leftChild->parent = delNode->parent;
	}
	//해당 원소가 두 자식 다 있을 때 오른쪽 서브트리에서 제일 작은값과 교체
	else {
		//오른쪽 서브트리의 루르노드부터 시작해서
		Node* curNode = delNode->rightChild;
		//오른쪽 서브트리의 제일 작은 노드까지 
		while (curNode->leftChild != nullptr) {
			curNode = curNode->leftChild;
		}
		//두 노드를 바꿔주고
		swap(curNode, delNode);
		//해당 원소의 부모노드에서 해당 원소 제거
		if (delNode->parent->leftChild == delNode) delNode->parent->leftChild = nullptr;
		else delNode->parent->rightChild = nullptr;
	}
	delete(delNode);
}
/// <summary>
/// 매개변수로 들어온 노드 포인터가 가리키는 노드 제거
/// </summary>
/// <param name="elem"></param>
void binarySearchTree::erase(Node* node) {
	//해당 원소가 리프 노드라면 
	if (node->leftChild == nullptr && node->rightChild == nullptr) {
		//해당 원소의 부모노드에서 해당 원소 제거
		if (node->parent->leftChild == node) node->parent->leftChild = nullptr;
		else node->parent->rightChild = nullptr;
	}
	//해당원소가 오른쪽 자식만 있을 때
	else if (node->leftChild == nullptr) {
		//만약 del노드가 del의 부모노드의 왼쪽자식이라면
		if (node->parent->leftChild == node) {
			node->parent->leftChild = node->rightChild;
		}
		//del노드가 부모노드의 오른쪽자식이라면
		else {
			node->parent->rightChild = node->rightChild;
		}
		//해당원소의 오른쪽자식의 부모노드를 해당원소의 부모노드로 설정
		node->rightChild->parent = node->parent;
	}
	//해당원소가 왼쪽 자식만 있을 때
	else if (node->rightChild == nullptr) {
		//del노드가 부모 노드의 왼쪽자식이라면
		if (node->parent->leftChild == node) {
			//부모노드의 왼쪽 자식을 해당원소의 왼쪽 자식으로 설정
			node->parent->leftChild = node->leftChild;
		}
		else {
			node->parent->rightChild = node->leftChild;
		}
		//해당원소의 왼쪽자식의 부모노드를 해당원소의 부모노드로 설정
		node->leftChild->parent = node->parent;
	}
	//해당 원소가 두 자식 다 있을 때 오른쪽 서브트리에서 제일 작은값과 교체
	else {
		//오른쪽 서브트리의 루르노드부터 시작해서
		Node* curNode = node->rightChild;
		//오른쪽 서브트리의 제일 작은 노드까지 
		while (curNode->leftChild != nullptr) {
			curNode = curNode->leftChild;
		}
		//두 노드를 바꿔주고
		swap(curNode, node);
		//해당 원소의 부모노드에서 해당 원소 제거
		if (node->parent->leftChild == node) node->parent->leftChild = nullptr;
		else node->parent->rightChild = nullptr;
	}
	delete(node);
}

/// <summary>
/// inorder 방식으로 순회하며 크기대로 출력
/// </summary>
/// <param name="root값 넣어주면 됨"></param>
void binarySearchTree::print(Node* node) {
	if (node == nullptr) return;

	print(node->leftChild);
	cout << node->data;
	print(node->rightChild);
}

/// <summary>
/// root노드 포인터 반환해주는 함수
/// </summary>
/// <returns>루트 노드</returns>
Node* binarySearchTree::getRoot() {
	return root;
}


int main() {
	binarySearchTree* bst=new binarySearchTree();
	bst->insert(5);
	bst->insert(2);
	bst->insert(3);
	bst->insert(4);
	bst->insert(1);
	bst->insert(6);
	bst->insert(7);
	
	bst->print(bst->getRoot());
	cout << '\n';

	bst->erase(3);
	bst->print(bst->getRoot());

	cout << '\n';
	bst->insert(3);
	bst->print(bst->getRoot());
	cout << '\n';
	bst->insert(3);
	bst->print(bst->getRoot());
	cout << '\n';

	bst->erase(bst->find(3));
	bst->print(bst->getRoot());
	cout << '\n';

	cout<<bst->find(3)->data;


}
```

## 힙

최대힙

```c++
#include <stdio.h>
#define MAX_SIZE 100    // Heap 의 최대 원소 개수 
 
typedef struct{    // Heap 의  노드 
    int key;    // Heap 의 key
    /* 여기에 데이터 추가 가능 ex) int data */ 
}element;    
 
typedef struct{    // Heap 자료구조 
    element heap[MAX_SIZE];     
    int size;
}Heap;
 
 
void max_heap_insert(Heap* h, element item){
    int i;
    i = ++(h->size);    // 마지막 위치(마지막 원소의 index+1) 
    
    /* 루트노드가 아니고, 삽입할 값이 적절한 위치를 찾을 때까지*/
    while( (i != 1) && (item.key > h->heap[i/2].key) ){
        h->heap[i] = h->heap[i/2];    // 자식 노드와 부모노드 교환 
        i /= 2;    // 한 레벨 위로 올라감 
    }
    
    h->heap[i] = item;    // 새로운 노드 삽입     
}
 
element max_heap_delete(Heap* h){
    int parent, child;
    element item, temp;
    
    item = h->heap[1];    // 반환할 노드 저장
    temp = h->heap[(h->size)--];    // 마지막 노드 temp 에 저장, 사이즈 1감소
    parent = 1;     
    child = 2; 
    
    while(child <= h->size){
        /* 왼쪽 자식 노드와 오른쪽 자식 노드 중 더 큰 자식 노드*/
        if( (child < h->size) && ((h->heap[child].key) < h->heap[child+1].key )){
            child++;    // 오른쪽 자식 노드 선택
        }
        
        /* 마지막 노드가 자식 노드보다 크면 종료 */
        if(temp.key >= h->heap[child].key){
            break;
        } 
        
        /* 부모노드와 자식노드 교환 */
        h->heap[parent] = h->heap[child];
        
        /* 한 레벨 아래로 이동 */ 
        parent = child;
        child *= 2;
    }
    
    /* 마지막 노드를 재설정한 위치에 삽입 */ 
    h->heap[parent] = temp;
    
    /* 최댓값 노드 반환 */ 
    return item;    
    
} 
 
 
int main(){
    Heap max_heap;
    element item;
    item.key = 9;
    max_heap_insert(&max_heap, item);
    item.key = 7;
    max_heap_insert(&max_heap, item);
    item.key = 6;
    max_heap_insert(&max_heap, item);
    item.key = 4;
    max_heap_insert(&max_heap, item);
    item.key = 5;
    max_heap_insert(&max_heap, item);
    item.key = 1;
    max_heap_insert(&max_heap, item);
    item.key = 3;
    max_heap_insert(&max_heap, item);
    item.key = 8;
    max_heap_insert(&max_heap, item);
    
    while(max_heap.size > 0){
        item = max_heap_delete(&max_heap);
        printf("%d ", item.key);
    }
        
    return 0;
} 

```

## 그래프

간선이 적으면 인접리스트

간선이 많으면 인접행렬

```c++
#include <iostream>
#include <vector>
using namespace std;

// 인접 리스트 : 실제 연결된 애들만 넣어줌.
void CreateGraph_AdjacencyList()
{
    struct Vertex
    {
        int data;
    };

    vector<Vertex> v(6); // 정점 6개 생성.

    //      0             1            2
    // [vector<int>][vector<int>][vector<int>]...
    vector<vector<int>> adjacent; // 2차원 배열.
    adjacent.resize(6);

    adjacent[0] = { 1, 3 }; // 0번 정점은 1, 3번 정점과 연결되어 있음.
    adjacent[1] = { 0, 2, 3 }; // 1번 정점은 0, 2, 3번 정점과 연결되어 있음.
    adjacent[3] = { 4 }; // 3번 정점은 4번 정점과 연결되어 있음.
    adjacent[4] = { 5 }; // 4번 정점은 5번 정점과 연결되어 있음.

    // Q) 0번->3번 연결되어 있나요?
    bool connected = false;
	
    // 정점이 가지고 있는 값들을 하나씩 조사.
    int size = adjacent[0].size();
    for (int i = 0; i < size; i++)
    {
        int vertex = adjacent[0][i];
        if (vertex == 3)
            connected = true;
    }
}

// 인접 행렬 : 메모리 소모 심하지만, 빠른 접근 가능.
void CreateGraph_AdjacencyMatrix()
{
    struct Vertex
    {
        int data;
    };

    vector<Vertex> v(6);

    // 연결된 목록을 행렬로 관리
    // [X][O][X][O][X][X] 0 -> 1, 3
    // [O][X][O][O][X][X] 1 -> 0, 2, 3
    // [X][X][X][X][X][X] 2 -> x
    // [X][X][X][X][O][X] 3 -> 4
    // [X][X][X][X][X][X] 4 -> x
    // [X][X][X][X][O][X] 5 -> 4

    vector<bool> v(6, false);

    vector<vector<bool>> adjacent(6, vector<bool>(6, false));
    adjacent[0][1] = true;
    adjacent[0][3] = true;

    adjacent[1][0] = true;
    adjacent[1][2] = true;
    adjacent[1][3] = true;

    adjacent[3][4] = true;
    adjacent[5][4] = true;

    // Q) 0번 -> 3번 연결되어 있나요?
    // 정점을 인덱스로 사용하여 바로 접근 가능.
    bool connected = adjacent[0][3];

    // 가중치 그래프를 인접 행렬로 만들기. (정점간 연결되어 있지 않은 경우 = -1)
    // 값을 가중치로 사용하면 됨.
    vector<vector<int>> adjacent2 =
    {
        { -1, 15, -1, 35, -1, -1},
        { 15, -1, 5, 10, -1, -1},
        { -1, 5, -1, -1, -1, -1},
        { 35, 10, -1, -1, 5, -1},
        { -1, -1, -1, 5, -1, 5},
        { -1, -1, -1, -1, 5, -1},
    };
}
```

