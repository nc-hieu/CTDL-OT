# TỔNG HỢP 12 THUẬT TOÁN DANH SÁCH LIÊN KẾT ĐƠN

---

# **PHẦN 1: CÁC PHÉP CHÈN (INSERT)**

## **THUẬT TOÁN 1: CHÈN PHẦN TỬ VÀO ĐẦU DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

Để chèn một phần tử vào đầu danh sách liên kết:

**Bước 1:** Tạo một node mới chứa giá trị x cần chèn
- Gọi `createNode(x)` để tạo node mới
- Lưu con trỏ này vào biến `p`

**Bước 2:** Liên kết node mới với danh sách hiện tại
- Gán `p->next = head` (node mới trỏ tới node đầu cũ)
- Điều này giữ toàn bộ danh sách cũ được nối với node mới

**Bước 3:** Cập nhật con trỏ head để trỏ tới node mới
- Gán `head = p` để head bây giờ trỏ tới node mới
- Node mới trở thành đầu danh sách

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu danh sách (có thể NULL)
- x: giá trị cần chèn

### **3. Dữ liệu ra (Output)**
- Danh sách được cập nhật, head trỏ tới node mới

### **4. Ví dụ**

**Input:** head: 2 → 3 → 5, x = 1

**Output:** head: 1 → 2 → 3 → 5

### **5. Mã C++**

```cpp
void insertHead(Node* &head, int x){
    Node* p = createNode(x);
    p->next = head;
    head = p;
}
```

---

## **THUẬT TOÁN 2: CHÈN PHẦN TỬ VÀO CUỐI DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

Để chèn một phần tử vào cuối danh sách liên kết:

**Bước 1:** Tạo một node mới chứa giá trị x
- Gọi `createNode(x)` để tạo node mới
- Lưu con trỏ này vào biến `p`

**Bước 2:** Kiểm tra xem danh sách có rỗng không
- Nếu `head == nullptr` (danh sách rỗng):
  - Gán `head = p` (node mới trở thành head)
  - Return để kết thúc hàm

**Bước 3:** Nếu danh sách không rỗng, duyệt tới node cuối cùng
- Khởi tạo `temp = head` để bắt đầu từ node đầu
- Dùng vòng lặp `while (temp->next != nullptr)` để tiến tới node cuối
  - Trong vòng lặp: `temp = temp->next` (dịch temp sang node tiếp theo)
  - Dừng khi `temp->next == nullptr` (temp hiện tại là node cuối)

**Bước 4:** Liên kết node mới vào cuối danh sách
- Gán `temp->next = p` (node cuối cũ trỏ tới node mới)
- Node mới hiện không có con (p->next = NULL mặc định)
- Danh sách được mở rộng thêm 1 node ở cuối

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu danh sách (có thể NULL)
- x: giá trị cần chèn

### **3. Dữ liệu ra (Output)**
- Danh sách được cập nhật, node mới ở cuối

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3, x = 5

**Output:** head: 1 → 2 → 3 → 5

### **5. Mã C++**

```cpp
void insertTail(Node* &head, int x){
    Node* p = createNode(x);
    
    if(head == nullptr){
        head = p;
        return;
    }

    Node* temp = head;
    while (temp->next != nullptr){
        temp = temp->next;
    }
    temp->next = p;
}
```

---

## **THUẬT TOÁN 3: CHÈN PHẦN TỬ TẠI VỊ TRÍ K**

### **1. Ý tưởng & Các bước thực hiện**

Để chèn một phần tử vào vị trí k cụ thể trong danh sách:

**Bước 1:** Kiểm tra tính hợp lệ của vị trí k
- Nếu `k < 1`: vị trí không hợp lệ, in lỗi và return

**Bước 2:** Kiểm tra trường hợp đặc biệt (danh sách rỗng)
- Nếu `head == nullptr` và `k > 1`: không thể chèn vào vị trí k vì danh sách rỗng, in lỗi và return

**Bước 3:** Tạo node mới
- Gọi `createNode(value)` để tạo node mới
- Lưu con trỏ vào biến `p`

**Bước 4:** Trường hợp chèn vào đầu (k == 1)
- Gán `p->next = head` (node mới trỏ tới node đầu cũ)
- Gán `head = p` (head trỏ tới node mới)
- Return để kết thúc

