Một trong những kĩ thuật cơ bản nhất liên quan đến cây đó chính là duyệt toàn bộ cây đó. Ta có hai phương pháp cơ bản để duyệt cây đó là BFS - duyệt theo chiều rộng và DFS là duyệt theo chiều sâu. 
## Setup
BFS và DFS là kĩ thuật duyệt cây/đồ thị cho nên trước khi thực hành thì ta cần biểu diễn đồ thị dưới dạng code. 
Một trong những cách đơn giản và hiệu quả nhất để biểu diễn đồ thị đó là sử dụng danh sách cạnh kề, thường dưới dạng một hash map, với mỗi key biểu diễn một nodes và values của nó là các cạnh kề với nodes. Chẳng hạn:
```python
graph = {
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
```
Danh sách trên tương đương với cây dưới đây: 
![[Pasted image 20250924205825.png]]

Trong phạm vi bài này thì ta sẽ chỉ đề cập đến các đồ thị không có trọng số và đồ thị vô hướng như đồ thị ở hình trên.
## Breadth First Search
Thuật toán tìm kiếm theo chiều rộng là thuật toán duyệt bắt đầu từ gốc, sau đó lần lượt xét qua các node của một cây theo ưu tiên về độ sâu từ nhỏ đến lớn.
Ở đây ta hiểu độ sâu của một node là số cạnh cần thiết để đi từ node gốc tới node cần xét.

```python

```