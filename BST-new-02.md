# CÁC THUẬT TOÁN CÂY NHỊ PHÂN BỔ SUNG

---

# **PHẦN 1: RẤT HAY GẶP TRONG ĐỀ THI ⭐⭐⭐**

## **THUẬT TOÁN 1: DUYỆT THEO TỪNG TẦNG (LEVEL ORDER / BFS)**

### **1. Ý tưởng & Các bước thực hiện**

Dùng **Queue (hàng đợi)** để duyệt cây theo từng tầng từ trên xuống:

**Bước 1:** Nếu cây rỗng → dừng

**Bước 2:** Đẩy root vào queue

**Bước 3:** Lặp khi queue không rỗng:
→ Lấy node đầu queue ra (dequeue), in giá trị
→ Nếu có con trái → đẩy vào queue
→ Nếu có con phải → đẩy vào queue

> Queue đảm bảo thứ tự: node ở tầng trên luôn được xử lý trước tầng dưới

### **2. Dữ liệu vào / ra**
- Input: root
- Output: In các phần tử theo từng tầng từ trên xuống

### **3. Ví dụ**
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```
Output: **50 30 70 20 40 60 80**

### **4. Mã C++**
```cpp
void levelOrder(Node* root) {
    if (root == nullptr) return;

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        Node* current = q.front();
        q.pop();

        cout << current->data << " ";

        if (current->left != nullptr)  q.push(current->left);
        if (current->right != nullptr) q.push(current->right);
    }
}
```

---

## **THUẬT TOÁN 2: ĐẾM SỐ NODE Ở MỨC K**

### **1. Ý tưởng & Các bước thực hiện**

Tương tự `printNodesAtLevel` nhưng trả về **số đếm** thay vì in:

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Nếu level == 1 → return 1 (đã tới đúng tầng, đếm node này)

**Bước 3:** Đệ quy xuống 2 nhánh với level giảm 1:
→ Return countAtLevel(trái, level-1) + countAtLevel(phải, level-1)

### **2. Dữ liệu vào / ra**
- Input: root, level (1 = gốc)
- Output: số node ở mức level (int)

### **3. Ví dụ**
Cây như trên, level=2 → Output: **2** (node 30 và 70)

### **4. Mã C++**
```cpp
int countNodesAtLevel(Node* root, int level) {
    if (root == nullptr) return 0;
    if (level == 1) return 1;
    return countNodesAtLevel(root->left, level - 1) +
           countNodesAtLevel(root->right, level - 1);
}
```

---

## **THUẬT TOÁN 3: TÌM PHẦN TỬ LỚN THỨ K TRONG BST**

### **1. Ý tưởng & Các bước thực hiện**

Dùng đặc tính: **duyệt Inorder ngược (Phải → Gốc → Trái)** sẽ cho dãy **giảm dần**.
Phần tử thứ k gặp đầu tiên chính là phần tử lớn thứ k.

**Bước 1:** Nếu root == NULL → dừng

**Bước 2:** Đệ quy vào nhánh **phải** trước (giá trị lớn nhất)

**Bước 3:** Tăng biến đếm `count++`
→ Nếu count == k → đây là phần tử lớn thứ k, lưu kết quả, dừng

**Bước 4:** Đệ quy vào nhánh **trái**

### **2. Dữ liệu vào / ra**
- Input: root, k, count (đếm số node đã qua), result (kết quả)
- Output: giá trị phần tử lớn thứ k

### **3. Ví dụ**
Cây: 20 30 40 50 60 70 80, k=3 → Output: **60** (lớn thứ 3)

### **4. Mã C++**
```cpp
void kthLargest(Node* root, int k, int &count, int &result) {
    if (root == nullptr) return;

    // Duyệt phải trước (giảm dần)
    kthLargest(root->right, k, count, result);

    count++;
    if (count == k) {
        result = root->data;
        return;
    }

    kthLargest(root->left, k, count, result);
}

