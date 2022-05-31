# OS의 일반적인 작동방식

## **운영체제의 구조**

<br>

### **운영체제(Operating System)**

**운영체제**는 컴퓨터 유저와 컴퓨터 하드웨어 사이의 인터페이스 역할을 한다. 자원이 필요한 프로그램에 자원을 할당하고, 자원을 할당받은 프로그램들의 실행을 제어한다.

운영체제가 하는 일은 다음과 같다.

* **프로세스 관리**
    - 프로세스와 쓰레드의 CPU 위에서의 작업들을 Scheduling(스케줄링)한다.
    - 유저와 시스템의 프로세스를 생성하거나 삭제한다.

<br>

* **메모리 관리**
    - 명령어들이 순서에 맞게 실행되도록 관리한다.
    - 모든 데이터들이 실행되기 전에 메모리에 올라갈 수 있도록 관리한다.
    - 메모리 공간을 할당하고 회수한다.
    - 언제 어떤 것이 메모리에 올라갈 지 결정한다.

<br>

* **저장소 관리**
 
* **보호 및 보안**

등등..

<br>

## **운영체제의 동작원리**

<br>

### **기본적인 원리**
OS는 사용자의 요청이 발생하면 적절하게 자원을 분배하여 그 요청을 처리해준다.
- 사용자의 요청: Event, Interrupt, H/W interrupt or S/W interrupt
- 자원 종류 : CPU, I/O, 메모리 등

<br>

### **OS의 작동방식**

<br>

#### **멀티프로그래밍(Multiprogramming)**
컴퓨터에는 CPU와 다양한 I/O device들이 존재하는데 CPU에는 단 하나의 프로그램 밖에 올라가지 않는다.
만약 해결 중이던 프로세스가 I/O 대기 상태면 그 시간동안 CPU가 놀게 된다.
따라서 메모리에 여러 프로세스들을 올려두고 I/O 대기 상태가 되면 다음 일로 넘어가 최대한 CPU의 대기상태를 제거하는 방법이 **멀티프로그래밍**이다.

멀티프로그래밍에도 단점이 있다. 이 방식을 쓰면 작업들마다 자원을 사용함에 있어 시간차가 생기게 된다.

예를 들어, 1번 작업이 CPU를 사용한 뒤 I/O를 사용하게 되면 CPU는 2번 작업에 할당되어 2번작업은 CPU를 사용하게 된다.
그런데 이때 1번 작업의 I/O 사용시간이 길어지게 되면 2번 작업이 CPU를 이용한 작업을 끝내더라도 I/O 작업으로 들어가지 못하고 계속 대기하게 된다.

이때 CPU 자원의 낭비가 일어나게 된다. 이런 문제를 해결하기 위해 **멀티테스킹(Multitasking)**이 나오게 된다.

<br>

#### **타임 셰어링(Time Sharing)**

시간 공유방식은 **멀티프로그래밍에서 확장된 방식**이다. 이것을 **멀티태스킹(Multitasking)**이라 부르기도 한다.
일괄 처리 시스템에서는 하나의 일이 끝날때까지 다른 작업이 CPU를 사용할 수 없는 문제가 있었다.

그래서 CPU가 scheduling을 통해 작업들을 빠르게 스위칭하면서 동시에 프로그램이 작동하는 것처럼 보이게 한다.
멀티 태스킹을 위해 메모리에 여러 일을 올려 놓을 경우 메모리가 모자를 수 있는데, 이런 경우 **스와핑**을 통해 프로세스를 가상 메모리에 저장한다.

CPU의 실행시간을 나누는 단위를 타임 슬라이스라고 한다.
일반적으로 10ms이며 모든 일은 타임 슬라이스동안 CPU를 점유하고 그 시간이 끝나면 CPU를 양보한다.

<br>

#### **인터럽트(Interrupt)**

현대의 OS는 **인터럽트 방식**을 사용한다.
인터럽트는 CPU가 일을 처리하고 있을 때 I/O device 등의 장치나 예외상황이 발생해 처리가 필요할 경우에 신호를 주어 처리할 수 있도록 하는 것을 말한다.
인터럽트는 **H/W Interrupt**, **S/W Interrupt**의 두 방식으로 나뉜다.

<br>

## **OS Loading**

1. 컴퓨터 전원이 켜지면 **CPU**는 **ROM(Read Only Memory)**에 저장된 내용을 읽는다.
    - ROM에는 POST와 부트로더가 저장되어 있다.
    - POST는 컴퓨터 전원이 켜지면 가장 먼저 실행되는 프로그램으로 컴퓨터에 이상이 있는지를 체크한다.
    - Boot Loader는 하드디스크에 저장되어 있는 OS프로그램을 가져와서 RAM에게 넘겨주는 일을 한다.

2. CPU는 초기화를 위해 Boot Loader에 모인 명령들을 읽고, Disk(HDD, SSD)에 있는 **프로그램들을 RAM(Random Access Memory)**에 올린다.

3. 프로그램들이 메모리에 올라오면 CPU가 해당 프로그램을 작동시킨다.