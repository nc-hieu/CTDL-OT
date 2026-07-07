# CÁC THUẬT TOÁN DANH SÁCH LIÊN KẾT ĐƠN BỔ SUNG

---

# **PHẦN 1: RẤT HAY GẶP TRONG ĐỀ THI ⭐⭐⭐**

## **THUẬT TOÁN 1: TÌM KIẾM PHẦN TỬ CÓ GIÁ TRỊ X**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Khởi tạo `current = head`, `pos = 1`

**Bước 2:** Duyệt từng node trong khi `current != nullptr`:
→ Nếu `current->data == x` → tìm thấy, return pos (vị trí)
→ Nếu không → `current = current->next`, `pos++`

**Bước 3:** Duyệt hết mà không thấy → return -1 (không tìm thấy)

### **2. Dữ liệu vào / ra**
- Input: head, x
- Output: vị trí đầu tiên tìm thấy x, -1 nếu không có

### **3. Ví dụ**
Danh sách: 1 → 3 → 5 → 3 → 7, x = 3 → Output: **2**

### **4. Mã C++**
```cpp
int search(Node* head, int x) {
    Node* current = head;
    int pos = 1;

    while (current != nullptr) {
        if (current->data == x) return pos;
        current = current->next;
        pos++;
    }

    return -1; // Không tìm thấy
}
```

---

## **THUẬT TOÁN 2: ĐẾM SỐ PHẦN TỬ TRONG DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Khởi tạo `count = 0`, `current = head`

**Bước 2:** Duyệt từng node: `count++`, `current = current->next`

**Bước 3:** Duyệt xong → return count

### **2. Dữ liệu vào / ra**
- Input: head
- Output: số lượng phần tử (int)

### **3. Ví dụ**
Danh sách: 1 → 2 → 3 → 4 → 5 → Output: **5**

### **4. Mã C++**
```cpp
int countNodes(Node* head) {
    int count = 0;
    Node* current = head;

    while (current != nullptr) {
        count++;
        current = current->next;
    }

    return count;
}
```

---

## **THUẬT TOÁN 3: ĐẾM SỐ LẦN XUẤT HIỆN CỦA GIÁ TRỊ X**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Khởi tạo `count = 0`, `current = head`

**Bước 2:** Duyệt từng node:
→ Nếu `current->data == x` → `count++`
→ `current = current->next`

**Bước 3:** Return count

### **2. Dữ liệu vào / ra**
- Input: head, x
- Output: số lần xuất hiện (int)

### **3. Ví dụ**
Danh sách: 1 → 3 → 3 → 5 → 3, x = 3 → Output: **3**

### **4. Mã C++**
```cpp
int countOccurrences(Node* head, int x) {
    int count = 0;
    Node* current = head;

    while (current != nullptr) {
        if (current->data == x) count++;
        current = current->next;
    }

    return count;
}
```

---

## **THUẬT TOÁN 4: TÍNH TỔNG CÁC PHẦN TỬ TRONG DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Khởi tạo `sum = 0`, `current = head`

**Bước 2:** Duyệt từng node: `sum += current->data`, `current = current->next`

**Bước 3:** Return sum

### **2. Dữ liệu vào / ra**
- Input: head
- Output: tổng giá trị (int)

### **3. Ví dụ**
Danh sách: 1 → 2 → 3 → 4 → 5 → Output: **15**

### **4. Mã C++**
```cpp
int sumList(Node* head) {
    int sum = 0;
    Node* current = head;

    while (current != nullptr) {
        sum += current->data;
        current = current->next;
    }

    return sum;
}
```

---

## **THUẬT TOÁN 5: SẮP XẾP DANH SÁCH (BUBBLE SORT)**

### **1. Ý tưởng & Các bước thực hiện**

Dùng thuật toán Bubble Sort: **đổi chỗ giá trị** (không đổi chỗ node) khi phần tử trước lớn hơn phần tử sau:

**Bước 1:** Kiểm tra danh sách rỗng hoặc 1 phần tử → return

**Bước 2:** Dùng 2 vòng lặp lồng nhau:
→ Vòng ngoài (`i`): lặp n-1 lần
→ Vòng trong (`current`): duyệt từ đầu đến gần cuối
→ Nếu `current->data > current->next->data` → đổi chỗ 2 giá trị (`swap`)