// Hàm gọi từ ngoài
int findKthLargest(Node* root, int k) {
    int count = 0, result = -1;
    kthLargest(root, k, count, result);
    return result;
}
```

---

## **THUẬT TOÁN 4: IN TẤT CẢ NODE TRONG KHOẢNG [a, b]**

### **1. Ý tưởng & Các bước thực hiện**

Tận dụng tính chất BST để tránh duyệt nhánh không cần thiết:

**Bước 1:** Nếu root == NULL → dừng

**Bước 2:** Nếu root->data > a → đệ quy tìm ở nhánh **trái**
→ Nhánh trái có thể có giá trị thuộc [a, b]

**Bước 3:** Nếu a ≤ root->data ≤ b → in root->data (thỏa mãn)

**Bước 4:** Nếu root->data < b → đệ quy tìm ở nhánh **phải**
→ Nhánh phải có thể có giá trị thuộc [a, b]

> Không đi vào nhánh trái nếu root->data ≤ a (toàn bộ trái nhỏ hơn a)
> Không đi vào nhánh phải nếu root->data ≥ b (toàn bộ phải lớn hơn b)

### **2. Dữ liệu vào / ra**
- Input: root, a, b
- Output: In tất cả node có giá trị trong [a, b]

### **3. Ví dụ**
Cây: 20 30 40 50 60 70 80, a=30, b=65 → Output: **30 40 50 60**

### **4. Mã C++**
```cpp
void printInRange(Node* root, int a, int b) {
    if (root == nullptr) return;

    // Chỉ tìm trái nếu có thể có giá trị >= a
    if (root->data > a)
        printInRange(root->left, a, b);

    // In nếu nằm trong khoảng [a, b]
    if (root->data >= a && root->data <= b)
        cout << root->data << " ";

    // Chỉ tìm phải nếu có thể có giá trị <= b
    if (root->data < b)
        printInRange(root->right, a, b);
}
```

---

# **PHẦN 2: HAY GẶP TRONG ĐỀ THI ⭐⭐**

## **THUẬT TOÁN 5: ĐẾM SỐ NODE TRONG KHOẢNG [a, b]**

### **1. Ý tưởng & Các bước thực hiện**

Tương tự `printInRange` nhưng **đếm** thay vì in:

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Khởi tạo count = 0

**Bước 3:** Nếu root->data > a → đếm thêm từ nhánh trái

**Bước 4:** Nếu a ≤ root->data ≤ b → count++ (node này thỏa mãn)

**Bước 5:** Nếu root->data < b → đếm thêm từ nhánh phải

**Bước 6:** Return count

### **2. Dữ liệu vào / ra**
- Input: root, a, b
- Output: số node có giá trị trong [a, b] (int)

### **3. Ví dụ**
Cây: 20 30 40 50 60 70 80, a=30, b=65 → Output: **4**

### **4. Mã C++**
```cpp
int countInRange(Node* root, int a, int b) {
    if (root == nullptr) return 0;

    int count = 0;

    if (root->data > a)
        count += countInRange(root->left, a, b);

    if (root->data >= a && root->data <= b)
        count++;

    if (root->data < b)
        count += countInRange(root->right, a, b);

    return count;
}
```

---

## **THUẬT TOÁN 6: KIỂM TRA CÂY CÓ CÂN BẰNG KHÔNG (BALANCED)**

### **1. Ý tưởng & Các bước thực hiện**

Cây cân bằng = mọi node đều có |chiều cao trái - chiều cao phải| ≤ 1

**Bước 1:** Nếu root == NULL → return true (cây rỗng là cân bằng)

**Bước 2:** Tính chiều cao nhánh trái: leftH = height(root->left)

**Bước 3:** Tính chiều cao nhánh phải: rightH = height(root->right)

**Bước 4:** Kiểm tra 3 điều kiện đều phải đúng:
→ |leftH - rightH| ≤ 1 (node hiện tại cân bằng)
→ isBalanced(root->left) == true (nhánh trái cân bằng)
→ isBalanced(root->right) == true (nhánh phải cân bằng)

**Bước 5:** Return kết quả AND của 3 điều kiện trên

### **2. Dữ liệu vào / ra**
- Input: root
- Output: true (cân bằng) / false (không cân bằng)

### **3. Ví dụ**
```
Cân bằng:          Không cân bằng:
    50                  50
   /  \                /
  30   70             30
 / \                 /
