# Vector

C++의 동적 배열

---

`<vector.h>`를 include하면 `std::vector`를 사용할 수 있다

선언은 다음과 같이 이루어진다.

```cpp
std::vector vector<int> vec(10);
```

길이가 10인 벡터가 만들어졌다. 기본적인 벡터 접근, 값 수정은 모두 배열과 동일하다.

vector만이 가지는 특정 함수에 대해 소개한다.

`vec.assign(n);` : 길이가 n이고 값을 0으로 하여 벡터 크기를 조절한다.

`vec.size()` : 벡터의 크기를 가져온다.

`vec.empty()` : 벡터의 크기가 0이면 `true`, 그렇지 않으면 `false`를 리턴한다.

`vec.front()` : 벡터에 가장 앞에 있는 원소를 가져온다.

`vec.back()` : 벡터의 가장 뒤에 있는 원소를 가져온다.

---

당연히, `vector`를 사용하여 다차원 동적 배열을 만드는 것도 가능하다.

행의 개수가 10, 열의 개수가 20인 vector의 선언은 다음과 같다.

```cpp
std::vector vector<vector<int>> vec(10, vector<int>(20));
```