**Bước 5:** Trường hợp chèn vào giữa hoặc cuối (k > 1)
- Khởi tạo `current = head` và `count = 1`
- Dùng vòng lặp để duyệt tới node ở vị trí (k-1):
  - Điều kiện: `current->next != nullptr && count < k - 1`
  - Trong vòng lặp: `current = current->next` và `count++`
  - Dừng khi tìm được node (k-1)

**Bước 6:** Kiểm tra vị trí k có hợp lệ không
- Nếu `current->next == nullptr && count < k - 1`:
  - Vị trí k vượt quá độ dài danh sách + 1
  - In lỗi, giải phóng node mới (`delete p`), và return

**Bước 7:** Chèn node mới vào vị trí k
- Gán `p->next = current->next` (node mới trỏ tới node (k+1))
- Gán `current->next = p` (node (k-1) trỏ tới node mới)
- Node mới giờ nằm ở vị trí k

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu
- value: giá trị cần chèn
- k: vị trí chèn (1 ≤ k ≤ độ dài+1)

### **3. Dữ liệu ra (Output)**
- Node mới được chèn tại vị trí k

### **4. Ví dụ**

**Input:** head: 1 → 3 → 5, value = 2, k = 2

**Output:** head: 1 → 2 → 3 → 5

### **5. Mã C++**

```cpp
void insertAt(Node* &head, int value, int k) {
    if (k < 1) {
        cout << "Vị trí không hợp lệ!";
        return;
    }

    if (head == nullptr && k > 1) {
        cout << "Vị trí không hợp lệ!";
        return;
    }

    Node* p = createNode(value);

    if (k == 1) {
        p->next = head;
        head = p;
        return;
    }

    Node* current = head;
    int count = 1;

    while (current->next != nullptr && count < k - 1) {
        current = current->next;
        count++;
    }

    if (current->next == nullptr && count < k - 1) {
        cout << "Vị trí không hợp lệ!";
        delete p;
        return;
    }

    p->next = current->next;
    current->next = p;
}
```

---

# **PHẦN 2: CÁC PHÉP XÓA (DELETE)**

## **THUẬT TOÁN 4: XÓA NODE ĐẦU DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

Để xóa node đầu danh sách liên kết:

**Bước 1:** Kiểm tra danh sách có rỗng không
- Nếu `head == nullptr`: danh sách rỗng, không có gì để xóa, return

**Bước 2:** Lưu con trỏ node đầu hiện tại
- Gán `temp = head` để giữ lại địa chỉ của node cần xóa

**Bước 3:** Cập nhật con trỏ head sang node tiếp theo
- Gán `head = head->next` (head trỏ tới node thứ 2)
- Nếu danh sách chỉ có 1 node, `head` sẽ trở thành NULL

**Bước 4:** Giải phóng bộ nhớ của node cũ
- Gọi `delete temp` để tiêu hủy node đầu cũ
- Quan trọng: phải xóa trước khi mất đường dẫn đến node này

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu

### **3. Dữ liệu ra (Output)**
- Node đầu bị xóa, head dịch sang node tiếp theo

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3

**Output:** head: 2 → 3

### **5. Mã C++**

```cpp
void deleteHead(Node* &head){
    if(head == nullptr) return;
    Node* temp = head;
    head = head->next;
    delete temp;
}
```

---

## **THUẬT TOÁN 5: XÓA NODE CUỐI DANH SÁCH**

### **1. Ý tưởng & Các bước thực hiện**

Để xóa node cuối danh sách liên kết:

**Bước 1:** Kiểm tra danh sách có rỗng không
- Nếu `head == nullptr`: danh sách rỗng, không có gì để xóa, return

**Bước 2:** Kiểm tra trường hợp đặc biệt (danh sách chỉ có 1 node)
- Nếu `head->next == nullptr`: danh sách chỉ có node đầu
  - Gọi `delete head` để xóa node duy nhất này
  - Gán `head = nullptr` để đánh dấu danh sách trở nên rỗng
  - Return để kết thúc

**Bước 3:** Duyệt tới node kề cuối (node có con trỏ next trỏ tới node cuối)
- Khởi tạo `current = head`
- Dùng vòng lặp điều kiện `current->next->next != nullptr`:
  - Tiếp tục lặp khi `current->next->next` không NULL
  - Dịch: `current = current->next`
  - Dừng khi `current->next->next == nullptr` (current giờ là node kề cuối)