**Bước 3:** Sau mỗi lượt vòng ngoài, phần tử lớn nhất "nổi" lên cuối

### **2. Dữ liệu vào / ra**
- Input: head
- Output: Danh sách được sắp xếp tăng dần

### **3. Ví dụ**
Danh sách: 3 → 1 → 4 → 1 → 5 → Output: **1 → 1 → 3 → 4 → 5**

### **4. Mã C++**
```cpp
void bubbleSort(Node* head) {
    if (head == nullptr || head->next == nullptr) return;

    bool swapped;
    do {
        swapped = false;
        Node* current = head;

        while (current->next != nullptr) {
            if (current->data > current->next->data) {
                // Đổi chỗ giá trị (không đổi chỗ node)
                swap(current->data, current->next->data);
                swapped = true;
            }
            current = current->next;
        }
    } while (swapped); // Lặp lại nếu còn đổi chỗ
}
```

---

## **THUẬT TOÁN 6: TÌM PHẦN TỬ Ở GIỮA DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

Dùng **kỹ thuật Rùa-Thỏ** (slow/fast pointer):

**Bước 1:** Nếu danh sách rỗng → return NULL

**Bước 2:** Khởi tạo `slow = head`, `fast = head`

**Bước 3:** Duyệt trong khi `fast != NULL && fast->next != NULL`:
→ `slow = slow->next` (nhảy 1 bước)
→ `fast = fast->next->next` (nhảy 2 bước)

**Bước 4:** Khi fast chạm cuối → slow đang ở **chính giữa**, return slow

> Danh sách chẵn: slow trả về node **giữa thứ 2**
> Danh sách lẻ: slow trả về node **chính giữa**

### **2. Dữ liệu vào / ra**
- Input: head
- Output: con trỏ tới node ở giữa

### **3. Ví dụ**
Danh sách: 1 → 2 → **3** → 4 → 5 → Output: **node 3**

Danh sách: 1 → 2 → **3** → 4 → Output: **node 3** (giữa thứ 2)

### **4. Mã C++**
```cpp
Node* findMiddle(Node* head) {
    if (head == nullptr) return nullptr;

    Node* slow = head;
    Node* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow; // slow đang ở chính giữa
}
```

---

# **PHẦN 2: HAY GẶP TRONG ĐỀ THI ⭐⭐**

## **THUẬT TOÁN 7: LẤY PHẦN TỬ TẠI VỊ TRÍ K**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Nếu k < 1 → vị trí không hợp lệ, return -1

**Bước 2:** Khởi tạo `current = head`, `count = 1`

**Bước 3:** Duyệt tới vị trí k:
→ Nếu count == k → return `current->data`
→ `current = current->next`, `count++`

**Bước 4:** Nếu `current == nullptr` trước khi đến k → vị trí vượt quá độ dài, return -1

### **2. Dữ liệu vào / ra**
- Input: head, k
- Output: giá trị tại vị trí k, -1 nếu không hợp lệ

### **3. Ví dụ**
Danh sách: 10 → 20 → 30 → 40, k=3 → Output: **30**

### **4. Mã C++**
```cpp
int getAt(Node* head, int k) {
    if (k < 1) return -1;

    Node* current = head;
    int count = 1;

    while (current != nullptr) {
        if (count == k) return current->data;
        current = current->next;
        count++;
    }

    return -1; // Vị trí vượt quá độ dài
}
```

---

## **THUẬT TOÁN 8: TÌM PHẦN TỬ THỨ K TỪ CUỐI**

### **1. Ý tưởng & Các bước thực hiện**

Dùng **2 con trỏ** cách nhau k bước:

**Bước 1:** Khởi tạo `fast = head`, `slow = head`

**Bước 2:** Dịch `fast` đi k bước trước:
→ Nếu `fast` chạm NULL trước khi đủ k bước → k vượt quá độ dài, return -1

**Bước 3:** Dịch cả `fast` và `slow` cùng lúc cho đến khi `fast == nullptr`:
→ `slow = slow->next`, `fast = fast->next`

**Bước 4:** Lúc này slow đang ở **phần tử thứ k từ cuối** → return `slow->data`

### **2. Dữ liệu vào / ra**
- Input: head, k
- Output: giá trị phần tử thứ k từ cuối, -1 nếu k không hợp lệ

