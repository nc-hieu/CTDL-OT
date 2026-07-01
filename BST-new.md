# TỔNG HỢP THUẬT TOÁN CÂY NHỊ PHÂN VÀ BST
---

# **PHẦN 1: CÁC PHÉP DUYỆT CÂY (TRAVERSAL)**

## **THUẬT TOÁN 1: DUYỆT CÂY THEO THỨ TỰ GIỮA (LNR - INORDER)**

### **1. Ý tưởng & Các bước thực hiện**

Để duyệt cây theo thứ tự Trái-Gốc-Phải:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, không có gì để duyệt, return

**Bước 2:** Đệ quy duyệt nhánh trái trước
- Gọi `LNR(root->left)` để xử lý toàn bộ cây con bên trái trước
- Đảm bảo các giá trị nhỏ hơn root được xử lý trước (với BST)

**Bước 3:** Thăm (xử lý) node gốc
- In ra giá trị `root->data` sau khi đã duyệt xong nhánh trái

**Bước 4:** Đệ quy duyệt nhánh phải
- Gọi `LNR(root->right)` để xử lý toàn bộ cây con bên phải
- Với BST, các giá trị này luôn lớn hơn root

**Ghi chú:** Với cây BST, vì luôn duyệt trái trước (nhỏ hơn) → gốc → phải (lớn hơn), kết quả luôn là dãy **tăng dần**

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Danh sách các phần tử in theo thứ tự LNR

### **4. Ví dụ**

**Input:** Cây BST
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:** 20 30 40 50 60 70 80 (theo thứ tự tăng dần)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để duyệt cây theo thứ tự Gốc-Trái-Phải:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, return

**Bước 2:** Thăm (xử lý) node gốc ngay lập tức
- In ra giá trị `root->data` trước tiên, ngay khi vào node này

**Bước 3:** Đệ quy duyệt nhánh trái
- Gọi `NLR(root->left)` để xử lý toàn bộ cây con bên trái

**Bước 4:** Đệ quy duyệt nhánh phải
- Gọi `NLR(root->right)` để xử lý toàn bộ cây con bên phải

**Ghi chú:** Vì node gốc luôn được xử lý đầu tiên, NLR thường dùng để **sao chép cây** (copy gốc trước rồi mới copy con) hoặc **lưu cấu trúc cây vào file** (ghi gốc trước để khi đọc lại có thể dựng cây từ trên xuống)

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Danh sách các phần tử in theo thứ tự NLR

### **4. Ví dụ**

**Input:** Cây BST (như ví dụ trên)

**Output:** 50 30 20 40 70 60 80 (gốc trước)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để duyệt cây theo thứ tự Trái-Phải-Gốc:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, return

**Bước 2:** Đệ quy duyệt nhánh trái trước
- Gọi `LRN(root->left)` để xử lý toàn bộ cây con bên trái

**Bước 3:** Đệ quy duyệt nhánh phải
- Gọi `LRN(root->right)` để xử lý toàn bộ cây con bên phải

**Bước 4:** Thăm (xử lý) node gốc cuối cùng
- In ra giá trị `root->data` sau khi đã duyệt xong cả 2 nhánh con

**Ghi chú:** Vì node gốc luôn được xử lý sau cùng (sau khi xử lý hết con), LRN thường dùng để **xóa cây** (phải xóa hết con trước khi xóa cha, tránh mất con trỏ) hoặc **tính toán từ dưới lên** (như tính chiều cao, tổng giá trị - cần biết kết quả của con trước khi tính cho cha)

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Danh sách các phần tử in theo thứ tự LRN

### **4. Ví dụ**

**Input:** Cây BST (như ví dụ trên)

**Output:** 20 40 30 60 80 70 50 (lá trước, gốc cuối)

### **5. Mã C++**

```cpp
void LRN(Node* root) {
    if (root == nullptr) return;
    LRN(root->left);
    LRN(root->right);
    cout << root->data << " ";
}
```

### **6. Bảng so sánh 3 duyệt**

| Loại | Tên | Thứ tự | Công dụng |
|------|-----|--------|----------|
| **LNR** | Inorder | Trái → Gốc → Phải | BST in tăng dần ✓ |
| **NLR** | Preorder | Gốc → Trái → Phải | Sao chép cây, lưu file |
| **LRN** | Postorder | Trái → Phải → Gốc | Xóa cây, tính toán từ dưới lên |

---