**Bước 4:** Lưu con trỏ node cuối cần xóa
- Gán `temp = current->next` (temp trỏ tới node cuối)

**Bước 5:** Cắt đứt liên kết cuối cùng
- Gán `current->next = nullptr` (node kề cuối không còn con trỏ tới node cuối)

**Bước 6:** Giải phóng bộ nhớ node cuối
- Gọi `delete temp` để xóa node cuối cũ
- Danh sách giờ kết thúc tại node kề cuối

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu

### **3. Dữ liệu ra (Output)**
- Node cuối bị xóa, danh sách rút ngắn 1 phần tử

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3

**Output:** head: 1 → 2

### **5. Mã C++**

```cpp
void deleteTail(Node* &head) {
    if (head == nullptr) return;

    if (head->next == nullptr) {
        delete head;
        head = nullptr;
        return;
    }

    Node* current = head;
    while (current->next->next != nullptr) {
        current = current->next;
    }

    Node* temp = current->next;
    current->next = nullptr;
    delete temp;
}
```

---

## **THUẬT TOÁN 6: XÓA PHẦN TỬ TẠI VỊ TRÍ K**

### **1. Ý tưởng & Các bước thực hiện**

Để xóa node tại vị trí k cụ thể:

**Bước 1:** Kiểm tra danh sách có rỗng không hoặc k không hợp lệ
- Nếu `head == nullptr` hoặc `k < 1`: không thể xóa, in lỗi và return

**Bước 2:** Trường hợp xóa node đầu (k == 1)
- Lưu `temp = head`
- Gán `head = head->next`
- Gọi `delete temp` để giải phóng bộ nhớ
- Return để kết thúc

**Bước 3:** Trường hợp xóa từ giữa hoặc cuối (k > 1)
- Khởi tạo `current = head` và `count = 1`
- Duyệt tìm node ở vị trí (k-1):
  - Vòng lặp: `while (current->next != nullptr && count < k-1)`
  - Trong lặp: `current = current->next` và `count++`
  - Dừng khi tìm được node (k-1)

**Bước 4:** Kiểm tra node (k) có tồn tại không
- Nếu `current->next == nullptr`: vị trí k không tồn tại, in lỗi và return

**Bước 5:** Xóa node tại vị trí k bằng nối tắt
- Lưu `temp = current->next` (temp trỏ tới node cần xóa)
- Gán `current->next = temp->next` (node (k-1) trỏ thẳng tới node (k+1), bỏ qua node k)
- Gọi `delete temp` để giải phóng bộ nhớ node (k)

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu
- k: vị trí cần xóa

### **3. Dữ liệu ra (Output)**
- Node tại vị trí k bị xóa, danh sách được cập nhật

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3 → 4, k = 2

**Output:** head: 1 → 3 → 4

### **5. Mã C++**

```cpp
void deleteAt(Node* &head, int k) {
    if (head == nullptr) return;

    if (k < 1 ){
        cout << "Vị trí không hợp lệ!";
        return;
    }

    if (k == 1) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return;
    }

    Node* current = head;
    int count = 1;

    while (current->next != nullptr && count < k-1) {
        current = current->next;
        count++;
    }

    if (current->next == nullptr){
        cout << "Vị trí không hợp lệ!";
        return; 
    } 

    Node* temp = current->next;
    current->next = temp->next;
    delete temp;
}
```

---

## **THUẬT TOÁN 7: XÓA TẤT CẢ PHẦN TỬ CÓ GIÁ TRỊ X**

### **1. Ý tưởng & Các bước thực hiện**

Để xóa tất cả node có giá trị bằng x:

**Bước 1:** Xóa tất cả node x ở đầu danh sách (có thể liên tiếp)
- Dùng vòng lặp `while (head != nullptr && head->data == x)`:
  - Lưu `temp = head`
  - Gán `head = head->next` (dịch head sang node tiếp theo)
  - Gọi `delete temp` để xóa node x cũ
  - Lặp lại nếu node đầu mới vẫn = x

**Bước 2:** Kiểm tra nếu danh sách trở nên rỗng
- Nếu `head == nullptr`: toàn bộ danh sách là x, return

