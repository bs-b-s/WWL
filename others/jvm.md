### **컴파일이란?**

> **우리가 이해하는 언어를 컴퓨터가 이해할 수 있는 언어로 변환하는 작업 컴파일이라고 한다.**

우리는 프로그래밍 언어(C, java, python...)를 사용하고 컴퓨터는 0과 1로 이루어진 바이너리 코드(binary code)를 사용한다.

컴퓨터가 이해하는 언어를 라고 한다. 그래서 우리는 프로그래밍 언어를 바이너리 코드로 변환 시켜야할 필요가 있다. 

#### **이때 문제가 생긴다.**

> #### **🚨** **CPU 제조사 마다 전부 다른 바이트 코드를 사용한다는 것이다!**

지금부터 각 언어들의 컴파일 과정을 보면서 이 문제를 어떻게 대응했는지 살펴보자.

### **Compilation** 

대표적인 언어로는 C가 있다. compilation은 플렛폼에 의존적이다.

소스 코드를 각기 다른 OS(윈도우, 맥, 리눅스...)에 맞게 전부 바이너리 코드로 변환하여 한번에 실행하는 방식이다.

그래서 별도의 실행파일이 존재한다.


### **Interpretation** 

대표적인 언어로는 python, javascript, Ruby, PHP가 있다. compilation처럼 소스 코드를 전부 바이너리 코드로 변환하고 실행한 것과는 다르게 실시간으로 한 줄씩 읽어들여 바이너리 코드로 변환함과 동시에 실행된다. 번역과 실행이 동시에 이루어지므로 별도의 실행파일이 존재하지 않는다.


### **JAVA의 JVM**

**👉🏾JVM** 

> java는 인터프리터와 컴파일러의 특징을 모두 가지고 있는 JVM을 사용한다.  
> Java Virtual Machine의 약자로 JAVA와 OS 사이에서 자바 바이트 코드를 기계어로 번역한다.

**👉🏾자바 컴파일 과정**


| **순서** | **작업** |
| --- | --- |
| 1 | JAVA 프로그램 실행 |
| 2 | OS가 JVM에 프로그램이 필요한 메모리를 할당한다. |
| 3 | JAVA 컴파일러(Javac)가 자바 소스코드(.java)를 자바 바이트 코드(.class)로 변환한다.   **▷ Compilation** |
| 4 | Class Loader가 번역된 .class 파일을 JVM에 로드한다. |
|    5 | JVM은 각 OS에 맞는 바이트 코드(기계어)로 번역한다.   **▷ Interpretation** |

보시다시피 자바 바이트 코드만 주면 JVM이 알아서 OS에 맞는 바이트 코드로 변환시켜주기 때문에 플렛폼에 종속적이지 않다.
