# ARM 프로세서

ARM\* 프로세서\*는 RISC\* 기반의 중앙처리장치(CPU)이다.

_\* ARM(Advanced RISC Machine): 발전된 RISC 기계를 말한다._   
_\* RISC(Reduced Instruction Set Computer): CPU 명령어의 개수를 줄여 명령어 해석시간을 줄임으로써 개별 명령어의 실행속도를 빠르게 한 컴퓨터다. CISC(Complex Instruction Set Computing)와 대조된다._  
_\* Processor: 하드웨어적인 측면에서 '컴퓨터 내에서 프로그램을 수행하는 하드웨어 유닛'이다._  

## ARM 프로세서 등장 배경

컴퓨터 기술이 현대화됨에 따라 고성능, 소형화를 추구하게 됐고, 80년대 아콘 컴퓨터는 마이크로컴퓨터를 설계했지만 칩 설계로 인한 한계를 느끼고 있었다.

비슷한 시기, 캘리포니아 대학교 버클리 캠퍼스의 한 프로젝트에서 한 프로그래머가 대부분의 프로그램이 명령어 세트의 작은 하위 집합만 사용한다는 것을 발견했다.

복잡하고 구현하기 어려우며 거의 사용되지 않는 명령어를 제거하여 미리 정의된 명령어의 수를 줄이게 되면, 남은 간단한 명령어는 더 빠르게 실행될 수 있고 칩의 전력과 공간을 적게 차지하게 된다는 것이다.

이를 RISC(Reduced Instruction Set Computer)아키텍처라 한다.

아콘은 새 컴퓨터에 쓸 만한 기성품 CPU를 찾을 수 없었고, 버클리 RISC 프로젝트에서 영감을 받아 직접 RISC 기반 CPU 아키텍처를 개발하기로 하는데 이것이 ARM의 시작인 `Acorn RISC Machine`이다.


## ARM 아키텍처

<img alt="ARM" src="https://user-images.githubusercontent.com/70997596/215261749-3c38405a-db74-422b-b70f-22b1f29e4816.png" width="400px">

- ARM Holdings는 칩 자체가 아닌 설계 구조를 판매하기 때문에 실제 기능이다 최적화는 개별 반도체 제조사에 따라 다르다.
- 명령 집합의 수가 적기 때문에 트랜지스터 수가 적다. 이를 통해 작은 크기, 낮은 전력소비, 낮은 발열, 속도 및 배터리 수명과 비용의 균형을 맞출 수 있다.


## ARM 특징

- ARM을 위해 개발된 프로그램은 오직 ARM 프로세서가 탑재된 기기에서만 실행할 수 있다. (x86 CPU 프로세서 기반 프로그램은 ARM 기반 기기에서 실행할 수 없다.)
- 하나의 ARM 기기에 동작하는 OS는 다른 ARM 기반 기기에서도 잘 동작한다.
- 오늘날 RISC와 CISC 자체의 속도는 큰 차이가 나지 않는다. CPU의 클럭 속도를 더 개선하기 힘든 현재, 명령어 길이가 일정하다는 특징이 명령어 병렬처리(Out-of-Order)에 유리하여, Apple의 M1칩이 CISC 기반 프로세스인 Intel과 AMD의 속도를 따라 잡았다.
- ARM 아키텍처는 현재 거의 모든 스마트폰 설계와 소형 모바일 장치, 노트북에서 사용되며, 슈퍼컴퓨터 중 하나인 Fugaku에서 ARM 프로세서가 사용되기도 했다.

---

## Reference

📄https://ko.wikipedia.org/wiki/축소_명령어_집합_컴퓨터