# **PHẦN 2: CÁC PHÉP CHÈN VÀ TÌM KIẾM TRONG BST**

## **THUẬT TOÁN 4: CHÈN PHẦN TỬ VÀO CÂY NHỊ PHÂN TÌM KIẾM**

### **1. Ý tưởng & Các bước thực hiện**

Để chèn một phần tử vào cây BST:

**Bước 1:** Kiểm tra node hiện tại có rỗng không
- Nếu `root == nullptr`: đây là vị trí cần chèn
  - Gọi `createNode(value)` để tạo node mới và gán cho root
  - Return true (chèn thành công)

**Bước 2:** So sánh giá trị cần chèn với node hiện tại
- Nếu `value < root->data`: giá trị nhỏ hơn, phải nằm bên nhánh trái
  - Đệ quy: `return insertNode(root->left, value)`

**Bước 3:** Kiểm tra nếu giá trị lớn hơn
- Nếu `value > root->data`: giá trị lớn hơn, phải nằm bên nhánh phải
  - Đệ quy: `return insertNode(root->right, value)`

**Bước 4:** Xử lý trường hợp giá trị đã tồn tại
- Nếu `value == root->data`: giá trị đã có trong cây
  - Return false (từ chối chèn, không cho phép trùng lặp trong BST)

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây
- value: giá trị cần chèn

### **3. Dữ liệu ra (Output)**
- true: nếu chèn thành công
- false: nếu giá trị đã tồn tại

### **4. Ví dụ**

**Input:** Cây rỗng, chèn lần lượt: 50, 30, 70, 20, 40

**Output:**
```
        50
       /  \
      30   70
     / \
    20 40
```

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để tìm kiếm một giá trị trong cây BST:

**Bước 1:** Kiểm tra điều kiện dừng (không tìm thấy)
- Nếu `root == nullptr`: đã đi tới cây con rỗng mà chưa tìm thấy
  - Return false

**Bước 2:** Kiểm tra giá trị tại node hiện tại
- Nếu `root->data == value`: đã tìm thấy giá trị cần tìm
  - Return true

**Bước 3:** So sánh để quyết định hướng tìm tiếp
- Nếu `value < root->data`: giá trị cần tìm nhỏ hơn, chỉ có thể nằm bên trái
  - Đệ quy: `return searchNode(root->left, value)`

**Bước 4:** Tìm ở nhánh phải nếu cần
- Nếu `value > root->data`: giá trị cần tìm lớn hơn, chỉ có thể nằm bên phải
  - Đệ quy: `return searchNode(root->right, value)`

**Ghi chú:** Nhờ tận dụng tính chất BST (trái < gốc < phải), thuật toán không cần duyệt toàn bộ cây mà chỉ đi theo 1 nhánh duy nhất, giúp tìm kiếm nhanh hơn nhiều so với duyệt tuần tự

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây
- value: giá trị cần tìm

### **3. Dữ liệu ra (Output)**
- true: nếu tìm thấy
- false: nếu không tìm thấy

### **4. Ví dụ**

**Input:** Cây: 50 → (30, 70) → (20, 40, 60, 80), tìm 40

**Output:** true (tìm thấy)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để tìm node có giá trị nhỏ nhất:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr` hoặc `root->left == nullptr`: 
  - Nếu cây rỗng, không có gì để tìm
  - Nếu node hiện tại không còn con trái, đây chính là node nhỏ nhất
  - Return root

**Bước 2:** Nếu chưa phải, tiếp tục đi sâu sang trái
- Đệ quy: `return findMin(root->left)`
- Vì trong BST, mọi giá trị bên trái luôn nhỏ hơn node hiện tại

**Ghi chú:** Lặp lại quá trình này cho tới khi gặp node không còn con trái (`left == NULL`), đó chính là node có giá trị nhỏ nhất trong toàn cây

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Con trỏ tới node có giá trị nhỏ nhất
- Nếu cây rỗng (root == NULL) trả về NULL

### **4. Ví dụ**

**Input:** Cây BST
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:** Node chứa giá trị 20 (node cực trái)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để tìm node có giá trị lớn nhất:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr` hoặc `root->right == nullptr`:
  - Nếu cây rỗng, không có gì để tìm
  - Nếu node hiện tại không còn con phải, đây chính là node lớn nhất
  - Return root

**Bước 2:** Nếu chưa phải, tiếp tục đi sâu sang phải
- Đệ quy: `return findMax(root->right)`
- Vì trong BST, mọi giá trị bên phải luôn lớn hơn node hiện tại