### **3. Ví dụ**
Danh sách: 1 → 2 → 3 → 4 → 5, k=2 → Output: **4** (phần tử thứ 2 từ cuối)

### **4. Mã C++**
```cpp
int getKthFromEnd(Node* head, int k) {
    if (head == nullptr || k < 1) return -1;

    Node* fast = head;
    Node* slow = head;

    // Dịch fast đi k bước trước
    for (int i = 0; i < k; i++) {
        if (fast == nullptr) return -1; // k vượt quá độ dài
        fast = fast->next;
    }

    // Dịch cả 2 cùng lúc cho tới khi fast == nullptr
    while (fast != nullptr) {
        slow = slow->next;
        fast = fast->next;
    }

    return slow->data;
}
```

---

## **THUẬT TOÁN 9: HỢP NHẤT 2 DANH SÁCH ĐÃ SẮP XẾP**

### **1. Ý tưởng & Các bước thực hiện**

Merge 2 danh sách đã tăng dần thành 1 danh sách tăng dần:

**Bước 1:** Nếu 1 danh sách rỗng → return danh sách còn lại

**Bước 2:** So sánh node đầu của 2 danh sách, chọn node nhỏ hơn làm head mới

**Bước 3:** Đệ quy ghép phần còn lại:
→ Nếu head1->data ≤ head2->data:
  - head1->next = merge(head1->next, head2)
  - return head1
→ Ngược lại:
  - head2->next = merge(head1, head2->next)
  - return head2

### **2. Dữ liệu vào / ra**
- Input: head1 (DS đã tăng), head2 (DS đã tăng)
- Output: con trỏ đầu danh sách đã merge (tăng dần)

### **3. Ví dụ**
DS1: 1 → 3 → 5, DS2: 2 → 4 → 6 → Output: **1 → 2 → 3 → 4 → 5 → 6**

### **4. Mã C++**
```cpp
Node* mergeSorted(Node* head1, Node* head2) {
    if (head1 == nullptr) return head2;
    if (head2 == nullptr) return head1;

    if (head1->data <= head2->data) {
        head1->next = mergeSorted(head1->next, head2);
        return head1;
    } else {
        head2->next = mergeSorted(head1, head2->next);
        return head2;
    }
}
```

---

## **THUẬT TOÁN 10: KIỂM TRA VÒNG LẶP (CYCLE DETECTION)**

### **1. Ý tưởng & Các bước thực hiện**

Dùng thuật toán **Floyd's Cycle Detection** (Rùa-Thỏ):

**Bước 1:** Nếu danh sách rỗng → return false

**Bước 2:** Khởi tạo `slow = head`, `fast = head`

**Bước 3:** Duyệt trong khi `fast != NULL && fast->next != NULL`:
→ `slow = slow->next` (nhảy 1)
→ `fast = fast->next->next` (nhảy 2)
→ Nếu `slow == fast` → có vòng lặp, return true

**Bước 4:** fast chạm NULL → không có vòng lặp, return false

> Nếu có cycle: fast và slow chắc chắn sẽ gặp nhau tại một điểm trong vòng lặp

### **2. Dữ liệu vào / ra**
- Input: head
- Output: true (có cycle) / false (không có cycle)

### **3. Ví dụ**
```
1 → 2 → 3 → 4 → 5
              ↑       |
              └───────┘  ← cycle tại node 3
```
Output: **true**

### **4. Mã C++**
```cpp
bool hasCycle(Node* head) {
    if (head == nullptr) return false;

    Node* slow = head;
    Node* fast = head;

    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;

        if (slow == fast) return true; // Gặp nhau → có cycle
    }

    return false; // fast chạm NULL → không có cycle
}
```

---

# **PHẦN 3: CƠ BẢN NHƯNG NÊN BIẾT ⭐**

## **THUẬT TOÁN 11: DUYỆT VÀ IN DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Kiểm tra rỗng → in thông báo

**Bước 2:** Duyệt từ head tới cuối, in từng node

**Bước 3:** In dạng: `data1 → data2 → ... → NULL`

### **2. Mã C++**
```cpp
void printList(Node* head) {
    if (head == nullptr) {
        cout << "Danh sách rỗng!" << endl;
        return;
    }

    Node* current = head;
    while (current != nullptr) {
        cout << current->data;
        if (current->next != nullptr) cout << " → ";
        current = current->next;
    }
    cout << " → NULL" << endl;
}
```

