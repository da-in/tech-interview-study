# 트라이(Trie)

트라이(Trie)는 문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조이다.

트라이의 어원은 re<b>tri</b>eval tree(검색트리)의 tri(트리)라고 불렸으나, tree와 발음상 구분되지 않아 trie(트라이)라고 부르게 되었다.

<img src="https://user-images.githubusercontent.com/66757141/209826134-e6663efd-01f1-4a18-a472-212120fdca0c.png" alt="Trie_example svg" width="500px" />

[_예시 이미지 출처 - youseop.github.io_](https://youseop.github.io/2020-11-09-BAEKJOON-14425_%EB%AC%B8%EC%9E%90%EC%97%B4%EC%A7%91%ED%95%A9/)

트라이 자료구조의 각 노드는 아래와 같이 `key`, `data`, `child` 값을 갖는다. `key`는 현재 노드에서 추가된 문자열, `data`는 현재 노드에서 완성된 문자열, `child`는 자식 노드를 의미한다.

![p3GjBIm](https://user-images.githubusercontent.com/66757141/209830220-44c2ee5a-1070-4885-92a9-401fd07a4cde.jpg)

## Trie 삽입

다음은 이 노드를 사용하여 문자열을 Trie 자료구조에 삽입하는 경우이다. 'abc'를 삽입하면 아래와 같이 'a', 'b', 'c'를 키로 갖는 노드들이 생성되고, 마지막 노드인 'c' 노드의 `data`에 완성된 값인 'abc'가 입력된다.

![6fux7GL](https://user-images.githubusercontent.com/66757141/209830236-6a70ba2b-de64-4e3a-9fd7-34dafe808482.jpg)

위 예시에 이어서 문자열 'ab'를 삽입한 예시이다.

![6IA9gxP](https://user-images.githubusercontent.com/66757141/209830242-95512a9f-c0f4-4172-aec0-39fdb2126725.jpg)

다음으로 문자열 'car'을 삽입한 예시이다.

<img src="https://user-images.githubusercontent.com/66757141/209830251-8ca01cc2-8fa5-4f1b-8062-af22fb2077b6.jpg" alt="mqprLVa" width="500px" />

<br/>

## Trie 탐색

## Trie 장단점

- 문자열 검색을 빠르게 한다.
- 문자열을 탐색할 때, 하나하나씩 전부 비교하면서 탐색을 하는 것보다 시간 복잡도 측면에서 훨씬 더 효율적이다.
- 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있으므로 메모리 측면에서 비효율적이다.

---

## Reference

📄https://ko.wikipedia.org/wiki/트라이_(컴퓨팅)  
📄https://youseop.github.io/2020-11-09-BAEKJOON-14425_%EB%AC%B8%EC%9E%90%EC%97%B4%EC%A7%91%ED%95%A9/  
📄https://velog.io/@kimdukbae/자료구조-트라이-Trie