20 40               20
```

### **4. Mã C++**
```cpp
int height(Node* root) {
    if (root == nullptr) return 0;
    return 1 + max(height(root->left), height(root->right));
}

bool isBalanced(Node* root) {
    if (root == nullptr) return true;

    int leftH  = height(root->left);
    int rightH = height(root->right);

    if (abs(leftH - rightH) > 1) return false;

    return isBalanced(root->left) && isBalanced(root->right);
}
```

---

## **THUẬT TOÁN 7: TÌM NODE CHA CỦA NODE X**

### **1. Ý tưởng & Các bước thực hiện**

Tìm node có con trái hoặc con phải chứa giá trị x:

**Bước 1:** Nếu root == NULL → return NULL (không tìm thấy)

**Bước 2:** Nếu con trái hoặc con phải của root chứa x → return root (root chính là cha)

**Bước 3:** Nếu x < root->data → đệ quy tìm ở nhánh **trái**

**Bước 4:** Nếu x > root->data → đệ quy tìm ở nhánh **phải**

**Bước 5:** Nếu x == root->data (chính là root/gốc) → return NULL (không có cha)

### **2. Dữ liệu vào / ra**
- Input: root, x
- Output: con trỏ tới node cha (NULL nếu x là gốc hoặc không có trong cây)

### **3. Ví dụ**
Cây: 50(30(20,40), 70), tìm cha của 20 → Output: **node 30**

### **4. Mã C++**
```cpp
Node* findParent(Node* root, int x) {
    if (root == nullptr) return nullptr;

    // Kiểm tra nếu con trái hoặc con phải là x
    if ((root->left  && root->left->data  == x) ||
        (root->right && root->right->data == x))
        return root;

    // Tận dụng BST để tìm đúng nhánh
    if (x < root->data)
        return findParent(root->left, x);
    else if (x > root->data)
        return findParent(root->right, x);

    // x chính là root (gốc cây), không có cha
    return nullptr;
}
```

---

## **THUẬT TOÁN 8: SAO CHÉP CÂY**

### **1. Ý tưởng & Các bước thực hiện**

Dùng duyệt **Preorder (NLR)**: sao chép gốc trước, rồi mới sao chép 2 nhánh con:

**Bước 1:** Nếu root == NULL → return NULL (không có gì để copy)

**Bước 2:** Tạo node mới với cùng giá trị: newNode = createNode(root->data)

**Bước 3:** Đệ quy sao chép nhánh trái: newNode->left = copyTree(root->left)

**Bước 4:** Đệ quy sao chép nhánh phải: newNode->right = copyTree(root->right)

**Bước 5:** Return newNode

### **2. Dữ liệu vào / ra**
- Input: root (cây gốc cần sao chép)
- Output: con trỏ tới gốc của cây mới (bản sao hoàn toàn độc lập)

### **3. Ví dụ**
Cây gốc: 50(30, 70) → Cây copy: 50(30, 70) (độc lập hoàn toàn)

### **4. Mã C++**
```cpp
Node* copyTree(Node* root) {
    if (root == nullptr) return nullptr;

    Node* newNode = createNode(root->data);
    newNode->left  = copyTree(root->left);
    newNode->right = copyTree(root->right);

    return newNode;
}
```

---

# **PHẦN 3: CƠ BẢN NHƯNG NÊN BIẾT ⭐**

## **THUẬT TOÁN 9: ĐẾM SỐ NODE KHÔNG PHẢI LÁ**

### **1. Ý tưởng & Các bước thực hiện**

Node không phải lá = có ít nhất 1 con (trái hoặc phải khác NULL):

**Bước 1:** Nếu root == NULL → return 0

**Bước 2:** Nếu cả 2 con đều NULL (là lá) → return 0 (không đếm)

**Bước 3:** Nếu có ít nhất 1 con (không phải lá) → đếm được 1
→ Return 1 + countNonLeaf(trái) + countNonLeaf(phải)

### **2. Dữ liệu vào / ra**
- Input: root
- Output: số node không phải lá (int)

### **3. Ví dụ**
Cây A(B(D,E), C) → Lá: D, E, C. Không phải lá: A, B → Output: **2**

### **4. Mã C++**
```cpp
int countNonLeaf(Node* root) {
    if (root == nullptr) return 0;

    // Là lá → không đếm
    if (root->left == nullptr && root->right == nullptr) return 0;

    // Không phải lá → đếm 1 + 2 nhánh con
    return 1 + countNonLeaf(root->left) + countNonLeaf(root->right);
}
```

---

## **THUẬT TOÁN 10: TÌM NODE KẾ VỊ INORDER (INORDER SUCCESSOR)**

### **1. Ý tưởng & Các bước thực hiện**

Node kế vị Inorder của X = **node nhỏ nhất lớn hơn X** (node tiếp theo trong duyệt LNR):

**Trường hợp 1: X có con phải**
→ Node kế vị = node nhỏ nhất của nhánh phải (cực trái của nhánh phải)

**Trường hợp 2: X không có con phải**
→ Duyệt từ gốc, lưu lại node tổ tiên cuối cùng mà X nằm bên trái
→ Node đó chính là kế vị

**Bước 1:** Tìm node X trong cây, lưu lại ancestor (tổ tiên)

**Bước 2:** Nếu X có con phải → return findMin(X->right)

**Bước 3:** Nếu X không có con phải → return ancestor cuối cùng mà đi trái

### **2. Dữ liệu vào / ra**
- Input: root, x
- Output: con trỏ tới node kế vị (NULL nếu X là lớn nhất)

### **3. Ví dụ**
Cây: 20 30 40 50 60 70 80, kế vị của 40 → **50**; kế vị của 50 → **60**

### **4. Mã C++**
```cpp
Node* inorderSuccessor(Node* root, int x) {
    Node* successor = nullptr;
    Node* current = root;

    while (current != nullptr) {
        if (x < current->data) {
            successor = current;       // Có thể là kế vị
            current = current->left;
        } else if (x > current->data) {
            current = current->right;
        } else {
            // Tìm thấy X
            if (current->right != nullptr) {
                // TH1: X có con phải → min của nhánh phải
                Node* temp = current->right;
                while (temp->left != nullptr) temp = temp->left;
                return temp;
            }
            break;
        }
    }

    // TH2: Không có con phải → trả về ancestor đã lưu
    return successor;
}
```

---

# **BẢNG TỔNG HỢP 10 THUẬT TOÁN BỔ SUNG**

| # | Tên thuật toán | Mức độ | Ý tưởng chính |
|---|---|---|---|
| 1 | levelOrder | ⭐⭐⭐ | Dùng Queue duyệt từng tầng |
| 2 | countNodesAtLevel | ⭐⭐⭐ | Đệ quy giảm level, đếm khi level==1 |
| 3 | findKthLargest | ⭐⭐⭐ | Inorder ngược (phải→gốc→trái) |
| 4 | printInRange | ⭐⭐⭐ | Tận dụng BST bỏ qua nhánh ngoài khoảng |
| 5 | countInRange | ⭐⭐ | Tương tự printInRange nhưng đếm |
| 6 | isBalanced | ⭐⭐ | Kiểm tra \|chiều cao trái - phải\| ≤ 1 |
| 7 | findParent | ⭐⭐ | Kiểm tra con trái/phải có chứa x |
| 8 | copyTree | ⭐⭐ | Preorder: copy gốc trước, con sau |
| 9 | countNonLeaf | ⭐ | Ngược lại countLeaf |
| 10 | inorderSuccessor | ⭐⭐ | Node nhỏ nhất lớn hơn X |

---

EOF
