# JVM의 구조

1. 자바 .java 라는 소스코드를 .class 라는 바이트코드로 변환시켜줌
    - 이 과정을 컴파일이라고함

---

2. class 파일들을 Class Loader 가 Runtime Data Area ,즉 , JVM메모리 공간으로 연결 시킴

   ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/085c71ec-9b5a-481e-92b0-d15efbd37d8c/image.png)

---

3. Runtime Data Area 는 총 5가지로 이루어져있다
    - 메서드 영역 , 힙영역 ( 모든 스레드가 공유 ) , 스택, PC Register, Native Method Stack
    
    - Method 영역
        
        1. 클래스 정보, 변수 정보, static으로 선언한 변수가 저장..
        2. 모든 스레드가 공유하는 영역
           ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/ee474bb6-10e6-4799-a5b6-af17934da224/image.png)
    
    - Heap 영역
        
        1. 동적으로 생성된 객체가 저장( new 연산을 통해 생성된 객체 )되는 영역, GC의 대상이 된다.
           ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/cfd66e0c-fa16-4ce5-8d2e-5678039c44bf/image.png)
        2. 효율적인 GC를 위하여 5가지 영역으로 나뉘어 있다.
           ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/6f92f814-4f31-4489-9279-669ce43efec4/image.png)
    
    - Stack 영역
        
        1. 지역변수나 메서드의 매개변수, 임시적으로 사용되는 변수, 메서드의 정보가 저장되는 영역이다
        
        * 헷갈리는 점!
        
        - Person 의 지역변수 p 는 Stack에 저장되고
        - new Person(... ) new연산자로 생성된 객체 자체는 HEAP영역에 저장된다.
          ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/d49ce5b7-2b81-4499-a135-e7f0608ee9c0/image.png)
          ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/29c9d0c9-d01f-42c5-9049-b28f9913e70d/image.png)
    
    - PC Register
        
        - 스레드가 시작될 떄 생성되며, **현재 수행중인** JVM의 명령어 주소를 저장하는 공간이다. 스레드가 어떤 부분을 어떤 명령어로 수행할 지를 저장하는 공간이다.
          ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/72feea7f-83ad-478b-a788-f477dbe6eae3/image.png)
    
    - Native Method Stack
        
        - JAVA가 아닌 다른 언어로 작성된 코드를 위한 공간
        - JNI(Java Native Interface) 를 통해 호출하는 C/C++ 등의 코드를 수행하기 위한 공간
          ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/2fd1d8b9-707c-427d-9ee8-1afee689c2b9/image.png)

---

4. Execution Engine을 통해 로드된 class파일의 bytecode가 실행된다.
   ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/b23c5005-d11e-48cb-bda2-2f4329842386/image.png)
    
    - 해당 class파일의 bytecode를 해석하는 방법에는 2가지가 존재한다.

   ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/285d4ccc-bbc8-4aba-bce4-01b1fd9d8c72/image.png)

   > JIT 컴파일러 방식
   > - Just In Time으로 무역학과 재학중일때 많이 배웠던 단어이다... 그 즉시 컴파일한다는 의미이다.

   > Interpreter 방식
   > - 한 줄 한 줄 단위로 컴파일한다는 의미
       > ![](https://velog.velcdn.com/images/qkrtkdwns3410/post/d0c9e5ce-3a1a-45a8-9bf5-afe0f649be89/image.png)

    - Native Method Interface(JNI)
        - JVM에 의해 실행되는 코드 중 **네이티브로 실행하는 것이 있다면** 
        - 해당 네이티브 코드를 호출하거나 호출 될 수 있도록 만든 일종의 프레임워크
    - Native Method Libraries
        - 네이티브 메서드 실행에 필요한 라이브러리