**Bước 3:** Xóa node x ở giữa hoặc cuối
- Khởi tạo `current = head` (bắt đầu từ node đầu hiện tại)
- Dùng vòng lặp `while (current->next != nullptr)`:
  - Kiểm tra `current->next->data == x`:
    - Nếu đúng: xóa node kế tiếp
      - Lưu `temp = current->next`
      - Gán `current->next = temp->next` (nối tắt bỏ qua node x)
      - Gọi `delete temp`
      - **Quan trọng:** Không tăng current vì node mới đôn lên có thể vẫn = x
    - Nếu sai: dịch current sang node tiếp theo (`current = current->next`)

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu
- x: giá trị cần xóa

### **3. Dữ liệu ra (Output)**
- Tất cả node có giá trị x bị xóa

### **4. Ví dụ**

**Input:** head: 1 → 2 → 2 → 2 → 3, x = 2

**Output:** head: 1 → 3

### **5. Mã C++**

```cpp
void deleteAllX(Node* &head, int x) {
    while (head != nullptr && head->data == x) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    if (head == nullptr) return;

    Node* current = head;
    while (current->next != nullptr) {
        if (current->next->data == x) {
            Node* temp = current->next;
            current->next = temp->next;
            delete temp;
        } else {
            current = current->next;
        }
    }
}
```

---

# **PHẦN 3: CÁC PHÉP BIẾN ĐỔI (TRANSFORM)**

## **THUẬT TOÁN 8: ĐẢO NGƯỢC DANH SÁCH LIÊN KẾT**

### **1. Ý tưởng & Các bước thực hiện**

Để đảo ngược danh sách liên kết:

**Bước 1:** Khởi tạo 3 con trỏ
- `prev = nullptr` (node trước đó, lúc đầu là NULL)
- `current = head` (node hiện tại, bắt đầu từ đầu)
- `nextNode = nullptr` (node tiếp theo, để lưu tạm)

**Bước 2:** Lưu lại node tiếp theo trước khi cắt liên kết
- Gán `nextNode = current->next` (lưu địa chỉ node tiếp theo)
- Điều này quan trọng vì sau bước 3 sẽ mất con trỏ tới node này

**Bước 3:** Quay ngược mũi tên của node hiện tại
- Gán `current->next = prev` (node hiện tại trỏ về node trước nó thay vì node sau)
- Như thế chiều mũi tên bị đảo ngược

**Bước 4:** Dịch 3 con trỏ sang node tiếp theo
- Gán `prev = current` (prev bây giờ trỏ tới node vừa xử lý)
- Gán `current = nextNode` (current dịch sang node tiếp theo)

**Bước 5:** Lặp lại bước 2-4 cho tất cả node
- Điều kiện: `while (current != nullptr)`
- Dừng khi current chạm tới cuối danh sách (NULL)

**Bước 6:** Cập nhật head
- Gán `head = prev` (head trỏ tới node cuối cũ, vừa trở thành đầu mới)

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node gốc

### **3. Dữ liệu ra (Output)**
- Danh sách được đảo ngược hoàn toàn

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3 → 4 → 5

**Output:** head: 5 → 4 → 3 → 2 → 1

### **5. Mã C++**

```cpp
void reverseList(Node* &head) {
    Node* prev = nullptr;
    Node* current = head;
    Node* nextNode = nullptr;

    while (current != nullptr) {
        nextNode = current->next;
        current->next = prev;
        
        prev = current;
        current = nextNode;
    }
    
    head = prev;
}
```

---

## **THUẬT TOÁN 9: TÁCH DANH SÁCH THÀNH SỐ CHẴN VÀ LẺ**

### **1. Ý tưởng & Các bước thực hiện**

Để tách danh sách thành 2 danh sách (chẵn và lẻ):

**Bước 1:** Khởi tạo 2 danh sách rỗng và 2 con trỏ tail
- Gán `pEven = NULL, pOdd = NULL` (đầu của 2 danh sách mới)
- Gán `tailEven = NULL, tailOdd = NULL` (cuối của 2 danh sách mới)

**Bước 2:** Duyệt qua danh sách gốc từng node
- Khởi tạo `current = head`
- Dùng vòng lặp `while (current != NULL)`

**Bước 3:** Lưu lại node tiếp theo trước khi cắt liên kết
- Gán `nextNode = current->next` (lưu địa chỉ node tiếp theo)

**Bước 4:** Cô lập node hiện tại
- Gán `current->next = NULL` (cắt đứt liên kết của node này)
- Node lúc này không trỏ tới node nào khác

