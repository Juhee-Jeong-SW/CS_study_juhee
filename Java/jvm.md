# JVM

## **JVM(Java Virtual Machine)**

- 스택 기반의 가상 머신.
- JVM의 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어들여 자바 API와 함께 실행하는 것이다.
- Java와 OS 사이에서 중개자 역할을 수행하여 Java가 OS에 구애받지 않고 재사용 가능하게 해준다.
- 메모리 관리, Garbage Collection(GC를 통해 자원을 관리)을 수행한다.
- 자바 바이트 코드를 실행할 수 있는 주체이다.

**[JVM을 알야아 하는 이유는 뭘까?]**

- > 한정된 메모리를 효율적으로 사용하여 최고의 성능을 내기 위해서라 할 수 있다. 동일한 기능의 프로그램이더라도 메모리 관리에 따라서 성능이 좌우되기 때문에 JVM이 하는 역할을 이해하고 메모리를 효율적으로 사용하여 최고의 성능을 낼 수 있을 것이다.

**[자바 프로그램 실행 과정]**

1. 프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다. JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
2. 자바 컴파일러(javac)가 자바 소스 코드를 읽어들여 자바 바이트 코드(.class)로 변환시킨다.
3. Class Loader를 통해 class 파일들을 JVM으로 로딩한다.
4. 로딩된 class 파일들은 Execution Engine을 통해 해석된다.
5. 해석된 바이트 코드는 Runtime Data Area에 배치되어 실질적인 수행이 이루어지게 된다. 이러한 실행 과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC 같은 관리 작업을 수행한다.

