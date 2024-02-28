# BST (Binary Search Tree)

### 이진 탐색 트리
- 이진 트리의 일종으로 부모 노드의 왼쪽 자식 노드는 부모 노드보다 값이 작고, 오른쪽 자식 노드는 부모 노드보다 값이 큰 상태로 만들어진 트리.

### 속성
- 모든 노드는 서로 다른 유일한 키를 가진다. 즉, <b>중복 값이 없음</b>
- 노드의 왼쪽 서브트리에는 그 노드의 값보다 작은 값을 지닌 노드만이 존재한다.
- 노드의 오른쪽 서브트리에는 그 노드의 값보다 큰 값을 지닌 노드만이 존재한다.
- 이진 트리의 성질을 물려받았다.
- 주로 연결 리스트(LinkedList)로 이루어진다.
- 중위 순회(inorder traverse)할 경우 키 값의 오름차순으로 순회한다.

### 시간 복잡도 - O(h)
(h : 트리의 높이)

### 탐색
1. 탐색하고자 하는 값을 루트 노드와 먼저 비교한다.
2. 루트 노드보다 작다면 왼쪽 서브 트리에서 찾는다.
3. 루트 노드보다 크다면 오른쪽 서브 트리에서 찾는다.
4. 찾고자 하는 값을 찾을 때까지 반복한다.

### 삽입
1. 삽입하려는 값을 탐색한다.
2. 삽입하려는 키가 없다면 탐색이 마지막으로 이뤄진 리프 노드의 키와 비교해서 왼쪽 혹은 오른쪽에 삽입한다. => 항상 리프 노드에 추가

```
void insert(TreeNode** root, int key) {
    TreeNode* ptr;     // 탐색을 진행할 포인터 
    TreeNode* newNode = (TreeNode*)malloc(sizeof(TreeNode));    // newNode 생성
    newNode->key = key;
    newNode->left = newNode->right = NULL; 
    
    if(*root == NULL){    // 트리가 비어 있을 경우 
        *root = newNode;
        return;
    }
    
    ptr = *root;    // root 노드부터 탐색 진행  
    
    while(ptr){
        if(key == ptr->key){    // 중복값 
            printf("Error : 중복값은 허용되지 않습니다!\n");
            return;
        }else if(key < ptr->key){    // 왼쪽 서브트리 
            if(ptr->left == NULL){    // 비어있다면 추가 
                ptr->left = newNode;
                return;
            }else{    // 비어있지 않다면 다시 탐색 진행 
                ptr= ptr->left;
            }
        }else{    // key > ptr->key 오른쪽 서브트리 
            if(ptr->right == NULL){    // 비어있다면 추가 
                ptr->right = newNode;
                return;
            }else{    // 비어있지 않다면 다시 탐색 진행 
                ptr = ptr->right;
            }
        }
    }
    
}
출처: https://code-lab1.tistory.com/10 [코드 연구소:티스토리]
```

### 삭제
- 삭제하는 노드가 리프노드라면 *(자식 노드가 없다면)* 노드를 삭제
- 자식 노드가 1개라면 해당 노드를 삭제하고, 자식 노드를 삭제한 노드의 위치로 옮긴다.
- 자식 노드가 2개라면
    1. 삭제할 노드 왼쪽 서브 트리의 가장 큰 자손을 삭제한 노드의 자리에 올린다.
    2. 삭제할 노드 오른쪽 서브 트리의 가장 작은 자손을 삭제한 노드의 자리에 올린다.

### 장점
- 탐색시 시간 복잡도가 줄어든다.(평균적으로 O(logN)
- 데이터를 삽입하거나 삭제해도 정렬이 유지된다.

### 단점
- 편항 트리가 될 수 있다.(최악의 경우 O(N)까지 가능)
