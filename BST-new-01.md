# TỔNG HỢP THUẬT TOÁN CÂY NHỊ PHÂN VÀ BST

---

# **PHẦN 1: CÁC PHÉP DUYỆT CÂY (TRAVERSAL)**

## **THUẬT TOÁN 1: DUYỆT CÂY THEO THỨ TỰ GIỮA (LNR - INORDER)**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Kiểm tra, nếu root == NULL thì cây con rỗng, không có gì để duyệt → dừng (điều kiện dừng đệ quy)

**Bước 2:** Gọi đệ quy sang **trái**: LNR(root->left)
→ Hàm tự lặp lại, đi sâu sang trái cho tới khi gặp NULL, sau đó quay lui

**Bước 3:** In root->data (xử lý node hiện tại)

**Bước 4:** Gọi đệ quy sang **phải**: LNR(root->right)
→ Tương tự, đi sâu sang phải rồi quay lui. **Sau bước này, hàm hiện tại kết thúc và quay lui về nút cha cấp cao hơn**.

> Với BST: luồng đệ quy sẽ in ra dãy **tăng dần** vì luôn xử lý trái (nhỏ hơn) → gốc → phải (lớn hơn)

### **2. Dữ liệu vào / ra**
- Input: root (con trỏ gốc cây)
- Output: In các phần tử theo thứ tự tăng dần