---

## **THUẬT TOÁN 12: HOÁN ĐỔI GIÁ TRỊ 2 NODE TẠI VỊ TRÍ i VÀ j**

### **1. Ý tưởng & Các bước thực hiện**

**Bước 1:** Kiểm tra i và j hợp lệ (i != j, đều trong phạm vi)

**Bước 2:** Duyệt tìm node tại vị trí i, lưu vào `nodeI`

**Bước 3:** Duyệt tìm node tại vị trí j, lưu vào `nodeJ`

**Bước 4:** Nếu tìm được cả 2 → đổi chỗ giá trị: `swap(nodeI->data, nodeJ->data)`

### **2. Dữ liệu vào / ra**
- Input: head, i, j
- Output: Giá trị 2 node tại i và j được hoán đổi

### **3. Ví dụ**
Danh sách: 1 → 2 → 3 → 4 → 5, i=2, j=4 → Output: **1 → 4 → 3 → 2 → 5**

### **4. Mã C++**
```cpp
void swapAt(Node* head, int i, int j) {
    if (i == j) return;

    Node* nodeI = nullptr;
    Node* nodeJ = nullptr;
    Node* current = head;
    int count = 1;

    while (current != nullptr) {
        if (count == i) nodeI = current;
        if (count == j) nodeJ = current;
        current = current->next;
        count++;
    }

    if (nodeI != nullptr && nodeJ != nullptr) {
        swap(nodeI->data, nodeJ->data);
    }
}
```

---

# **BẢNG TỔNG HỢP 12 THUẬT TOÁN BỔ SUNG**

| # | Tên thuật toán | Mức độ | Ý tưởng chính |
|---|---|---|---|
| 1 | search | ⭐⭐⭐ | Duyệt tìm giá trị x, trả vị trí |
| 2 | countNodes | ⭐⭐⭐ | Duyệt đếm tất cả node |
| 3 | countOccurrences | ⭐⭐⭐ | Đếm số lần x xuất hiện |
| 4 | sumList | ⭐⭐⭐ | Tính tổng tất cả giá trị |
| 5 | bubbleSort | ⭐⭐⭐ | Đổi chỗ giá trị khi sai thứ tự |
| 6 | findMiddle | ⭐⭐⭐ | Rùa-Thỏ tìm node giữa |
| 7 | getAt | ⭐⭐ | Duyệt đến đúng vị trí k |
| 8 | getKthFromEnd | ⭐⭐ | 2 con trỏ cách nhau k bước |
| 9 | mergeSorted | ⭐⭐ | Ghép 2 DS đã sắp xếp |
| 10 | hasCycle | ⭐⭐ | Floyd: slow/fast, gặp nhau = cycle |
| 11 | printList | ⭐ | Duyệt in từng node |
| 12 | swapAt | ⭐ | Tìm 2 node, đổi chỗ giá trị |

---

## **TỔNG KẾT: TẤT CẢ THUẬT TOÁN DSLK ĐƠN**

| # | Thuật toán | Nhóm |
|---|---|---|
| 1 | insertHead | Chèn |
| 2 | insertTail | Chèn |
| 3 | insertAt | Chèn |
| 4 | deleteHead | Xóa |
| 5 | deleteTail | Xóa |
| 6 | deleteAt | Xóa |
| 7 | deleteAllX | Xóa |
| 8 | reverseList | Biến đổi |
| 9 | splitEvenOdd | Biến đổi |
| 10 | removeDuplicates | Biến đổi |
| 11 | IsPalindrome | Kiểm tra |
| 12A | FindMin | Tìm kiếm |
| 12B | FindMax | Tìm kiếm |
| **13** | **search** | **Tìm kiếm** |
| **14** | **countNodes** | **Đếm** |
| **15** | **countOccurrences** | **Đếm** |
| **16** | **sumList** | **Tính toán** |
| **17** | **bubbleSort** | **Sắp xếp** |
| **18** | **findMiddle** | **Tìm kiếm** |
| **19** | **getAt** | **Tìm kiếm** |
| **20** | **getKthFromEnd** | **Tìm kiếm** |
| **21** | **mergeSorted** | **Biến đổi** |
| **22** | **hasCycle** | **Kiểm tra** |
| **23** | **printList** | **Duyệt** |
| **24** | **swapAt** | **Biến đổi** |

---

EOF
