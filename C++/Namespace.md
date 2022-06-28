# [C++/MacOS] Namespace란? using namespace std가 뭘까?

c++ 코드를 짜보면 아래와 같은 코드를 많이 봤을 것이다. 
`using namespace std;` 
저 줄은 무엇이고 왜 사용하는 것일까?
- - -

## C++ Namespace란?
간단하게 __namespace__ 란 __이름 공간__ 이라고 생각하면 된다. 

보통 프로그램을 짤 때 여러 파일들이 생기기 마련이다.
그 파일들을 한꺼번에 컴파일하려고 할 때 같은 이름의 함수나 구조체가 존재한다면 컴퓨터는 이에 대한 오류를 낸다. 

같은 이름의 변수나 함수, 구조체가 있을 때 오류가 발생하는 것은 당연한 일이다. 이름 충돌이 일어났기 때문이다. 

Namespace는 이러한 이름충돌을 방지하기 위해서 만들어진 것이다. 

__Namespace는 변수, 함수, 구조체 등의 소속을 정해주는 것이다.__
__소속을 지정해줌으로써 같은 이름이어도 헷갈리지 않도록 도와주는 것이다.__

아래 코드를 봐보자.
```
#include <iostream>
using namespace std; //이거는 나중에 설명하도록 하겠다

int cal(int a, int b){     //더하는 함수
    int result = a + b;
    return result;
}

int cal(int a, int b){    //빼는 함수
    int result = a - b;
    return result;
}
int main(){
    int a = 5;
    int b = 3;
    
    int add = cal(a, b);
    int sub = cal(a, b);
    cout << sum << endl;
    cout << sub << endl;
}
```
cal이라는 함수 두개가 이름 충돌을 일으키고 있기 때문에 아래와 같은 오류가 뜬다. 
```
namespace.cpp:8:5: error: redefinition of 'cal'
int cal(int a, int b){
    ^
namespace.cpp:3:5: note: previous definition is here
int cal(int a, int b){
    ^
1 error generated.
```

- - -
## Namespace 사용법
__Namespace로 감싸기!__
Namespace는 함수뿐만 아니라 구조체, 변수 등 모두 사용할 수 있다. 

```
namespace 네임스페이스 이름 {
    함수, 구조체, 변수 등 선언
}
```

오류가 발생했던 두 개의 cal 함수를 namespace로 감싸면 이름 충돌을 해결할 수 있다.

```
namespace Add {
    int cal(int a, int b){     //더하는 함수
        int result = a + b;
        return result;
    }
}

namespace Sub {
    int cal(int a, int b){    //빼는 함수
        int result = a - b;
        return result;
    }
}
```

- - -
## Namespace 요소 접근법
1. 한정된 이름(qualified name)을 사용한 접근 
`Namespace_name::요소` 

감싸주었던 namespace 이름과 콜론 두개를 적어주고 호출하고 싶은 요소 이름을 이어 적어주면 된다. 
아래 코드처럼 말이다. 

- __::__ <- scope resolution operator
```
int main(){
    int a = 5;
    int b = 3;
    
    int add = Add::cal(a, b);
    int sub = Sub::cal(a, b);
    cout << sum << endl;
    cout << sub << endl;
}
```