### **3. Ví dụ**
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```
Output: **20 30 40 50 60 70 80**

### **4. Mã C++**
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

**Bước 1:** Nếu root == NULL thì cây con rỗng, không có gì để duyệt → dừng (điều kiện dừng đệ quy)

**Bước 2:** In root->data ngay lập tức (xử lý gốc trước)

**Bước 3:** Gọi đệ quy sang **trái**: NLR(root->left) 
→ Hàm tự lặp lại, đi sâu sang trái cho tới khi gặp NULL, sau đó quay lui

**Bước 4:** Gọi đệ quy sang **phải**: NLR(root->right)
→ Tương tự, đi sâu sang phải rồi quay lui. **Sau bước này, hàm hiện tại kết thúc và quay lui về nút cha cấp cao hơn**.

> Gốc luôn được xử lý **trước**, thường dùng để **sao chép cây** hoặc **lưu cây vào file**

### **2. Dữ liệu vào / ra**
- Input: root
- Output: In các phần tử theo thứ tự gốc trước

### **3. Ví dụ**
Cây như trên → Output: **50 30 20 40 70 60 80**

### **4. Mã C++**
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

**Bước 1:** Nếu root == NULL thì cây con rỗng, không có gì để duyệt → dừng (điều kiện dừng đệ quy)

**Bước 2:** Gọi đệ quy sang **trái**: LRN(root->left)
→ Hàm tự lặp lại, đi sâu sang trái cho tới khi gặp NULL, sau đó quay lui

**Bước 3:** Gọi đệ quy sang **phải**: LRN(root->right)
→ Tương tự, đi sâu sang phải rồi quay lui. 

**Bước 4:** In root->data (xử lý gốc **sau cùng**). **Sau bước này, hàm hiện tại kết thúc và quay lui về nút cha cấp cao hơn**.

> Gốc luôn được xử lý **sau** khi 2 nhánh con xong, thường dùng để **xóa cây** (phải xóa con trước, cha sau)

### **2. Dữ liệu vào / ra**
- Input: root
- Output: In các phần tử theo thứ tự lá trước, gốc sau

### **3. Ví dụ**
Cây như trên → Output: **20 40 30 60 80 70 50**

### **4. Mã C++**
```cpp
void LRN(Node* root) {
    if (root == nullptr) return;
    LRN(root->left);
    LRN(root->right);
    cout << root->data << " ";
}
```

### **5. Bảng so sánh 3 duyệt**

| Loại | Thứ tự | Công dụng |
|------|--------|----------|
| **LNR** | Trái → Gốc → Phải | BST in tăng dần |
| **NLR** | Gốc → Trái → Phải | Sao chép cây, lưu file |
| **LRN** | Trái → Phải → Gốc | Xóa cây, tính từ dưới lên |

---

# **PHẦN 2: CÁC PHÉP CHÈN VÀ TÌM KIẾM TRONG BST**

## **THUẬT TOÁN 4: CHÈN PHẦN TỬ VÀO CÂY NHỊ PHÂN TÌM KIẾM**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → tạo node mới tại đây, return true
→ Đây là vị trí đúng cần chèn (đệ quy chạy tới chỗ trống thì dừng)

**Bước 2:** Nếu value < root->data → đệ quy chèn vào **trái**
→ Nhỏ hơn thì đi trái (tính chất BST)

**Bước 3:** Nếu value > root->data → đệ quy chèn vào **phải**
→ Lớn hơn thì đi phải

**Bước 4:** Nếu value == root->data → return false (từ chối trùng lặp)

### **2. Dữ liệu vào / ra**
- Input: root, value
- Output: true (chèn thành công) / false (trùng giá trị)

### **3. Ví dụ**
Chèn 40 vào cây gốc 50 → đi trái (30) → đi phải → chèn vào vị trí trống

### **4. Mã C++**
```cpp
bool insertNode(Node* &root, int value){
    if (root == nullptr){
        root = createNode(value);
        return true;
    }
    if (value < root->data) return insertNode(root->left, value);
    else if (value > root->data) return insertNode(root->right, value);
    return false;
}
```

---

## **THUẬT TOÁN 5: TÌM KIẾM PHẦN TỬ TRONG CÂY NHỊ PHÂN TÌM KIẾM**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return false (đi tới chỗ trống mà chưa thấy → không có)

**Bước 2:** Nếu root->data == value → return true (tìm thấy)

**Bước 3:** Nếu value < root->data → đệ quy tìm ở **trái**

**Bước 4:** Nếu value > root->data → đệ quy tìm ở **phải**

> Nhờ tính chất BST, mỗi bước loại bỏ được 1 nhánh, không cần duyệt toàn bộ cây

### **2. Dữ liệu vào / ra**
- Input: root, value
- Output: true / false

### **3. Ví dụ**
Tìm 40 trong cây: 50 → trái (30) → phải (40) → tìm thấy ✓

### **4. Mã C++**
```cpp
bool searchNode(Node* root, int value){
    if (root == nullptr) return false;
    if (root->data == value) return true;
    else if (value < root->data) return searchNode(root->left, value);
    else return searchNode(root->right, value);
}
```

---

## **THUẬT TOÁN 6: TÌM NODE CÓ GIÁ TRỊ NHỎ NHẤT TRONG CÂY BST**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL hoặc root->left == NULL → return root
→ Không có con trái nghĩa là đây là node nhỏ nhất (đã tới cực trái)

**Bước 2:** Đệ quy tiếp sang **trái**: findMin(root->left)
→ Tiếp tục đi trái cho tới khi không còn trái nữa

> Trong BST, giá trị nhỏ nhất **luôn ở cực trái**

### **2. Dữ liệu vào / ra**
- Input: root
- Output: con trỏ tới node nhỏ nhất (NULL nếu cây rỗng)

### **3. Ví dụ**
Cây: 50 → 30 → 20 → Output: node 20

### **4. Mã C++**
```cpp
Node* findMin(Node* root) {
    if (root == nullptr || root->left == nullptr) return root;
    return findMin(root->left);
}
```

---

## **THUẬT TOÁN 7: TÌM NODE CÓ GIÁ TRỊ LỚN NHẤT TRONG CÂY BST**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL hoặc root->right == NULL → return root
→ Không có con phải nghĩa là đây là node lớn nhất (đã tới cực phải)

**Bước 2:** Đệ quy tiếp sang **phải**: findMax(root->right)

> Trong BST, giá trị lớn nhất **luôn ở cực phải**

### **2. Dữ liệu vào / ra**
- Input: root
- Output: con trỏ tới node lớn nhất (NULL nếu cây rỗng)

### **3. Ví dụ**
Cây: 50 → 70 → 80 → Output: node 80

### **4. Mã C++**
```cpp
Node* findMax(Node* root) {
    if (root == nullptr || root->right == nullptr) return root;
    return findMax(root->right);
}
```

---

# **PHẦN 3: CÁC PHÉP ĐẾM VÀ TÍNH TOÁN TRÊN CÂY**

## **THUẬT TOÁN 8: ĐẾM SỐ NODE TRONG CÂY**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0 (cây rỗng, không có node nào)

**Bước 2:** Đếm nhánh trái: countNodes(root->left) → đệ quy trả về số node bên trái

**Bước 3:** Đếm nhánh phải: countNodes(root->right) → đệ quy trả về số node bên phải

**Bước 4:** Return 1 + trái + phải
→ Số 1 là chính node hiện tại, cộng tổng 2 nhánh

### **2. Dữ liệu vào / ra**
- Input: root
- Output: tổng số node (int)

### **3. Ví dụ**
```
    A
   / \
  B   C
 / \
D   E
```
Output: 5

### **4. Mã C++**
```cpp
int countNodes(Node* root) {
    if (root == nullptr) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}
