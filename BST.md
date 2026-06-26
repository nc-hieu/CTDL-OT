# TỔNG HỢP THUẬT TOÁN CÂY NHỊ PHÂN VÀ BST

---

# **PHẦN 1: CÁC PHÉP DUYỆT CÂY (TRAVERSAL)**

## **THUẬT TOÁN 1: DUYỆT CÂY THEO THỨ TỰ GIỮA (LNR - INORDER)**

### **1. Tên thuật toán**
Duyệt cây nhị phân theo thứ tự Trái-Gốc-Phải (LNR - Inorder Traversal)

### **2. Ý tưởng**
- Đệ quy sang nhánh **Trái** trước
- Sau đó **thăm/xử lý** node gốc (in giá trị)
- Cuối cùng đệ quy sang nhánh **Phải**
- Với BST, LNR sẽ in các phần tử theo **thứ tự tăng dần**

### **3. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **4. Dữ liệu ra (Output)**
- Danh sách các phần tử in theo thứ tự LNR

### **5. Các bước**

**Bước 1:** Kiểm tra root == NULL → return

**Bước 2:** Đệ quy duyệt nhánh trái: LNR(root->left)

**Bước 3:** Thăm node gốc: in root->data

**Bước 4:** Đệ quy duyệt nhánh phải: LNR(root->right)

### **6. Ví dụ**

**Input:** Cây BST
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:** 20 30 40 50 60 70 80 (theo thứ tự tăng dần)

### **7. Mã C++**

```cpp
void LNR(Node* root) {
    if (root == nullptr) return;
    LNR(root->left);
    cout << root->data << " ";
    LNR(root->right);
}
```

---

## **THUẬT TOÁN 2: DUYỆT CÂY THEO THỨ TỰ TRƯỚC (NLR - PREORDER)**

### **1. Tên thuật toán**
Duyệt cây nhị phân theo thứ tự Gốc-Trái-Phải (NLR - Preorder Traversal)

### **2. Ý tưởng**
- **Thăm/xử lý** node gốc trước (in giá trị)
- Sau đó đệ quy sang nhánh **Trái**
- Cuối cùng đệ quy sang nhánh **Phải**
- NLR thường dùng để **sao chép cây** hoặc **lưu cây vào file**

### **3. Mã C++**

```cpp
void NLR(Node* root) {
    if (root == nullptr) return;
    cout << root->data << " ";
    NLR(root->left);
    NLR(root->right);
}
```

---

## **THUẬT TOÁN 3: DUYỆT CÂY THEO THỨ TỰ SAU (LRN - POSTORDER)**

### **1. Tên thuật toán**
Duyệt cây nhị phân theo thứ tự Trái-Phải-Gốc (LRN - Postorder Traversal)

### **2. Ý tưởng**
- Đệ quy sang nhánh **Trái** trước
- Sau đó đệ quy sang nhánh **Phải**
- Cuối cùng **thăm/xử lý** node gốc (in giá trị)
- LRN thường dùng để **xóa cây** hoặc **tính toán từ dưới lên**

### **3. Mã C++**

```cpp
void LRN(Node* root) {
    if (root == nullptr) return;
    LRN(root->left);
    LRN(root->right);
    cout << root->data << " ";
}
```

### **4. Bảng so sánh 3 duyệt**

| Loại | Tên | Thứ tự | Công dụng |
|------|-----|--------|----------|
| **LNR** | Inorder | Trái → Gốc → Phải | BST in tăng dần ✓ |
| **NLR** | Preorder | Gốc → Trái → Phải | Sao chép cây, lưu file |
| **LRN** | Postorder | Trái → Phải → Gốc | Xóa cây, tính toán từ dưới lên |

---

# **PHẦN 2: CÁC PHÉP CHÈN VÀ TÌM KIẾM TRONG BST**

## **THUẬT TOÁN 4: CHÈN PHẦN TỬ VÀO CÂY NHỊ PHÂN TÌM KIẾM**

### **1. Tên thuật toán**
Chèn phần tử vào cây nhị phân tìm kiếm (Insert Node in BST)

### **2. Ý tưởng**
- Sử dụng đệ quy để tìm vị trí chèn
- Nếu value < root->data, đệ quy sang nhánh trái
- Nếu value > root->data, đệ quy sang nhánh phải
- Nếu value == root->data, từ chối (không cho phép trùng)

### **3. Mã C++**

```cpp
bool insertNode(Node* &root, int value){
    if (root == nullptr){
        root = createNode(value);
        return true;
    }

    if (value < root->data) {
        return insertNode(root->left, value);
    }
    else if (value > root->data) {
        return insertNode(root->right, value);
    }

    return false;
}
```