**Ghi chú:** Lặp lại quá trình này cho tới khi gặp node không còn con phải (`right == NULL`), đó chính là node có giá trị lớn nhất trong toàn cây

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Con trỏ tới node có giá trị lớn nhất
- Nếu cây rỗng (root == NULL) trả về NULL

### **4. Ví dụ**

**Input:** Cây BST (như ví dụ trên)

**Output:** Node chứa giá trị 80 (node cực phải)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để đếm tổng số node trong cây:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, có 0 node, return 0

**Bước 2:** Đếm số node của nhánh trái
- Gọi đệ quy `countNodes(root->left)` để đếm tổng số node bên nhánh trái

**Bước 3:** Đếm số node của nhánh phải
- Gọi đệ quy `countNodes(root->right)` để đếm tổng số node bên nhánh phải

**Bước 4:** Cộng tổng và trả về kết quả
- Return `1 + countNodes(root->left) + countNodes(root->right)`
- Số 1 đại diện cho chính node gốc hiện tại, cộng thêm số node ở 2 nhánh con

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng số node trong cây

### **4. Ví dụ**

**Input:** Cây
```
        A
       / \
      B   C
     / \
    D   E
```

**Output:** 5 node (A, B, C, D, E)

### **5. Mã C++**

```cpp
int countNodes(Node* root) {
    if (root == nullptr) return 0;
    
    return 1 + countNodes(root->left) + countNodes(root->right);
}
```

---

## **THUẬT TOÁN 9: TÍNH TỔNG GIÁ TRỊ CÁC NODE TRONG CÂY**

### **1. Ý tưởng & Các bước thực hiện**

Để tính tổng giá trị tất cả các node:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, tổng = 0, return 0

**Bước 2:** Tính tổng giá trị của nhánh trái
- Gọi đệ quy `sumTree(root->left)` để tính tổng giá trị bên nhánh trái

**Bước 3:** Tính tổng giá trị của nhánh phải
- Gọi đệ quy `sumTree(root->right)` để tính tổng giá trị bên nhánh phải

**Bước 4:** Cộng tổng và trả về kết quả
- Return `root->data + sumTree(root->left) + sumTree(root->right)`
- Cộng giá trị node hiện tại với tổng giá trị của 2 nhánh con

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây (các node chứa giá trị số)

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng giá trị tất cả node

### **4. Ví dụ**

**Input:** Cây
```
        10
       /  \
      5    15
     / \
    2   3
```

**Output:** 10 + 5 + 15 + 2 + 3 = **35**

### **5. Mã C++**

```cpp
int sumTree(Node* root) { 
    if (root == nullptr) return 0; 
    return root->data + sumTree(root->left) + sumTree(root->right); 
}
```

---

## **THUẬT TOÁN 10: ĐẾM SỐ NODE LÁ TRONG CÂY**

### **1. Ý tưởng & Các bước thực hiện**

Để đếm số node lá (node không có con):

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, có 0 lá, return 0

**Bước 2:** Kiểm tra node hiện tại có phải là lá không
- Nếu `root->left == nullptr && root->right == nullptr`: 
  - Node này không có con trái lẫn con phải → đây là node lá
  - Return 1 (đếm được 1 lá)

**Bước 3:** Nếu không phải lá, tiếp tục tìm ở 2 nhánh con
- Đệ quy đếm lá bên nhánh trái: `countLeaf(root->left)`
- Đệ quy đếm lá bên nhánh phải: `countLeaf(root->right)`

**Bước 4:** Cộng kết quả từ 2 nhánh và trả về
- Return `countLeaf(root->left) + countLeaf(root->right)`
- Lưu ý: không cộng thêm 1 vì node hiện tại không phải lá

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng số node lá trong cây

### **4. Ví dụ**

**Input:** Cây
```
        A
       / \
      B   C
     / \
    D   E
```

**Output:** 3 lá (D, E, C)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để tính chiều cao (số tầng) của cây:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, chiều cao = 0, return 0

**Bước 2:** Tính chiều cao của nhánh trái
- Gọi đệ quy `leftHeight = height(root->left)` để đo chiều cao nhánh trái

**Bước 3:** Tính chiều cao của nhánh phải
- Gọi đệ quy `rightHeight = height(root->right)` để đo chiều cao nhánh phải

