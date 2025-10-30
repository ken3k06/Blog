Về lí thuyết cơ bản về graph mình có note ở đây:  [[Math/Graph Theory/Các khái niệm cơ bản|Các khái niệm cơ bản]]
Tham khảo: https://www.freecodecamp.org/news/graph-algorithms-in-python-bfs-dfs-and-beyond/

## Biểu diễn đồ thị 

Có 2 cách chính để biểu diễn một đồ thị trong ngôn ngữ lập trình đó là sử dụng ma trận kề hoặc danh sách kề. 
Danh sách kề là một danh sách có dạng đỉnh - đỉnh kề như sau:
```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}
```
Tức là từ $A$ có cạnh nối đến hai đỉnh $B$ và $C$.
Còn nếu dùng ma trận kề thì ta biểu diễn như sau:
```python
# A, B, C, D
matrix = [
    [0, 1, 1, 0],  # A
    [1, 0, 0, 1],  # B
    [1, 0, 0, 0],  # C
    [0, 1, 0, 0]   # D
]
```
Trong bài này thì mình sẽ sử dụng danh sách kề để biểu diễn đồ thị và đồ thị sẽ là đồ thị vô hướng. 

Tuy nhiên, mỗi cách biểu diễn sẽ có ưu và nhược điểm riêng mà mình sẽ đề cập sau. 

Cài đặt có thể tham khảo tại đây: https://github.com/YuriiBarninets/graph

## Thực hành 
Ví dụ ta có đồ thị như sau:
```python
sample = {
    'A': ['B'],
    'B': ['A', 'C', 'H'],
    'C': ['B', 'D'],
    'D': ['C', 'E', 'G'],
    'E': ['D', 'F'],
    'F': ['E'],
    'G': ['D'],
    'H': ['B', 'I', 'J', 'M'],
    'I': ['H'],
    'J': ['H', 'K'],
    'K': ['J', 'L'],
    'L': ['K'],
    'M': ['H']
}

class Graph:
    def __init__(self, directed = False):
        self.graph = {}
        self.directed = directed 
    def add_vertex(self, v):
        if v not in self.graph:
            self.graph[v] = []
    def add_edge(self, u, v):
        if u not in self.graph:
            self.add_vertex(u)
        if v not in self.graph:
            self.add_vertex(v)
        if v not in self.graph[u]:
            self.graph[u].append(v)
        if not self.directed and u not in self.graph[v]:
            self.graph[v].append(u)
    def remove_edge(self, u, v):
        if u in self.graph and v in self.graph[u]:
            self.graph[u].remove(v)
        if not self.directed and v in self.graph and u in self.graph[v]:
            self.graph[v].remove(u)
    def remove_vertex(self,v):
        if v in self.graph:
            del self.graph[v]
        for key in self.graph:
            if v in self.graph[key]:
                self.graph[key].remove(v)
    def display(self):
        for v in self.graph:
            print(f"{v} --> {self.graph[v]}")
sample = {
    'A': ['B'],
    'B': ['A', 'C', 'H'],
    'C': ['B', 'D'],
    'D': ['C', 'E', 'G'],
    'E': ['D', 'F'],
    'F': ['E'],
    'G': ['D'],
    'H': ['B', 'I', 'J', 'M'],
    'I': ['H'],
    'J': ['H', 'K'],
    'K': ['J', 'L'],
    'L': ['K'],
    'M': ['H']
}
G = Graph()
for key in sample:
    adj = sample[key]
    for ver in adj:
        G.add_edge(key, ver)
G.display()
```
![[Pasted image 20251028212350.png]]

Có hai thuật toán quan trọng trên đồ thị đó chính là DFS và BFS

### Breadth First Search 

Thuật toán BFS hay còn gọi là thuật toán duyệt đồ thị ưu tiên chiều rộng, là một trong những thuật toán tìm kiếm cơ bản và thiết yếu trên đồ thị. Mà trong đó, những đỉnh nào gần đỉnh xuất phát hơn sẽ được duyệt trước. 