---

## **THUẬT TOÁN 5: TÌM KIẾM PHẦN TỬ TRONG CÂY NHỊ PHÂN TÌM KIẾM**

### **1. Tên thuật toán**
Tìm kiếm phần tử trong cây nhị phân tìm kiếm (Search Node in BST)

### **2. Ý tưởng**
- Sử dụng đệ quy để tìm kiếm
- Tận dụng tính chất BST để tìm nhanh (không cần duyệt hết cây)
- Nếu root->data == value, return true (tìm thấy)

### **3. Mã C++**

```cpp
bool searchNode(Node* root, int value){
    if (root == nullptr) return false;

    if (root->data == value) return true;

    else if (value < root->data)
        return searchNode(root->left, value);
    else
        return searchNode(root->right, value);
}
```

---

## **THUẬT TOÁN 6: TÌM NODE CÓ GIÁ TRỊ NHỎ NHẤT TRONG CÂY BST**

### **1. Tên thuật toán**
Tìm node có giá trị nhỏ nhất trong cây nhị phân tìm kiếm (Find Minimum in BST)

### **2. Ý tưởng**
- Trong BST, giá trị nhỏ nhất luôn nằm **ở cực trái** của cây
- Đi sang trái cho tới khi root->left == NULL

### **3. Mã C++**

```cpp
Node* findMin(Node* root) {
    if (root == nullptr || root->left == nullptr) {
        return root;
    }
    return findMin(root->left);
}
```

---

## **THUẬT TOÁN 7: TÌM NODE CÓ GIÁ TRỊ LỚN NHẤT TRONG CÂY BST**

### **1. Tên thuật toán**
Tìm node có giá trị lớn nhất trong cây nhị phân tìm kiếm (Find Maximum in BST)

### **2. Ý tưởng**
- Trong BST, giá trị lớn nhất luôn nằm **ở cực phải** của cây
- Đi sang phải cho tới khi root->right == NULL

### **3. Mã C++**

```cpp
Node* findMax(Node* root) {
    if (root == nullptr || root->right == nullptr) {
        return root;
    }
    return findMax(root->right);
}
```

---

# **PHẦN 3: CÁC PHÉP ĐẾM VÀ TÍNH TOÁN TRÊN CÂY**

## **THUẬT TOÁN 8: ĐẾM SỐ NODE TRONG CÂY**

### **1. Tên thuật toán**
Đếm tổng số node trong cây nhị phân (Count Nodes)

### **2. Ý tưởng**
- Số node = 1 (node gốc) + số node nhánh trái + số node nhánh phải

### **3. Mã C++**

```cpp
int countNodes(Node* root) {
    if (root == nullptr) return 0;
    
    return 1 + countNodes(root->left) + countNodes(root->right);
}
```

---

## **THUẬT TOÁN 9: TÍNH TỔNG GIÁ TRỊ CÁC NODE TRONG CÂY**

### **1. Tên thuật toán**
Tính tổng giá trị của tất cả các node trong cây nhị phân (Sum Tree)

### **2. Ý tưởng**
- Tổng = giá trị node gốc + tổng nhánh trái + tổng nhánh phải

### **3. Mã C++**

```cpp
int sumTree(Node* root) { 
    if (root == nullptr) return 0; 
    return root->data + sumTree(root->left) + sumTree(root->right); 
}
```

---

## **THUẬT TOÁN 10: ĐẾM SỐ NODE LÁ TRONG CÂY**

### **1. Tên thuật toán**
Đếm số node lá trong cây nhị phân (Count Leaf Nodes)

### **2. Ý tưởng**
- Node lá = node không có con (left == NULL AND right == NULL)
- Nếu node hiện tại là lá, đếm được 1

### **3. Mã C++**

```cpp
int countLeaf(Node* root) {
    if (root == nullptr) return 0;

    if (root->left == nullptr && root->right == nullptr) {
        return 1;
    }

    return countLeaf(root->left) + countLeaf(root->right);
}
```

---

## **THUẬT TOÁN 11: TÍNH CHIỀU CAO CỦA CÂY**

### **1. Tên thuật toán**
Tính chiều cao (độ sâu) của cây nhị phân (Tree Height)

### **2. Ý tưởng**
- Chiều cao = 1 + max(chiều cao nhánh trái, chiều cao nhánh phải)

### **3. Mã C++**

```cpp
int height(Node* root) {
    if (root == nullptr) return 0;

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + max(leftHeight, rightHeight);
}
```