![https://user-images.githubusercontent.com/33534771/83471568-f7200100-a4bf-11ea-810f-3ea08018317f.png](https://user-images.githubusercontent.com/33534771/83471568-f7200100-a4bf-11ea-810f-3ea08018317f.png)

### **각각의 역할**

**[Class Loader(클래스 로더)]**

- Runtim시에 JVM내로 클래스(.class 파일)를 로드하고 링크를 통해 배치하는 작업을 수행한다. (Runtime : 클래스를 처음으로 참조할 때.)
- 사용하지 않는 클래스들은 메모리에서 삭제한다.
- 동적 로드를 담당한다.

**[Execution Engine(실행 엔진)]**

- 클래스를 실행시키는 역할이다.
- 클래스 로더가 JVM 내의 Runtime Data Area에 바이트 코드를 배치시키고 이것은 실행 엔진에 의해서 실행된다.
- 자바 바이트 코드는 비교적 인간이 보기 편한 형태로 기술된 것이다. 그래서 실행 엔진은 이와 같은 바이트 코드를 실제로 JVM 내부에서 기계가 실행할 수 있는 형태로 변경한다.
- 실행 엔진은 자바 바이트 코드를 명령어 단위로 읽어서 실행한다.
- 2가지 방식이 존재한다.
  - 최초의 JVM은 인터프리터 방식이었기 때문에 속도가 느린 단점이 존재했지만, JIT 컴파일러 방식을 통해 이 점을 보완했다.

1. Interpreter(인터프리터)

- 자바 바이트 코드를 명령어 단위로 읽어서 실행한다.
- 한 줄씩 실행하기 때문에 느리다.

1. JIT(Just-In-Time) Compiler

- 인터프리터 방식의 단점을 보완하기 위해 등장했다.
- 인터프리터 방식으로 실행하다가 적절한 시점에 바이트 코드 전체를 컴파일하여 네이티브 코드로 변경하고 이후에는 더 이상 인터프리팅하지 않고 네이티브 코드로 직접 실행하는 방식이다.
- 네이티브 코드는 캐시에 보관하기 때문에 한 번 컴파일된 코드는 빠르게 수행된다.
- 한 번만 실행되는 코드라면 JIT 컴파일러가 컴파일하는 게 인터프리팅하는 것보다 오래 걸리므로 인터프리팅하는 것이 유리하다.
- 이처럼 해당 메소드가 얼마나 자주 수행되는지 체크하고 일정 정도를 넘을 때만 컴파일을 수행하는 게 좋다.

**[Garbage Collector]**

- GC를 수행하는 모듈이 존재한다.

**[Runtime Data Area]**

- JVM이 프로그램을 수행하기 위해 OS로부터 할당받은 메모리 공간이다.
- 이 공간은 용도에 따라 여러 영역으로 나누어 관리한다.

![https://user-images.githubusercontent.com/33534771/83472428-2fc0da00-a4c2-11ea-90a9-dac474fada4b.png](https://user-images.githubusercontent.com/33534771/83472428-2fc0da00-a4c2-11ea-90a9-dac474fada4b.png)

1. PC Register
   - Thread가 시작될 때, 각각의 Thread 별로 생성되는 공간으로 현재 수행 중인 JVM 명령어 주소를 가지게 된다.
2. JVM 스택 영역
   - 프로그램의 실행 과정에서 임시로 할당되었다가 메소드를 빠져나가면 바로 소멸되는 특성의 데이터를 저장하기 위한 영역이다.
   - 메소드의 매개변수, 지역 변수 등 메소드의 정보를 저장한다.
3. Natvie Method Stack
   - Java외의 언어로 작성된 네이티브 코드를 위한 영역이다.
   - 자바 프로그램이 컴파일 되어 생성되는 바이트 코드가 아닌 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역이다.
4. Method Area(Class Area, Static Area)
   - 클래스 정보를 처음 메모리 공간에 올릴 때, 초기화 되는 대상을 저장하기 위한 메모리 공간.
   - 모든 쓰레드가 **공유하는 메모리 영역**이다. 클래스, 인터페이스, 메소드, 필드, Static 변수 등의 바이트 코드를 보관한다.
   - Runtime Constant Pool이라는 것이 존재하며, 이는 별도의 관리 영역으로 상수 자료형을 저장하여 참조하고 중복을 막는 역할을 수행한다. (각 클래스와 인터페이스의 상수, 메소드와 필드에 대한 모든 레퍼런스를 담고 있는 테이블이다.)
   - Java 7부터 String Constant Pool은 Heap 영역으로 변경되어 GC의 관리 대상이 되었다.
5. Heap(힙 영역)
   - **객체**를 저장하는 가상 메모리 공간이다.
   - 런타임시 동적으로 할당하여 사용하는 영역.
   - `new` 연산자로 **생성된 객체와 배열을 저장**한다.
   - 클래스 영역에 올라온 클래스들로만 객체로 생성할 수 있으며, 세 부분으로 나눌 수 있다.
   - **GC의 관리 대상에 포함된다.**

![https://user-images.githubusercontent.com/33534771/83472881-3f8cee00-a4c3-11ea-942c-9b7aa0f4ea04.png](https://user-images.githubusercontent.com/33534771/83472881-3f8cee00-a4c3-11ea-942c-9b7aa0f4ea04.png)

- New/Young 영역
  - Eden : 객체들이 최초로 생성되는 공간.
  - Survivor 0/1 : Eden에서 참조되는 객체들이 저장되는 공간.
- Old 영역
  - New 영역에서 일정 시간 참조되고 살아남은 객체들이 저장되는 공간이다.
  - Eden 영역에서 인스턴스가 가득차게 되면 첫 번째 GC가 발생한다. (minor GC)
  - Eden 영역에 있는 값들을 Survivor 1 영역에 복사하고, 이 영역을 제외한 나머지 영역의 객체를 삭제한다.
  - Eden 영역에서 GC가 한 번 발생한 후 살아남은 객체는 Survivor 영역으로 이동한다. 이 과정을 반복하다가 살아남은 객체는 Old 영역으로 이동된다.
- Permanent Generation
  - 생성된 객체들의 주소값이 저장되는 공간이다.
  - 리플렉션을 사용하여 동적으로 클래스가 로딩되는 경우 사용된다.
  - Old 영역에서 살아남은 객체가 영원히 남아있는 곳이 아니다.
  - 이 영역에서 발생하는 GC는 Major GC의 횟수에 포함된다.