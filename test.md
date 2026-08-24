Chào mừng bạn đến với phần học **tự viết Dockerfile**! Đây được coi là kỹ năng quan trọng bậc nhất giúp xóa nhòa khoảng cách giữa lập trình viên (Dev) và người vận hành hệ thống (Ops). Thay vì phải cài đặt ứng dụng một cách thủ công, Dockerfile cho phép chúng ta khai báo toàn bộ môi trường chạy bằng code (Infrastructure as Code) một cách rõ ràng, dễ đọc, và có thể quản lý bằng Git.

Để bạn có thể tự tin tự viết bất kỳ Dockerfile nào từ cơ bản đến phức tạp, tôi sẽ giải thích thật kỹ và chi tiết từ quy tắc viết, bản chất hoạt động của các câu lệnh, cho đến các kỹ thuật tối ưu hóa nâng cao được đúc kết từ các tài liệu chuyên gia của bạn.

---

### I. QUY TẮC ĐẶT TÊN VÀ ĐẶC TÍNH CỦA DOCKERFILE

1.  **Quy tắc đặt tên bắt buộc**: Tệp tin cấu hình phải được đặt tên chính xác là **`Dockerfile`** (bắt buộc phải viết hoa chữ **`D`**, viết liền và không có đuôi mở rộng như `.txt` hay `.sh`). Các cách đặt tên như `dockerfile` hay `Docker file` đều không hợp lệ.
    *   *Ngoại lệ*: Khi bạn có nhiều môi trường (như môi trường test, debug), bạn có thể đặt tên tệp tùy ý (ví dụ: `mailer-base.df` hoặc `app-dev.df`) nhưng lúc build bạn phải chỉ định rõ đường dẫn bằng cờ `-f`.
2.  **Nguyên tắc hoạt động**: Docker Engine sẽ đọc Dockerfile và thực thi tuần tự **từng dòng một từ trên xuống dưới** để xây dựng (build) nên Image.
3.  **Cú pháp chung**: Các dòng lệnh trong Dockerfile luôn tuân theo cấu trúc:
    \\[\text{INSTRUCTION argument}\\]
    Mặc dù tên các chỉ thị (`INSTRUCTION`) không phân biệt chữ hoa chữ thường, nhưng quy chuẩn chung của ngành công nghiệp là **luôn viết hoa toàn bộ các chỉ thị** để phân biệt rõ ràng với các tham số truyền vào.

---

### II. BẢN CHẤT KIẾN TRÚC: LAYER VẬT LÝ VS. SIÊU DỮ LIỆU (METADATA)

Một sai lầm phổ biến là nghĩ rằng mỗi dòng lệnh trong Dockerfile đều tạo ra một lớp dữ liệu (layer) mới làm nặng Image. Thực tế, Docker phân biệt rất rõ ràng giữa hai loại chỉ thị:

1.  **Chỉ thị tạo Layer Vật lý (Physical Layers)**: Đây là các chỉ thị trực tiếp thêm/sửa/xóa tệp tin hoặc cài đặt phần mềm vào Image. Mỗi chỉ thị này sẽ tạo ra một lớp dữ liệu vật lý thực sự và làm thay đổi dung lượng của Image.
    *   Các chỉ thị thuộc nhóm này: **`FROM`**, **`RUN`**, **`COPY`**, **`ADD`**.
2.  **Chỉ thị cấu hình Siêu dữ liệu (Metadata)**: Các chỉ thị này không thêm bất kỳ tệp tin nào, do đó **không tạo ra layer vật lý và không làm tăng dung lượng Image**. Chúng chỉ ghi nhận các thiết lập cấu hình vào file JSON metadata của Image để hướng dẫn container cách khởi chạy.
    *   Các chỉ thị thuộc nhóm này: **`LABEL`**, **`ENV`**, **`EXPOSE`**, **`WORKDIR`**, **`USER`**, **`ENTRYPOINT`**, **`CMD`**.