**Bước 5:** Phân loại node theo chẵn hoặc lẻ
- Kiểm tra `current->data % 2 == 0` (số chẵn):
  - Nếu danh sách chẵn rỗng (`pEven == NULL`):
    - Gán `pEven = current, tailEven = current` (current là node đầu)
  - Nếu không rỗng:
    - Gán `tailEven->next = current` (liên kết node vào đuôi)
    - Gán `tailEven = current` (dời tailEven lên node mới)
- Tương tự cho danh sách lẻ

**Bước 6:** Dịch sang node tiếp theo
- Gán `current = nextNode` (duyệt tiếp node tiếp theo)

**Bước 7:** Rút cạn danh sách gốc
- Gán `head = NULL` (danh sách gốc trở thành rỗng vì các node đã được tách)

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu danh sách gốc

### **3. Dữ liệu ra (Output)**
- pEven: danh sách chứa phần tử chẵn
- pOdd: danh sách chứa phần tử lẻ
- head: được set = NULL

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3 → 4 → 5

**Output:** 
- pEven: 2 → 4 → NULL
- pOdd: 1 → 3 → 5 → NULL

### **5. Mã C++**

```cpp
void splitEvenOdd(Node* &head, Node* &pEven, Node* &pOdd) {
    pEven = NULL; pOdd = NULL;
    Node* tailEven = NULL; 
    Node* tailOdd = NULL;
    
    Node* current = head;
    
    while (current != NULL) {
        Node* nextNode = current->next;
        current->next = NULL;
        
        if (current->data % 2 == 0) {
            if (pEven == NULL) {
                pEven = current;
                tailEven = current;
            } else {
                tailEven->next = current;
                tailEven = current;
            }
        } else {
            if (pOdd == NULL) {
                pOdd = current;
                tailOdd = current;
            } else {
                tailOdd->next = current;
                tailOdd = current;
            }
        }
        
        current = nextNode;
    }
    
    head = NULL;
}
```

---

## **THUẬT TOÁN 10: XÓA CÁC PHẦN TỬ TRÙNG LẶP**

### **1. Ý tưởng & Các bước thực hiện**

Để xóa tất cả phần tử trùng lặp:

**Bước 1:** Kiểm tra danh sách có rỗng hoặc chỉ 1 node
- Nếu `head == NULL || head->next == NULL`: không có trùng, return

**Bước 2:** Duyệt từng phần tử (current)
- Khởi tạo `current = head`
- Dùng vòng lặp `while (current->next != NULL)`

**Bước 3:** Với mỗi phần tử, dò xét các phần tử phía sau (runner)
- Khởi tạo `runner = current` (runner cũng bắt đầu từ current)
- Dùng vòng lặp `while (runner->next != NULL)`

**Bước 4:** Kiểm tra node kế tiếp của runner có trùng với current không
- Nếu `runner->next->data == current->data`:
  - Xóa node kế tiếp:
    - Lưu `temp = runner->next` (node cần xóa)
    - Gán `runner->next = temp->next` (nối tắt bỏ qua node trùng)
    - Gọi `delete temp`
    - **Quan trọng:** Không tăng runner vì node mới đôn lên có thể vẫn trùng
- Nếu không trùng:
  - Gán `runner = runner->next` (dịch runner sang node tiếp theo)

**Bước 5:** Sang phần tử tiếp theo
- Gán `current = current->next` (duyệt tiếp phần tử kế tiếp)

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu

### **3. Dữ liệu ra (Output)**
- Tất cả node trùng bị xóa, chỉ giữ lại node đầu tiên

### **4. Ví dụ**

**Input:** head: 1 → 2 → 1 → 2 → 1 → 3

**Output:** head: 1 → 2 → 3

### **5. Mã C++**

```cpp
void removeDuplicates(Node* head) {
    if (head == NULL || head->next == NULL) return;

    Node* current = head;

    while (current->next != NULL) {
        Node* runner = current;
        
        while (runner->next != NULL) {
            if (runner->next->data == current->data) {
                Node* temp = runner->next;
                runner->next = temp->next;
                delete temp;
            } else {
                runner = runner->next;
            }
        }
        current = current->next;
    }
}
```

---

# **PHẦN 4: CÁC PHÉP TÌM KIẾM (SEARCH)**