**Bước 4:** Chọn nhánh cao hơn và cộng thêm tầng hiện tại
- So sánh `max(leftHeight, rightHeight)` để lấy nhánh có chiều cao lớn hơn
- Return `1 + max(leftHeight, rightHeight)` (cộng thêm 1 tầng của chính node hiện tại)

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Số nguyên = chiều cao cây (số tầng)

### **4. Ví dụ**

**Input:** Cây
```
        A
       / \
      B   C
     / \
    D   E
```

**Output:** 3 (tầng)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để đếm số node chỉ có đúng 1 con (trái hoặc phải, không phải cả 2):

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, return 0

**Bước 2:** Kiểm tra node hiện tại có đúng 1 con không
- Dùng phép XOR: `(root->left == nullptr) != (root->right == nullptr)`
- Biểu thức này trả về true nếu một bên NULL còn bên kia không NULL (chỉ có 1 con)
- Lưu kết quả vào `hasOneChild` (true = 1, false = 0)

**Bước 3:** Đếm tiếp ở nhánh trái và nhánh phải
- Đệ quy đếm: `countOneChild(root->left)` và `countOneChild(root->right)`

**Bước 4:** Cộng tổng và trả về kết quả
- Return `hasOneChild + countOneChild(root->left) + countOneChild(root->right)`
- Cộng kết quả node hiện tại (0 hoặc 1) với kết quả từ 2 nhánh con

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng số node có đúng 1 con

### **4. Ví dụ**

**Input:** Cây
```
        A (2 con)
       / \
      B   C (1 con: B)
     / \
    D   E (0 con)
```

**Output:** 1 node (C có đúng 1 con)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để đếm số node có đầy đủ 2 con (cả trái và phải):

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, return 0

**Bước 2:** Kiểm tra node hiện tại có đủ 2 con không
- Dùng phép AND: `root->left != nullptr && root->right != nullptr`
- Biểu thức trả về true chỉ khi cả con trái và con phải đều tồn tại
- Lưu kết quả vào `hasTwoChildren` (true = 1, false = 0)

**Bước 3:** Đếm tiếp ở nhánh trái và nhánh phải
- Đệ quy đếm: `countTwoChildren(root->left)` và `countTwoChildren(root->right)`

**Bước 4:** Cộng tổng và trả về kết quả
- Return `hasTwoChildren + countTwoChildren(root->left) + countTwoChildren(root->right)`
- Cộng kết quả node hiện tại (0 hoặc 1) với kết quả từ 2 nhánh con

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng số node có đúng 2 con

### **4. Ví dụ**

**Input:** Cây
```
        A (2 con) ✓
       / \
      B   C (1 con)
     / \
    D   E (0 con)
```

**Output:** 2 node (A và B đều có 2 con)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để đếm số node có giá trị lớn hơn x (tận dụng tính chất BST):

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, return 0

**Bước 2:** So sánh giá trị node hiện tại với x
- Nếu `root->data > x`: node hiện tại thỏa mãn điều kiện
  - Vì là BST, tất cả các node ở **nhánh phải** chắc chắn cũng > x (không cần kiểm tra từng cái)
  - Cộng: node hiện tại (1) + toàn bộ nhánh phải + tiếp tục kiểm tra nhánh trái
  - Return `1 + countNodesGreaterThanX(root->right, x) + countNodesGreaterThanX(root->left, x)`

**Bước 3:** Xử lý trường hợp node không thỏa mãn
- Nếu `root->data <= x`: node hiện tại không thỏa
  - Vì là BST, toàn bộ **nhánh trái** chắc chắn cũng ≤ x → bỏ qua không cần kiểm tra
  - Chỉ cần tiếp tục tìm ở nhánh phải
  - Return `countNodesGreaterThanX(root->right, x)`

**Ghi chú:** Đây là cách tối ưu nhờ tính chất BST - không cần duyệt toàn bộ cây mà loại bỏ được cả 1 nhánh con không cần kiểm tra

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây
- x: giá trị cần so sánh

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng số node có giá trị > x

### **4. Ví dụ**

**Input:** BST, x = 40
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:** 4 node (50, 70, 60, 80 > 40)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để đếm số node có giá trị nhỏ hơn x (tận dụng tính chất BST):

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, return 0