---

## **THUẬT TOÁN 12: ĐẾM SỐ NODE CÓ ĐÚNG 1 CON**

### **1. Tên thuật toán**
Đếm số node có đúng 1 con trong cây nhị phân (Count One Child Nodes)

### **2. Ý tưởng**
- Node có đúng 1 con = (left == NULL && right != NULL) XOR (left != NULL && right == NULL)

### **3. Mã C++**

```cpp
int countOneChild(Node* root){
    if(root == nullptr){
        return 0;
    }
    
    bool hasOneChild = (root->left == nullptr) != (root->right == nullptr);

    return hasOneChild + countOneChild(root->left) + countOneChild(root->right);
}
```

---

## **THUẬT TOÁN 13: ĐẾM SỐ NODE CÓ ĐỦ 2 CON**

### **1. Tên thuật toán**
Đếm số node có đúng 2 con trong cây nhị phân (Count Two Children Nodes)

### **2. Ý tưởng**
- Node có 2 con = (left != NULL) AND (right != NULL)

### **3. Mã C++**

```cpp
int countTwoChildren(Node* root){
    if(root == nullptr){
        return 0;
    }

    bool hasTwoChildren = (root->left != nullptr && root->right != nullptr);

    return hasTwoChildren + countTwoChildren(root->left) + countTwoChildren(root->right);
}
```

---

# **PHẦN 4: CÁC PHÉP ĐẾM CÓ ĐIỀU KIỆN TRONG BST**

## **THUẬT TOÁN 14: ĐẾM SỐ NODE CÓ GIÁ TRỊ LỚN HƠN X TRONG BST**

### **1. Tên thuật toán**
Đếm số node có giá trị lớn hơn x trong cây nhị phân tìm kiếm (Count Nodes Greater Than X)

### **2. Ý tưởng**
- Nếu root->data > x: cộng 1 + toàn bộ nhánh phải + tìm tiếp nhánh trái
- Nếu root->data ≤ x: chỉ tìm nhánh phải (tận dụng tính chất BST)

### **3. Mã C++**

```cpp
int countNodesGreaterThanX(Node* root, int x) {
    if (root == nullptr) {
        return 0;
    }
    
    if (root->data > x) {
        return 1 + countNodesGreaterThanX(root->right, x) + 
               countNodesGreaterThanX(root->left, x);
    } 
    else {
        return countNodesGreaterThanX(root->right, x);
    }
}
```

---

## **THUẬT TOÁN 15: ĐẾM SỐ NODE CÓ GIÁ TRỊ NHỎ HƠN X TRONG BST**

### **1. Tên thuật toán**
Đếm số node có giá trị nhỏ hơn x trong cây nhị phân tìm kiếm (Count Nodes Less Than X)

### **2. Ý tưởng**
- Nếu root->data < x: cộng 1 + toàn bộ nhánh trái + tìm tiếp nhánh phải
- Nếu root->data ≥ x: chỉ tìm nhánh trái (tận dụng tính chất BST)

### **3. Mã C++**

```cpp
int countNodesLessThanX(Node* root, int x) {
    if (root == nullptr) {
        return 0;
    }
    
    if (root->data < x) {
        return 1 + countNodesLessThanX(root->left, x) + 
               countNodesLessThanX(root->right, x);
    } 
    else {
        return countNodesLessThanX(root->left, x);
    }
}
```

---

# **PHẦN 5: CÁC PHÉP XÓA VÀ CHỈNH SỬA CÂY**

## **THUẬT TOÁN 16: IN CÁC NODE Ở MỘT MỨC (LEVEL) CỤ THỂ**

### **1. Tên thuật toán**
In các node ở một mức (level) cụ thể trong cây nhị phân (Print Nodes at Level)

### **2. Ý tưởng**
- Giảm level đi 1 mỗi lần đi sâu xuống 1 tầng
- Khi level == 1, in ra giá trị node
- Duyệt cả 2 nhánh để tìm hết các node ở level đó

### **3. Mã C++**

```cpp
void printNodesAtLevel(Node* root, int level) {
    if (root == nullptr || level <= 0) {
        return; 
    }
    
    if (level == 1) {
        cout << root->data << " ";
        return; 
    }
    
    printNodesAtLevel(root->left, level - 1);
    printNodesAtLevel(root->right, level - 1);
}
```

---

## **THUẬT TOÁN 17: XÓA NODE X TRONG CÂY BST**

### **1. Tên thuật toán**
Xóa node có giá trị x trong cây nhị phân tìm kiếm (Delete Node in BST)