## **THUẬT TOÁN 11: KIỂM TRA DANH SÁCH CÓ PHẢI LÀ PALINDROME KHÔNG**

### **1. Ý tưởng & Các bước thực hiện**

Để kiểm tra danh sách liên kết có phải Palindrome (đối xứng):

**Bước 1:** Kiểm tra trường hợp đặc biệt
- Nếu `head == NULL || head->next == NULL`: rỗng hoặc 1 node là Palindrome, return true

**Bước 2:** Tìm điểm giữa danh sách (phương pháp Rùa-Thỏ)
- Khởi tạo `slow = head` (rùa, nhảy 1 bước)
- Khởi tạo `fast = head` (thỏ, nhảy 2 bước)
- Dùng vòng lặp `while (fast != NULL && fast->next != NULL)`:
  - Gán `slow = slow->next` (rùa nhảy 1 bước)
  - Gán `fast = fast->next->next` (thỏ nhảy 2 bước)
  - Khi thỏ chạm đích, rùa đang đúng ở chính giữa

**Bước 3:** Đảo ngược nửa sau danh sách
- Khởi tạo 3 con trỏ: `prev = NULL, curr = slow, nextNode = NULL`
- Khởi tạo `secondHalfHead = NULL` (để lưu head nửa sau sau khi đảo)
- Đảo ngược từ `slow` tới cuối danh sách:
  - Dùng vòng lặp `while (curr != NULL)`:
    - Gán `nextNode = curr->next`
    - Gán `curr->next = prev`
    - Gán `prev = curr, secondHalfHead = prev`
    - Gán `curr = nextNode`

**Bước 4:** So sánh 2 nửa
- Khởi tạo `p1 = head` (chạy nửa trước từ đầu)
- Khởi tạo `p2 = secondHalfHead` (chạy nửa sau từ head mới)
- Khởi tạo `isPalin = true`
- Dùng vòng lặp `while (p2 != NULL)`:
  - Nếu `p1->data != p2->data`: gán `isPalin = false`, break
  - Dịch: `p1 = p1->next, p2 = p2->next`

**Bước 5:** Khôi phục nửa sau (đảo lần 2 để trở về trạng thái gốc)
- Tương tự bước 3, đảo ngược nửa sau từ `secondHalfHead` lần nữa

**Bước 6:** Return kết quả
- Trả về `isPalin`

### **2. Dữ liệu vào (Input)**
- head: con trỏ tới node đầu

### **3. Dữ liệu ra (Output)**
- true: nếu danh sách là Palindrome
- false: nếu không

### **4. Ví dụ**

**Input:** head: 1 → 2 → 3 → 2 → 1

**Output:** true (là Palindrome)

**Input:** head: 1 → 2 → 3

**Output:** false (không là Palindrome)

### **5. Mã C++**

```cpp
bool IsPalindrome(Node* head) {
    if (head == NULL || head->next == NULL) return true;

    Node* slow = head;
    Node* fast = head;
    
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    Node* prev = NULL;
    Node* curr = slow;
    Node* nextNode = NULL;
    Node* secondHalfHead = NULL;
    
    while (curr != NULL) {
        nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        secondHalfHead = prev;
        curr = nextNode;
    }

    Node* p1 = head;
    Node* p2 = secondHalfHead;
    
    bool isPalin = true;
    while (p2 != NULL) {
        if (p1->data != p2->data) {
            isPalin = false;
            break;
        }
        p1 = p1->next;
        p2 = p2->next;
    }
    
    prev = NULL;
    curr = secondHalfHead;
    
    while (curr != NULL) {
        nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    
    return isPalin;
}
```

---

## **THUẬT TOÁN 12: TÌM GIÁ TRỊ NHỎ NHẤT VÀ LỚN NHẤT**

### **THUẬT TOÁN 12A: TÌM GIÁ TRỊ NHỎ NHẤT**

### **1. Ý tưởng & Các bước thực hiện**

Để tìm phần tử có giá trị nhỏ nhất:

**Bước 1:** Kiểm tra danh sách có rỗng không
- Nếu `pHead == NULL`: danh sách rỗng, không có giá trị, in lỗi và return -1

**Bước 2:** Khởi tạo giá trị min
- Gán `minVal = pHead->data` (min ban đầu = giá trị node đầu)