**Bước 2:** So sánh giá trị node hiện tại với x
- Nếu `root->data < x`: node hiện tại thỏa mãn điều kiện
  - Vì là BST, tất cả các node ở **nhánh trái** chắc chắn cũng < x (không cần kiểm tra từng cái)
  - Cộng: node hiện tại (1) + toàn bộ nhánh trái + tiếp tục kiểm tra nhánh phải
  - Return `1 + countNodesLessThanX(root->left, x) + countNodesLessThanX(root->right, x)`

**Bước 3:** Xử lý trường hợp node không thỏa mãn
- Nếu `root->data >= x`: node hiện tại không thỏa
  - Vì là BST, toàn bộ **nhánh phải** chắc chắn cũng ≥ x → bỏ qua không cần kiểm tra
  - Chỉ cần tiếp tục tìm ở nhánh trái
  - Return `countNodesLessThanX(root->left, x)`

**Ghi chú:** Tương tự thuật toán đếm số lớn hơn x, nhưng đảo ngược hướng tìm kiếm

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây
- x: giá trị cần so sánh

### **3. Dữ liệu ra (Output)**
- Số nguyên = tổng số node có giá trị < x

### **4. Ví dụ**

**Input:** BST, x = 50
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:** 3 node (30, 20, 40 < 50)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để in tất cả các node ở một mức (tầng) cụ thể:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr` hoặc `level <= 0`: cây con rỗng hoặc mức không hợp lệ, return

**Bước 2:** Kiểm tra đã tới đúng mức cần in chưa
- Nếu `level == 1`: node hiện tại chính là node ở mức cần tìm
  - In ra giá trị `root->data`
  - Return (dừng, không đi sâu thêm)

**Bước 3:** Nếu chưa tới mức cần thiết, tiếp tục đi sâu xuống
- Đệ quy nhánh trái với mức giảm đi 1: `printNodesAtLevel(root->left, level - 1)`
- Đệ quy nhánh phải với mức giảm đi 1: `printNodesAtLevel(root->right, level - 1)`
- Việc giảm level mỗi lần đi sâu giúp theo dõi còn bao nhiêu tầng nữa mới tới đích

**Ghi chú:** Phải duyệt cả 2 nhánh (trái và phải) vì có thể có nhiều node ở cùng 1 mức, không thể dừng lại sau khi tìm thấy 1 node

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây
- level: mức cần in (1 = gốc, 2 = con của gốc, ...)

### **3. Dữ liệu ra (Output)**
- In ra tất cả node ở mức level cụ thể

### **4. Ví dụ**

**Input:** Cây
```
        A (level 1)
       / \
      B   C (level 2)
     / \   \
    D   E   F (level 3)
```

**printNodesAtLevel(root, 2):** Output: **B C**

**printNodesAtLevel(root, 3):** Output: **D E F**

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để xóa node có giá trị x trong BST:

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: không tìm thấy x trong cây, return false

**Bước 2:** Tìm node cần xóa dựa trên tính chất BST
- Nếu `x < root->data`: giá trị cần xóa nhỏ hơn, tìm tiếp ở nhánh trái
  - Đệ quy: `return deleteNode(root->left, x)`
- Nếu `x > root->data`: giá trị cần xóa lớn hơn, tìm tiếp ở nhánh phải
  - Đệ quy: `return deleteNode(root->right, x)`

**Bước 3:** Đã tìm thấy node cần xóa (x == root->data), lưu lại địa chỉ
- Gán `temp = root` để giữ địa chỉ node cần xóa, chuẩn bị gọi delete

**Bước 4:** Xử lý trường hợp node không có con trái (TH1 và TH2 gộp lại)
- Nếu `root->left == nullptr`:
  - Kéo con phải lên thế chỗ: `root = root->right` (nếu con phải cũng NULL thì root trở thành NULL, đúng với trường hợp node không có con nào)
  - Xóa node cũ: `delete temp`
  - Return true

**Bước 5:** Xử lý trường hợp node không có con phải
- Nếu `root->right == nullptr`:
  - Kéo con trái lên thế chỗ: `root = root->left`
  - Xóa node cũ: `delete temp`
  - Return true

**Bước 6:** Xử lý trường hợp node có đầy đủ 2 con (phức tạp nhất)
- Tìm "kẻ thế mạng" là node có giá trị nhỏ nhất trong nhánh phải:
  - Khởi tạo `substitute = root->right`
  - Dùng vòng lặp đi tới cực trái: `while (substitute->left != nullptr) substitute = substitute->left`
- Copy giá trị của kẻ thế mạng đè lên node hiện tại: `root->data = substitute->data`
- Gọi đệ quy xóa chính node thế mạng đó ở nhánh phải (vì giờ giá trị đã bị trùng lặp): `return deleteNode(root->right, substitute->data)`

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây (tham chiếu)
- x: giá trị cần xóa

### **3. Dữ liệu ra (Output)**
- true: nếu xóa thành công
- false: nếu không tìm thấy node

### **4. Ví dụ**

**Input:** Xóa node 30 từ cây
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:**
```
        50
       /  \
      40   70
     /    / \
    20   60 80