---

### III. GIẢI THÍCH CHI TIẾT TỪNG CHỈ THỊ (INSTRUCTIONS) CỐT LÕI

#### 1. FROM (Chỉ thị khởi nguồn)
Mọi Dockerfile hợp lệ **bắt buộc phải mở đầu bằng chỉ thị `FROM`**. Chỉ thị này xác định Image nền (Base Image) mà bạn muốn dùng làm móng để xây dựng ứng dụng của mình.
*   Cú pháp: `FROM <image_name>[:<tag>]`.
*   Ví dụ: `FROM node:18` hoặc `FROM python:3.10-slim`.
*   *Trường hợp đặc biệt*: Nếu bạn muốn xây dựng một Image trống rỗng hoàn toàn để tự đóng gói mã nguồn biên dịch sẵn (như Go hay Rust), bạn sử dụng: **`FROM scratch`**.

#### 2. LABEL (Ghi chú siêu dữ liệu)
Được dùng để gán các thông tin bổ sung (key/value) vào Image như tác giả, phiên bản, mô tả ứng dụng để phục vụ mục đích tra cứu.
*   Ví dụ: `LABEL maintainer="nguyenvana@gmail.com"`.

#### 3. RUN (Thực thi lệnh khi Build)
Chỉ thị này sẽ khởi chạy một tiến trình bên trong một container tạm thời trong quá trình build, thực hiện lệnh cài đặt, và lưu lại kết quả thành một layer mới.
*   Ví dụ: `RUN apt-get update && apt-get install -y git`.
*   *Mẹo viết chuẩn*: Để tránh tạo ra quá nhiều layer vật lý làm phình dung lượng Image, bạn nên **gộp các lệnh liên quan lại với nhau bằng toán tử `&&` và dấu gạch chéo ngược `\`** để xuống dòng.

#### 4. COPY vs. ADD (Đưa file từ ngoài vào container)
Cả hai chỉ thị này đều dùng để sao chép tệp tin từ máy host (nằm trong thư mục chứa Dockerfile - gọi là build context) vào bên trong Image. Tuy nhiên chúng có sự khác biệt lớn về tính năng:
*   **`COPY <nguồn> <đích>`**: Là lựa chọn an toàn và được khuyến khích sử dụng cho các tác vụ sao chép file/thư mục cục bộ thông thường.
*   **`ADD <nguồn> <đích>`**: Thừa hưởng tất cả tính năng của `COPY` nhưng bổ sung thêm 2 khả năng nâng cao:
    1.  Tự động tải tệp tin từ một đường dẫn URL trên Internet xuống Image.
    2.  Nếu file nguồn là một tệp nén cục bộ (như `.tar`, `.tgz`, `.zip`), `ADD` sẽ **tự động giải nén** tệp đó ra thư mục đích bên trong Image.
    *   *Khuyến cáo*: Không nên dùng `ADD` để tải file từ URL vì nó sẽ tạo ra layer lưu trữ file nén tạm mà không thể dọn dẹp sạch sẽ. Hãy dùng `RUN wget` hoặc `RUN curl` kết hợp giải nén và xóa file tạm trong một dòng lệnh `RUN` duy nhất để tối ưu dung lượng.

#### 5. ENV vs. ARG (Quản lý biến số)
*   **`ENV` (Environment Variable)**: Định nghĩa các biến môi trường sẽ **tồn tại cả trong quá trình build và cả khi container chạy thực tế (runtime)**.
    *   Ví dụ: `ENV APPROOT="/app"`. Các tiến trình chạy trong container sau này đều có thể đọc giá trị của biến này.
*   **`ARG` (Build Argument)**: Định nghĩa biến chỉ **tồn tại tạm thời trong lúc build Image**. Khi build xong, biến này sẽ biến mất và container chạy thực tế không nhìn thấy nó.
    *   Bạn có thể ghi đè giá trị này lúc gõ lệnh build qua cờ: `docker build --build-arg VERSION=2.0 .`.

#### 6. WORKDIR (Đặt thư mục làm việc mặc định)
Thay đổi thư mục hoạt động cho các lệnh `RUN`, `COPY`, `CMD`, `ENTRYPOINT` phía sau. Nó tương đương lệnh `cd` nhưng thông minh hơn ở chỗ: **nếu thư mục đích chưa tồn tại, nó sẽ tự động tạo ra thư mục đó**.
*   Ví dụ: `WORKDIR /app`.

#### 7. USER (Phân quyền bảo mật)
Mặc định, Docker sẽ thực thi mọi lệnh trong Dockerfile dưới quyền của người dùng cao nhất là `root`. Để tránh rủi ro bảo mật (nhỡ ứng dụng có lỗ hổng và hacker chiếm quyền điều khiển container), bạn nên **tạo một user hạn chế quyền và chuyển ngữ cảnh sang user đó** bằng chỉ thị `USER` trước khi khởi chạy ứng dụng.
*   Ví dụ:
    ```dockerfile
    RUN useradd -r -m -u 350 myuser
    USER myuser
    ```

#### 8. EXPOSE (Khai báo cổng kết nối)
Chỉ mang tính chất **tài liệu hóa (self-documentation)** giúp thông báo cho người vận hành hoặc các công cụ điều phối biết ứng dụng bên trong container sẽ lắng nghe trên cổng mạng nào. Chỉ thị này **không tự động mở hay map cổng ra máy host**; bạn vẫn cần khai báo cờ `-p` hoặc `-P` khi chạy container.
*   Ví dụ: `EXPOSE 8080`.

#### 9. ENTRYPOINT vs. CMD (Cấu hình lệnh khởi chạy)
Đây là hai chỉ thị dễ gây bối rối nhất nhưng lại cực kỳ quyền lực khi phối hợp với nhau. Chúng xác định lệnh nào sẽ được chạy mặc định khi container được khởi chạy.

##### A. Hai dạng viết (Formats):
*   **Dạng mảng Exec (Khuyên dùng)**: `ENTRYPOINT ["node", "app.js"]`. Docker sẽ chạy trực tiếp tiến trình mà không thông qua trình shell trung gian, giúp tiến trình nhận được đầy đủ các tín hiệu hệ thống (như `SIGTERM` khi dừng container).
*   **Dạng Shell**: `ENTRYPOINT node app.js`. Docker sẽ chạy lệnh dưới dạng `/bin/sh -c "node app.js"`. Việc này khiến tiến trình chính không mang PID 1 và không thể nhận tín hiệu tắt lịch sự từ Docker.

##### B. Cách phối hợp đỉnh cao:
*   **`ENTRYPOINT`**: Định nghĩa phần lệnh **cố định và không thể bị thay đổi** dễ dàng khi chạy container (trừ khi dùng cờ `--entrypoint`).
*   **`CMD`**: Định nghĩa phần **tham số mặc định** truyền vào cho `ENTRYPOINT`. Tham số này **có thể bị ghi đè hoàn toàn** bằng cách truyền tham số trực tiếp sau lệnh `docker run`.

> 💡 **Ví dụ thực tế phối hợp (Công cụ Ping)**:
> ```dockerfile
> ENTRYPOINT ["ping"]
> CMD ["google.com"]
> ```
> *   Nếu bạn chạy mặc định: `docker run my-ping` -> Container sẽ chạy: `ping google.com`.
> *   Nếu bạn ghi đè tham số: `docker run my-ping facebook.com` -> Container sẽ chạy: `ping facebook.com` (chữ `facebook.com` đã đè bẹp `google.com` của chỉ thị `CMD`).

---

### IV. CÁC CHIẾN THUẬT TỐI ƯU HÓA DOCKERFILE NÂNG CAO

#### 1. Cơ chế Caching và Quy tắc sắp xếp lệnh (Instruction Ordering)
Khi bạn chạy lệnh `docker build`, Docker sẽ kiểm tra xem dòng lệnh đó đã từng được build chưa để sử dụng lại bản lưu đệm (**Using cache**) nhằm tăng tốc độ build. 
*   **Nguyên lý phá vỡ cache**: Nếu một dòng lệnh trong Dockerfile bị thay đổi (hoặc file copy vào có sự thay đổi), **toàn bộ các dòng lệnh phía dưới dòng đó đều bị vô hiệu hóa cache** và buộc phải build lại từ đầu.
*   **Quy tắc sắp xếp**: Hãy đưa các chỉ thị **ít thay đổi lên trên cùng** (như cài đặt hệ điều hành, cài đặt thư viện hệ thống) và đưa các chỉ thị **thường xuyên thay đổi xuống dưới cùng** (như sao chép mã nguồn ứng dụng).

> ❌ **Cách viết tồi (Phá vỡ cache liên tục)**:
> ```dockerfile
> FROM node:18
> COPY . /app             # Code thay đổi liên tục khiến cache bị vỡ ngay tại đây!
> WORKDIR /app
> RUN npm install        # Dòng này cực kỳ nặng nhưng phải chạy lại mỗi lần bạn sửa code
> ```
> 
>  **Cách viết chuẩn (Tối ưu cache của chuyên gia)**:
> ```dockerfile
> FROM node:18
> WORKDIR /app
> COPY package.json .     # Chỉ copy file mô tả thư viện trước
> RUN npm install        # Chạy npm install. Dòng này chỉ phải chạy lại khi bạn thêm thư viện mới
> COPY . .                # Cuối cùng mới copy toàn bộ code vào để chạy
> ```

#### 2. Multi-stage Builds (Xây dựng đa giai đoạn - Tuyệt chiêu giảm dung lượng)
Một vấn đề lớn của môi trường sản xuất là Image quá nặng do phải gánh thêm các bộ công cụ biên dịch (SDK, Compiler, Git, v.v.) chỉ dùng lúc build ứng dụng. Việc này vừa tốn đĩa cứng, vừa tăng nguy cơ bảo mật hệ thống.

**Multi-stage Builds** cho phép bạn khai báo nhiều chỉ thị `FROM` trong cùng một Dockerfile. Mỗi `FROM` là một giai đoạn độc lập và bạn có thể **sao chép thành phẩm từ giai đoạn trước sang giai đoạn sau**.

>  **Ví dụ Dockerfile Đa giai đoạn hoàn chỉnh cho ứng dụng Go**:
> ```dockerfile
> # GIAI ĐOẠN 1: Biên dịch code (Sử dụng Image Golang nặng chứa đầy đủ công cụ)
> FROM golang:1.20-alpine AS builder
> WORKDIR /build
> COPY . .
> RUN go build -o myapp
> 
> # GIAI ĐOẠN 2: Chạy Production (Chỉ sử dụng một Image runtime siêu nhẹ)
> FROM alpine:latest AS production
> WORKDIR /app
> # Chỉ copy đúng file chạy duy nhất đã biên dịch ở giai đoạn 1 sang đây
> COPY --from=builder /build/myapp .
> ENTRYPOINT ["./myapp"]
> ```
> *Kết quả*: Image cuối cùng của bạn cực kỳ sạch sẽ, nhẹ (chỉ khoảng mười mấy MB thay vì hàng trăm MB ở giai đoạn build) và hoàn toàn bảo mật vì không chứa mã nguồn hay trình biên dịch thô.

---

💬 **Chúng ta đã đi qua toàn bộ cẩm nang chi tiết nhất về cách tự viết Dockerfile.** 

Bạn có muốn tôi hướng dẫn bạn tự viết thử một file Dockerfile hoàn chỉnh đầu tiên cho một dự án cụ thể (ví dụ: một trang web chạy bằng Node.js hoặc Python) để thực hành áp dụng ngay các quy tắc tối ưu cache này không?