```

---

## **THUẬT TOÁN 9: TÍNH TỔNG GIÁ TRỊ CÁC NODE TRONG CÂY**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Tính tổng nhánh trái: sumTree(root->left)

**Bước 3:** Tính tổng nhánh phải: sumTree(root->right)

**Bước 4:** Return root->data + trái + phải
→ Cộng giá trị node hiện tại với tổng 2 nhánh

### **2. Dữ liệu vào / ra**
- Input: root
- Output: tổng giá trị (int)

### **3. Ví dụ**
Cây: 10, 5, 15, 2, 3 → Output: 35

### **4. Mã C++**
```cpp
int sumTree(Node* root) { 
    if (root == nullptr) return 0; 
    return root->data + sumTree(root->left) + sumTree(root->right); 
}
```

---

## **THUẬT TOÁN 10: ĐẾM SỐ NODE LÁ TRONG CÂY**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Nếu root->left == NULL **và** root->right == NULL → return 1
→ Node không có con nào = node lá, đếm được 1

**Bước 3:** Nếu không phải lá → đệ quy cả 2 nhánh
→ Return countLeaf(trái) + countLeaf(phải)
→ Cộng số lá tìm được từ 2 nhánh (không cộng thêm 1 vì node hiện tại không phải lá)

### **2. Dữ liệu vào / ra**
- Input: root
- Output: số node lá (int)

### **3. Ví dụ**
Cây A(B(D,E), C) → Lá: D, E, C → Output: 3

### **4. Mã C++**
```cpp
int countLeaf(Node* root) {
    if (root == nullptr) return 0;
    if (root->left == nullptr && root->right == nullptr) return 1;
    return countLeaf(root->left) + countLeaf(root->right);
}
```

---

## **THUẬT TOÁN 11: TÍNH CHIỀU CAO CỦA CÂY**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0 (cây rỗng cao 0)

**Bước 2:** Đệ quy tính chiều cao nhánh trái: leftHeight = height(root->left)

**Bước 3:** Đệ quy tính chiều cao nhánh phải: rightHeight = height(root->right)

**Bước 4:** Return 1 + max(leftHeight, rightHeight)
→ Chọn nhánh cao hơn, cộng thêm 1 (tầng của node hiện tại)

### **2. Dữ liệu vào / ra**
- Input: root
- Output: chiều cao (int)

### **3. Ví dụ**
Cây A(B(D,E), C) → Chiều cao: 3

### **4. Mã C++**
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

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Kiểm tra node hiện tại có đúng 1 con không
→ `hasOneChild = (left == NULL) != (right == NULL)`
→ Phép XOR: 1 bên NULL, 1 bên không NULL → true (1), còn lại → false (0)

**Bước 3:** Đệ quy đếm ở 2 nhánh con

**Bước 4:** Return hasOneChild + countOneChild(trái) + countOneChild(phải)

### **2. Dữ liệu vào / ra**
- Input: root
- Output: số node có đúng 1 con (int)

### **3. Ví dụ**
Cây A(B(D,E), C(F,_)) → C có 1 con → Output: 1

### **4. Mã C++**
```cpp
int countOneChild(Node* root){
    if(root == nullptr) return 0;
    bool hasOneChild = (root->left == nullptr) != (root->right == nullptr);
    return hasOneChild + countOneChild(root->left) + countOneChild(root->right);
}
```

---

## **THUẬT TOÁN 13: ĐẾM SỐ NODE CÓ ĐỦ 2 CON**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Kiểm tra node hiện tại có đủ 2 con không
→ `hasTwoChildren = (left != NULL && right != NULL)`
→ Cả 2 bên đều không NULL → true (1), còn lại → false (0)

**Bước 3:** Đệ quy đếm ở 2 nhánh con

**Bước 4:** Return hasTwoChildren + countTwoChildren(trái) + countTwoChildren(phải)

### **2. Dữ liệu vào / ra**
- Input: root
- Output: số node có 2 con (int)

### **3. Ví dụ**
Cây A(B(D,E), C) → A và B đều có 2 con → Output: 2

### **4. Mã C++**
```cpp
int countTwoChildren(Node* root){
    if(root == nullptr) return 0;
    bool hasTwoChildren = (root->left != nullptr && root->right != nullptr);
    return hasTwoChildren + countTwoChildren(root->left) + countTwoChildren(root->right);
}
```

---

# **PHẦN 4: CÁC PHÉP ĐẾM CÓ ĐIỀU KIỆN TRONG BST**

## **THUẬT TOÁN 14: ĐẾM SỐ NODE CÓ GIÁ TRỊ LỚN HƠN X TRONG BST**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Nếu root->data > x:
→ Node này thỏa mãn (+1)
→ Toàn bộ nhánh **phải** chắc chắn cũng > x → cộng hết (không cần kiểm tra thêm)
→ Nhánh **trái** chưa chắc, tiếp tục đệ quy kiểm tra
→ Return 1 + countGreater(phải, x) + countGreater(trái, x)

**Bước 3:** Nếu root->data ≤ x:
→ Node này không thỏa
→ Toàn bộ nhánh **trái** chắc chắn cũng ≤ x → bỏ qua
→ Chỉ tiếp tục kiểm tra nhánh **phải**
→ Return countGreater(phải, x)

### **2. Dữ liệu vào / ra**
- Input: root, x
- Output: số node có giá trị > x (int)

### **3. Ví dụ**
Cây 50(30(20,40), 70(60,80)), x=40 → Output: 4 (50,70,60,80)

### **4. Mã C++**
```cpp
int countNodesGreaterThanX(Node* root, int x) {
    if (root == nullptr) return 0;
    if (root->data > x)
        return 1 + countNodesGreaterThanX(root->right, x) + countNodesGreaterThanX(root->left, x);
    else
        return countNodesGreaterThanX(root->right, x);
}
```

---

## **THUẬT TOÁN 15: ĐẾM SỐ NODE CÓ GIÁ TRỊ NHỎ HƠN X TRONG BST**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Nếu root->data < x:
→ Node này thỏa mãn (+1)
→ Toàn bộ nhánh **trái** chắc chắn cũng < x → cộng hết
→ Nhánh **phải** chưa chắc, tiếp tục đệ quy kiểm tra
→ Return 1 + countLess(trái, x) + countLess(phải, x)

**Bước 3:** Nếu root->data ≥ x:
→ Node này không thỏa
→ Toàn bộ nhánh **phải** chắc chắn cũng ≥ x → bỏ qua
→ Chỉ tiếp tục kiểm tra nhánh **trái**
→ Return countLess(trái, x)

### **2. Dữ liệu vào / ra**
- Input: root, x
- Output: số node có giá trị < x (int)

### **3. Ví dụ**
Cây như trên, x=50 → Output: 3 (30,20,40)

### **4. Mã C++**
```cpp
int countNodesLessThanX(Node* root, int x) {
    if (root == nullptr) return 0;
    if (root->data < x)
        return 1 + countNodesLessThanX(root->left, x) + countNodesLessThanX(root->right, x);
    else
        return countNodesLessThanX(root->left, x);
}
```

---

# **PHẦN 5: CÁC PHÉP XÓA VÀ CHỈNH SỬA CÂY**

## **THUẬT TOÁN 16: IN CÁC NODE Ở MỘT MỨC (LEVEL) CỤ THỂ**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL hoặc level <= 0 → dừng

**Bước 2:** Nếu level == 1 → in root->data, dừng
→ Đã tới đúng tầng cần in

**Bước 3:** Đệ quy xuống 2 nhánh với level giảm đi 1:
→ printNodesAtLevel(root->left, level - 1)
→ printNodesAtLevel(root->right, level - 1)
→ Mỗi lần đi sâu 1 tầng thì giảm level đi 1, khi level == 1 thì in

### **2. Dữ liệu vào / ra**
- Input: root, level (1 = gốc, 2 = con của gốc, ...)
- Output: In tất cả node ở mức level

### **3. Ví dụ**
Cây A(B(D,E), C), level=2 → Output: **B C**

### **4. Mã C++**
```cpp
void printNodesAtLevel(Node* root, int level) {
    if (root == nullptr || level <= 0) return;
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

**Bước 1:** Nếu root == NULL → return false (không tìm thấy x)

**Bước 2:** Tìm node cần xóa (dùng tính chất BST):
→ Nếu x < root->data → đệ quy tìm ở **trái**
→ Nếu x > root->data → đệ quy tìm ở **phải**

**Bước 3:** Đã tìm thấy node cần xóa (x == root->data), có 3 trường hợp:

**TH1: Không có con trái (left == NULL)**
→ Kéo con phải lên thế chỗ: `root = root->right`
→ Xóa node cũ. (Nếu cả 2 đều NULL thì root = NULL, coi như xóa node lá)

**TH2: Không có con phải (right == NULL)**
→ Kéo con trái lên thế chỗ: `root = root->left`
→ Xóa node cũ

**TH3: Có đủ 2 con**
→ Tìm node **nhỏ nhất của nhánh phải** (substitute = cực trái của root->right)
→ Copy giá trị substitute lên node hiện tại: `root->data = substitute->data`
→ Gọi đệ quy xóa substitute ở nhánh phải: `deleteNode(root->right, substitute->data)`

### **2. Dữ liệu vào / ra**
- Input: root, x
- Output: true (xóa thành công) / false (không tìm thấy)

### **3. Ví dụ**
Xóa 30 (có 2 con 20 và 40):
→ Tìm substitute = 40 (min của nhánh phải 30)
→ Copy 40 lên vị trí 30
→ Xóa 40 ở nhánh phải

### **4. Mã C++**
```cpp
bool deleteNode(Node* &root, int x) {
    if (root == nullptr) return false;
    if (x < root->data) return deleteNode(root->left, x);
    else if (x > root->data) return deleteNode(root->right, x);
    else {
        Node* temp = root;
        if (root->left == nullptr) { root = root->right; delete temp; return true; }
        else if (root->right == nullptr) { root = root->left; delete temp; return true; }
        else {
            Node* substitute = root->right;
            while (substitute->left != nullptr) substitute = substitute->left;
            root->data = substitute->data;
            return deleteNode(root->right, substitute->data);
        }
    }
}
```

---

## **THUẬT TOÁN 18: XÓA TOÀN BỘ CÂY BST**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu root == NULL → dừng

**Bước 2:** Đệ quy xóa nhánh **trái**: clear(root->left)

**Bước 3:** Đệ quy xóa nhánh **phải**: clear(root->right)

**Bước 4:** Xóa node hiện tại: delete root → root = nullptr
→ Phải xóa con trước cha (Postorder), nếu xóa cha trước sẽ mất đường dẫn đến con

### **2. Dữ liệu vào / ra**
- Input: root (tham chiếu)
- Output: Cây bị xóa hoàn toàn, root = nullptr

### **3. Ví dụ**
Thứ tự xóa cây 50(30(20,40),70): 20→40→30→70→50

### **4. Mã C++**
```cpp
void clear(Node* &root) {
    if (root == nullptr) return;
    clear(root->left);
    clear(root->right);
    delete root;
    root = nullptr;
}
```

---

## **THUẬT TOÁN 19: KIỂM TRA CÂY CÓ PHẢI LÀ BST KHÔNG (DÙNG INORDER)**

### **1. Ý tưởng & Các bước thực hiện**

**Ý tưởng cốt lõi:** Duyệt Inorder BST hợp lệ luôn cho dãy **tăng dần nghiêm ngặt**. Nếu phát hiện có 1 cặp không tăng → không phải BST.

**Hàm chính isBSTInOrder:**
→ Khởi tạo `prev = nullptr` rồi gọi hàm helper

**Hàm helper isInOrderBST(root, prev):**

**Bước 1:** Nếu root == NULL → return true (cây rỗng là hợp lệ)

**Bước 2:** Đệ quy kiểm tra nhánh **trái** trước
→ Nếu trái không hợp lệ → return false ngay

**Bước 3:** So sánh node hiện tại với prev (node đã duyệt liền trước)
→ Nếu root->data ≤ prev->data → vi phạm tăng dần → return false

**Bước 4:** Cập nhật prev = root (để lần sau so sánh với node tiếp theo)

**Bước 5:** Đệ quy kiểm tra nhánh **phải**

### **2. Dữ liệu vào / ra**
- Input: root
- Output: true (là BST) / false (không phải BST)

### **3. Ví dụ**
Cây hợp lệ: Inorder 20→30→40→50→60→70→80 (tăng dần) → **true**

Cây không hợp lệ (60 ở sai vị trí): Inorder 20→30→60→50→... → **false**

### **4. Mã C++**
```cpp
bool isInOrderBST(Node* root, Node* &prev) {
    if (root == nullptr) return true;
    if (!isInOrderBST(root->left, prev)) return false;
    if (prev != nullptr && root->data <= prev->data) return false;
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
| 12 | countOneChild | Đếm | Node 1 con (XOR) | ⭐⭐ |
| 13 | countTwoChildren | Đếm | Node 2 con (AND) | ⭐⭐ |
| 14 | countGreaterThanX | Đếm | Tận dụng BST | ⭐⭐ |
| 15 | countLessThanX | Đếm | Tận dụng BST | ⭐⭐ |
| 16 | printNodesAtLevel | In | Giảm level mỗi tầng | ⭐⭐ |
| 17 | deleteNode | Xóa | 3 trường hợp | ⭐⭐⭐ |
| 18 | clear | Xóa | Postorder (con trước cha) | ⭐ |
| 19 | isBSTInOrder | Kiểm tra | Inorder tăng dần | ⭐⭐ |

---