```

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để xóa toàn bộ cây (giải phóng hết bộ nhớ):

**Bước 1:** Kiểm tra điều kiện dừng
- Nếu `root == nullptr`: cây con rỗng, không có gì để xóa, return

**Bước 2:** Xóa toàn bộ nhánh trái trước
- Đệ quy: `clear(root->left)` để xóa hết các node bên nhánh trái

**Bước 3:** Xóa toàn bộ nhánh phải
- Đệ quy: `clear(root->right)` để xóa hết các node bên nhánh phải

**Bước 4:** Xóa node gốc hiện tại
- Gọi `delete root` để giải phóng bộ nhớ của node hiện tại
- **Quan trọng:** Phải xóa con trước rồi mới xóa cha (dùng Postorder), nếu xóa cha trước sẽ mất con trỏ dẫn tới các node con

**Bước 5:** Cập nhật con trỏ về NULL
- Gán `root = nullptr` để đánh dấu vị trí này đã trống, tránh con trỏ "treo" (dangling pointer)

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây (tham chiếu)

### **3. Dữ liệu ra (Output)**
- Cây bị xóa hoàn toàn, root = nullptr

### **4. Ví dụ**

**Input:** Cây
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```

**Output:** Cây rỗng (root = nullptr)

### **5. Mã C++**

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

### **1. Ý tưởng & Các bước thực hiện**

Để kiểm tra một cây nhị phân có phải là BST hợp lệ không:

**Bước 1:** Khởi tạo con trỏ phụ và gọi hàm helper
- Trong hàm chính `isBSTInOrder`, khởi tạo `prev = nullptr` (lưu node đã duyệt trước đó)
- Gọi hàm đệ quy `isInOrderBST(root, prev)` (truyền prev theo tham chiếu để giữ trạng thái qua các lần gọi)

**Bước 2:** Kiểm tra điều kiện dừng trong hàm helper
- Nếu `root == nullptr`: cây con rỗng, coi như hợp lệ, return true

**Bước 3:** Kiểm tra nhánh trái trước (theo đúng thứ tự Inorder)
- Đệ quy: `if (!isInOrderBST(root->left, prev)) return false`
- Nếu nhánh trái không hợp lệ thì toàn bộ cây cũng không hợp lệ, dừng ngay

**Bước 4:** So sánh node hiện tại với node đã duyệt trước đó (prev)
- Nếu `prev != nullptr && root->data <= prev->data`:
  - Giá trị hiện tại không lớn hơn giá trị trước đó → vi phạm tính chất tăng dần của BST
  - Return false

**Bước 5:** Cập nhật prev thành node hiện tại
- Gán `prev = root` để lần so sánh tiếp theo dùng node này làm mốc

**Bước 6:** Kiểm tra nhánh phải
- Đệ quy: `return isInOrderBST(root->right, prev)`
- Trả về kết quả kiểm tra của nhánh phải (đã bao gồm tất cả các so sánh trước đó)

**Ghi chú:** Thuật toán dựa trên tính chất: nếu duyệt Inorder (Trái-Gốc-Phải) một cây BST hợp lệ, ta luôn nhận được dãy số **tăng dần nghiêm ngặt**. Nếu phát hiện một cặp giá trị không tăng dần, cây đó không phải BST

### **2. Dữ liệu vào (Input)**
- root: con trỏ tới node gốc cây

### **3. Dữ liệu ra (Output)**
- true: nếu cây là BST
- false: nếu không phải BST

### **4. Ví dụ**

**Input 1:** Cây hợp lệ
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```
**Output:** true (Inorder: 20 30 40 50 60 70 80, tăng dần)

**Input 2:** Cây không hợp lệ
```
        50
       /  \
      30   70
     / \
    20 60  ← SAI vị trí
```
**Output:** false (Inorder không tăng dần)

### **5. Mã C++**

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

