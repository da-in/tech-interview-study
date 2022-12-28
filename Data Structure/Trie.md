# 트라이(Trie)

**트라이(Trie)** 는 문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조이다. 검색어 자동 완성, 사전 검색 등에 유용하다.

트라이의 어원은 re<b>tri</b>eval tree(검색트리)의 **tri** (트리)라고 불렸으나, tree와 발음상 구분되지 않아 trie(트라이)라고 부르게 되었다.

<p>
  <img align="top" src="https://user-images.githubusercontent.com/66757141/209826134-e6663efd-01f1-4a18-a472-212120fdca0c.png" alt="Trie_example svg" width="400px" />
  <img align="top" src="https://user-images.githubusercontent.com/66757141/209834538-7e137cd7-1363-4778-b6f9-30f23551dfc9.png" alt="Trie_example svg" width="300px" />
</p>

[_아래 예시 이미지 출처 - youseop.github.io_](https://youseop.github.io/2020-11-09-BAEKJOON-14425_%EB%AC%B8%EC%9E%90%EC%97%B4%EC%A7%91%ED%95%A9/)

트라이 자료구조의 각 노드는 아래와 같이 `key`, `data`, `child` 값을 갖는다. `key`는 현재 노드에서 추가된 문자열(접두사), `data`는 현재 노드에서 완성된 문자열(끝 표시), `child`는 자식 노드를 의미한다.

![p3GjBIm](https://user-images.githubusercontent.com/66757141/209830220-44c2ee5a-1070-4885-92a9-401fd07a4cde.jpg)

## Trie 문자열 삽입

왼쪽은 이 노드를 사용하여 문자열을 Trie 자료구조에 삽입하는 경우이다. 'abc'를 삽입하면 아래와 같이 'a', 'b', 'c'를 키로 갖는 노드들이 생성되고, 마지막 노드인 'c' 노드의 `data`에 완성된 값인 'abc'가 입력된다.

오른쪽은 위 예시에 이어서 문자열 'ab'를 삽입한 예시이다.

<div>
  <img src="https://user-images.githubusercontent.com/66757141/209830236-6a70ba2b-de64-4e3a-9fd7-34dafe808482.jpg" alt="6fux7GL">
  <img src="https://user-images.githubusercontent.com/66757141/209830242-95512a9f-c0f4-4172-aec0-39fdb2126725.jpg" alt="6IA9gxP">
</div>

다음으로 문자열 'car'을 삽입한 예시이다.

<img src="https://user-images.githubusercontent.com/66757141/209830251-8ca01cc2-8fa5-4f1b-8062-af22fb2077b6.jpg" alt="mqprLVa" width="500px" />

<br/>

## Trie 문자열 탐색

위 이미지에서 문자열 'abc'가 있는지 탐색하는 경우, 차례로 'a', 'b', 'c' 노드를 방문하여 최종적으로 Data에 해당 문자열이 있는지(끝 표시)를 확인한다. 중간에 노드가 없거나, Data에 값이 없는 경우 해당 문자열은 Trie에 존재하지 않는다.

<br/>

## Trie 장단점

- **문자열 추가** 시 길이만큼의 노드를 거치고 생성하기에 $O(L)$ \* 의 시간복잡도를 갖는다.

- **문자열 탐색** 시 모든 문자열과 일치 여부를 확인하는 것 $O(n)$ 이 아니라, 찾고자 하는 문자열의 길이 만큼의 노드만을 거쳐 탐색 $O(L)$ 하므로 시간 복잡도 측면에서 훨씬 더 효율적이다.

- **이진탐색트리(Binary Search Tree, BST)** 에서 탐색이 정수형일 때에는 값을 바로 비교하므로 시간복잡도가 $O(log n)$ 이지만, 문자열을 탐색할 경우 $O(L * log n)$ 로 좋지 않고, Trie는 이에 최적화되어있다.

  _\* $L$ 은 문자열의 길이_

- 모든 문자열들의 접두사(문자)의 경우의 수를 노드로 갖고 포인터 정보를 저장하기 때문에 **공간복잡도에서 치명적이다** .

<br/>

## Trie 구현

```python
# Python program for insert and search
# operation in a Trie
class TrieNode:
    # Trie node class
    def __init__(self):
        self.children = [None]*26
        # isEndOfWord is True if node represent the end of the word
        self.isEndOfWord = False

class Trie:
    # Trie data structure class
    def __init__(self):
        self.root = self.getNode()
    def getNode(self):
        # Returns new trie node (initialized to NULLs)
        return TrieNode()
    def _charToIndex(self,ch):
        # private helper function
        # Converts key current character into index
        # use only 'a' through 'z' and lower case
        return ord(ch)-ord('a')
    def insert(self,key):
        # If not present, inserts key into trie
        # If the key is prefix of trie node,
        # just marks leaf node
        pCrawl = self.root
        length = len(key)
        for level in range(length):
            index = self._charToIndex(key[level])
            # if current character is not present
            if not pCrawl.children[index]:
                pCrawl.children[index] = self.getNode()
            pCrawl = pCrawl.children[index]
        # mark last node as leaf
        pCrawl.isEndOfWord = True
    def search(self, key):
        # Search key in the trie
        # Returns true if key presents
        # in trie, else false
        pCrawl = self.root
        length = len(key)
        for level in range(length):
            index = self._charToIndex(key[level])
            if not pCrawl.children[index]:
                return False
            pCrawl = pCrawl.children[index]
        return pCrawl.isEndOfWord

# This code is contributed by Atul Kumar (www.facebook.com/atul.kr.007)
```

---

## Reference

📄https://ko.wikipedia.org/wiki/트라이_(컴퓨팅)  
📄https://youseop.github.io/2020-11-09-BAEKJOON-14425_%EB%AC%B8%EC%9E%90%EC%97%B4%EC%A7%91%ED%95%A9/  
📄https://velog.io/@kimdukbae/자료구조-트라이-Trie  
📄https://www.geeksforgeeks.org/trie-insert-and-search/