### **2. Ý tưởng - 3 Trường hợp**

**TH1:** Node không có con → xóa luôn

**TH2:** Node có 1 con → kéo con lên thế

**TH3:** Node có 2 con → tìm node nhỏ nhất bên phải, copy giá trị, xóa node đó

### **3. Mã C++**

```cpp
bool deleteNode(Node* &root, int x) {
    if (root == nullptr) return false; 

    if (x < root->data) {
        return deleteNode(root->left, x);
    } 
    else if (x > root->data) {
        return deleteNode(root->right, x);
    } 
    else {
        Node* temp = root;

        if (root->left == nullptr) {
            root = root->right;
            delete temp;
            return true;
        } 
        else if (root->right == nullptr) {
            root = root->left;
            delete temp;
            return true;
        } 
        else {
            Node* substitute = root->right;
            while (substitute->left != nullptr) {
                substitute = substitute->left;
            }

            root->data = substitute->data;
            return deleteNode(root->right, substitute->data);
        }
    }
}
```

---

## **THUẬT TOÁN 18: XÓA TOÀN BỘ CÂY BST**

### **1. Tên thuật toán**
Xóa toàn bộ cây nhị phân tìm kiếm (Clear Tree / Delete Tree)

### **2. Ý tưởng**
- Dùng **duyệt Postorder (LRN)**: Trái → Phải → Gốc
- Xóa từ **lá lên gốc** để tránh mất con trỏ

### **3. Mã C++**

```cpp
void clear(Node* &root) {
    if (root == nullptr) {
        return;
    }
    clear(root->left);
    clear(root->right);
    delete root;
    root = nullptr;
}
```

---

## **THUẬT TOÁN 19: KIỂM TRA CÂY CÓ PHẢI LÀ BST KHÔNG (DÙNG INORDER)**

### **1. Tên thuật toán**
Kiểm tra cây nhị phân có phải là BST không sử dụng duyệt Inorder (Verify BST using Inorder)

### **2. Ý tưởng**
- **Tính chất BST:** Duyệt Inorder → Dãy **tăng dần nghiêm ngặt**
- Giữ con trỏ **prev** = node duyệt trước đó
- Nếu node hiện tại ≤ prev → **KHÔNG phải BST**

### **3. Mã C++**

```cpp
bool isInOrderBST(Node* root, Node* &prev) {
    if (root == nullptr) {
        return true;
    }

    if (!isInOrderBST(root->left, prev)) {
        return false;
    }

    if (prev != nullptr && root->data <= prev->data) {
        return false;
    }
    prev = root;

    return isInOrderBST(root->right, prev);
}

bool isBSTInOrder(Node* root) {
    Node* prev = nullptr;
    return isInOrderBST(root, prev);
}
```

---

# **BẢNG TỔNG HỢP 19 THUẬT TOÁN**

| # | Tên thuật toán | Loại | Ý tưởng chính | Độ khó |
|---|---|---|---|---|
| 1 | LNR (Inorder) | Duyệt | Trái → Gốc → Phải | ⭐ |
| 2 | NLR (Preorder) | Duyệt | Gốc → Trái → Phải | ⭐ |
| 3 | LRN (Postorder) | Duyệt | Trái → Phải → Gốc | ⭐ |
| 4 | insertNode | Chèn | Đệ quy tìm vị trí | ⭐⭐ |
| 5 | searchNode | Tìm | Tìm kiếm BST | ⭐⭐ |
| 6 | findMin | Tìm | Cực trái | ⭐ |
| 7 | findMax | Tìm | Cực phải | ⭐ |
| 8 | countNodes | Đếm | 1 + trái + phải | ⭐ |
| 9 | sumTree | Tính | data + trái + phải | ⭐ |
| 10 | countLeaf | Đếm | Đếm node lá | ⭐ |
| 11 | height | Tính | 1 + max(trái, phải) | ⭐⭐ |
| 12 | countOneChild | Đếm | Node 1 con | ⭐⭐ |
| 13 | countTwoChildren | Đếm | Node 2 con | ⭐⭐ |
| 14 | countGreaterThanX | Đếm | Tận dụng BST | ⭐⭐ |
| 15 | countLessThanX | Đếm | Tận dụng BST | ⭐⭐ |
| 16 | printNodesAtLevel | In | Giảm level | ⭐⭐ |
| 17 | deleteNode | Xóa | 3 trường hợp | ⭐⭐⭐ |
| 18 | clear | Xóa | Postorder | ⭐ |
| 19 | isBSTInOrder | Kiểm tra | Duyệt Inorder | ⭐⭐ |

---