**Bước 3:** Duyệt từ node thứ 2 tới cuối
- Khởi tạo `current = pHead->next`
- Dùng vòng lặp `while (current != NULL)`

**Bước 4:** So sánh mỗi node với minVal hiện tại
- Nếu `current->data < minVal`:
  - Gán `minVal = current->data` (cập nhật minVal nhỏ hơn)
- Dịch: `current = current->next`

**Bước 5:** Return giá trị min tìm được
- Trả về `minVal`

### **2. Dữ liệu vào (Input)**
- pHead: con trỏ tới node đầu

### **3. Dữ liệu ra (Output)**
- Giá trị nhỏ nhất (int)
- Nếu danh sách rỗng trả về -1

### **4. Ví dụ**

**Input:** head: 5 → 2 → 8 → 1 → 9

**Output:** 1

### **5. Mã C++**

```cpp
int FindMin(Node* pHead) {
    if (pHead == NULL) {
        cout << "Loi: Danh sach rong!" << endl;
        return -1;
    }

    int minVal = pHead->data;
    Node* current = pHead->next;

    while (current != NULL) {
        if (current->data < minVal) {
            minVal = current->data;
        }
        current = current->next;
    }
    
    return minVal;
}
```

---

### **THUẬT TOÁN 12B: TÌM GIÁ TRỊ LỚN NHẤT**

### **1. Ý tưởng & Các bước thực hiện**

Để tìm phần tử có giá trị lớn nhất:

**Bước 1:** Kiểm tra danh sách có rỗng không
- Nếu `pHead == NULL`: danh sách rỗng, không có giá trị, in lỗi và return -1

**Bước 2:** Khởi tạo giá trị max
- Gán `maxVal = pHead->data` (max ban đầu = giá trị node đầu)

**Bước 3:** Duyệt từ node thứ 2 tới cuối
- Khởi tạo `current = pHead->next`
- Dùng vòng lặp `while (current != NULL)`

**Bước 4:** So sánh mỗi node với maxVal hiện tại
- Nếu `current->data > maxVal`:
  - Gán `maxVal = current->data` (cập nhật maxVal lớn hơn)
- Dịch: `current = current->next`

**Bước 5:** Return giá trị max tìm được
- Trả về `maxVal`

### **2. Dữ liệu vào (Input)**
- pHead: con trỏ tới node đầu

### **3. Dữ liệu ra (Output)**
- Giá trị lớn nhất (int)
- Nếu danh sách rỗng trả về -1

### **4. Ví dụ**

**Input:** head: 5 → 2 → 8 → 1 → 9

**Output:** 9

### **5. Mã C++**

```cpp
int FindMax(Node* pHead) {
    if (pHead == NULL) {
        cout << "Loi: Danh sach rong!" << endl;
        return -1;
    }

    int maxVal = pHead->data;
    Node* current = pHead->next;

    while (current != NULL) {
        if (current->data > maxVal) {
            maxVal = current->data;
        }
        current = current->next;
    }
    
    return maxVal;
}
```

---

# **BẢNG TỔNG HỢP 12 THUẬT TOÁN**

| # | Tên thuật toán | Loại | Ý tưởng chính | Độ khó |
|---|---|---|---|---|
| 1 | insertHead | Chèn | Chèn vào đầu | ⭐ |
| 2 | insertTail | Chèn | Chèn vào cuối | ⭐ |
| 3 | insertAt | Chèn | Chèn tại vị trí k | ⭐⭐ |
| 4 | deleteHead | Xóa | Xóa đầu | ⭐ |
| 5 | deleteTail | Xóa | Xóa cuối | ⭐⭐ |
| 6 | deleteAt | Xóa | Xóa tại vị trí k | ⭐⭐ |
| 7 | deleteAllX | Xóa | Xóa tất cả x | ⭐⭐ |
| 8 | reverseList | Biến đổi | Đảo ngược | ⭐⭐ |
| 9 | splitEvenOdd | Biến đổi | Tách chẵn/lẻ | ⭐⭐ |
| 10 | removeDuplicates | Biến đổi | Xóa trùng | ⭐⭐ |
| 11 | IsPalindrome | Kiểm tra | Kiểm tra Palindrome | ⭐⭐⭐ |
| 12A | FindMin | Tìm kiếm | Tìm min | ⭐ |
| 12B | FindMax | Tìm kiếm | Tìm max | ⭐ |

---
