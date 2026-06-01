---
aliases:
  - Principal Component Analysis
  - Phân tích thành phần chính
  - PCA
---
# Principal Component Analysis
> [!abstract]+ Ý nghĩa thuật ngữ & Bản chất
> Thuật ngữ **Phân tích Thành phần chính** - *Principal Component Analysis (PCA)* là một kỹ thuật biến đổi tuyến tính, nhằm chiếu dữ liệu từ không gian đa chiều xuống một không gian con có số chiều nhỏ hơn (*lower-dimensional subspace*), sao cho lượng thông tin (đo bằng phương sai - *Variance*) được giữ lại là tối đa. Mục tiêu tối thượng của PCA là loại bỏ sự dư thừa của dữ liệu, nén thông tin và phá vỡ **Lời nguyền của số chiều** - *Curse of Dimensionality*.

---

## 1. Ý nghĩa thuật ngữ PCA

> [!abstract] Sự phình to giả tạo của dữ liệu
> **Phân tích Thành phần chính** (*Principal Component Analysis* - *PCA*)  là một thuật toán sinh ra từ một bài toán thực tế rằng khách hàng thường giao cho chúng ta một bảng dữ liệu có hàng trăm, hàng nghìn cột (số chiều cực lớn), nhưng thực chất lượng thông tin cốt lõi, không bị trùng lặp lại rất ít. 
> 
> Số lượng "thông tin cốt lõi, không trùng lặp" đó trong toán học gọi là **số chiều thực sự** (*intrinsic dimensionality*). 

Để dễ hiểu tại sao dữ liệu lại hay bị phình to trong thực tế, ta hãy xem xét ví dụ sau:

> [!example]+ Ví dụ trực giác: Số đo cơ thể con người
> Giả sử bạn đi thu thập dữ liệu đo lường cơ thể của 100 người. Bạn ghi nhận 2 biến số (2 cột dữ liệu):
> - Cột 1: Chiều dài cánh tay trái ($x_1$)
> - Cột 2: Chiều dài cánh tay phải ($x_2$)
> 
> Về mặt lưu trữ máy tính, bộ dữ liệu này có 2 chiều (2D). Nhưng hãy thử suy nghĩ bằng trực giác: Cánh tay trái và cánh tay phải của một người bình thường gần như dài y hệt nhau. Biết được độ dài tay trái, ta gần như dự đoán chính xác 100% độ dài tay phải. Hai biến này có **độ tương quan** (*correlation*) vô cùng hoàn hảo.
>
> Nếu vẽ 100 mẫu này lên đồ thị 2D với hai cột lần lượt là *chiều dài tay trái* và *chiều dài tay phải*, các điểm dữ liệu sẽ không nằm rải rác khắp nơi mà xếp thành một đường chéo thẳng tắp. Nghĩa là ở đây ta thực sự không cần đến 2 trục tọa độ ($x_1, x_2$) để lưu thông tin mà chỉ cần 1 trục tọa độ mới chạy dọc theo đường chéo đó, đặt tên là trục "Chiều dài sải tay".

Việc gộp nhiều cột có độ tương quan cao thành 1 hoặc 1 vài trục cốt lõi mà không làm mất đi đặc trưng của dữ liệu chính là bài toán dẫn đến lý do *PCA* ra đời. Với ví dụ trước đó, người ta gọi trục *"Chiều dài sải tay"* là một **Thành phần chính** (*Principal Component*). 

---

## 2. Bản chất (đọc thêm)

Cái hay của PCA nằm ở chỗ nó hợp nhất hai góc nhìn tưởng chừng khác biệt về cùng một bản chất toán học:

1. **Góc nhìn Tối đa hóa Phương sai** (*Maximum Variance Formulation* - Hotelling, 1933): PCA tìm kiếm một không gian con sao cho khi chiếu trực giao dữ liệu lên đó, sự phân tán (phương sai) của dữ liệu là lớn nhất có thể. Tại sao lại là phương sai? Bởi vì phương sai lớn đồng nghĩa với sự phân tán nhiều, lượng thông tin biểu diễn cao (*more variation = more useful information*).
2. **Góc nhìn Tối thiểu hóa Sai số** (*Minimum Error Formulation* - Pearson, 1901): PCA tìm kiếm phép chiếu tuyến tính sao cho trung bình bình phương khoảng cách (sai số tái tạo - *reconstruction error*) từ các điểm dữ liệu gốc đến hình chiếu của chúng trên không gian con là nhỏ nhất.

Bên cạnh đó, PCA còn có một góc nhìn Xác suất sâu sắc được gọi là **PCA Xác suất** (*Probabilistic PCA - PPCA*). Ở góc nhìn này, PCA được mô hình hóa như một **Mô hình biến tiềm ẩn** (*Latent Variable Model*) sinh mẫu tuyến tính - Gauss:
$\mathbf{x} = \mathbf{W}\mathbf{z} + \boldsymbol{\mu} + \boldsymbol{\epsilon}$
Trong đó biến tiềm ẩn $\mathbf{z} \sim \mathcal{N}(\mathbf{0}, \mathbf{I})$ sinh ra dữ liệu quan sát $\mathbf{x}$, cộng thêm nhiễu $\boldsymbol{\epsilon} \sim \mathcal{N}(\mathbf{0}, \sigma^2\mathbf{I})$. PPCA giải quyết nhược điểm không có hàm hợp lý (*likelihood function*) của PCA truyền thống, cho phép xử lý dữ liệu bị thiếu (*missing values*) và so sánh với các mô hình xác suất khác.

---

## 3. Mô hình hóa Toán học & Ràng buộc 

Phần này sẽ trình bày toán học chặt chẽ cho *PCA* dưới góc nhìn *Ma trận dữ liệu*. Cách tiếp cận này giúp ta kiểm soát hoàn hảo chiều không gian và kết nối trực tiếp với lý thuyết Hiệp phương sai.

> [!danger]+ Ràng buộc & Giả định của PCA
> Tuyệt đối phải tuân thủ các giả định sau khi mô hình hóa *PCA*:
> - **Dữ liệu phải được ly sai**: Chuyển ma trận dữ liệu gốc $\mathbf{X}$ thành ma trận ly sai $\mathbf{X}_c$ để các trục chiếu đi qua trọng tâm của đám mây dữ liệu.
> - **Giả định Tuyến tính**: *PCA* chỉ tìm các **tổ hợp tuyến tính** của biến gốc. ***Nó thất bại hoàn toàn trên bộ dữ liệu có sự kết hợp phi tuyến phức tạp như $Y = X^2$ hoặc hơn thế.***

### 3.1. Phép chiếu trong Đại số tuyến tính

Trước khi đi vào quy mô ma trận, ta cần xây dựng trực giác từ không gian nhỏ nhất: chiếu một điểm dữ liệu đơn lẻ. 

Giả sử ta có một điểm dữ liệu biểu diễn dưới dạng vector cột $\mathbf{x}$ và một trục tọa độ mới được định nghĩa bởi một **vector đơn vị** $\mathbf{u}$ (với điều kiện độ dài $\|\mathbf{u}\| = 1$). Theo định nghĩa của giải tích thông thường, **tích vô hướng** (*dot product*) giữa hai vector này được tính bằng:

> [!info]+ Trực giác Phép chiếu 1 điểm
> $$\mathbf{u}^T \mathbf{x} = \|\mathbf{u}\| \|\mathbf{x}\| \cos(\theta)$$
> Trong đó $\theta$ là góc hợp bởi vector $\mathbf{x}$ và trục $\mathbf{u}$. Vì $\mathbf{u}$ là vector đơn vị ($\|\mathbf{u}\| = 1$), phương trình được triệt tiêu thành:
> $$\mathbf{u}^T \mathbf{x} = \|\mathbf{x}\| \cos(\theta)$$

Về mặt hình học lượng giác, $\|\mathbf{x}\| \cos(\theta)$ chính xác là cạnh kề của một tam giác vuông tạo bởi điểm $\mathbf{x}$ khi chiếu $\mathbf{x}$ vuông góc xuống trục $\mathbf{u}$. 

Do đó, tích vô hướng $\mathbf{u}^T \mathbf{x}$ (hay $\mathbf{x}^T \mathbf{u}$) sinh ra một giá trị vô hướng. Giá trị này mang ý nghĩa hình học cực kỳ quan trọng: nó là độ dài từ gốc tọa độ đến điểm đã chiếu xuống trục. Hay nói cách khác, **đó chính là tọa độ mới của $\mathbf{x}$ trên trục $\mathbf{u}$**.

Từ trực giác cốt lõi đó, ta mở rộng quy mô cho toàn bộ tập dữ liệu. Giả sử ta có bộ dữ liệu gồm $n$ quan sát và $p$ đặc trưng (*Lưu ý rằng trong **học máy** người ta thường dùng $N$ (Number of samples) thay cho n và $D$ (Dimensionality) thay cho p*), biểu diễn dưới dạng ma trận ly sai $\mathbf{X}_c$ kích thước $n \times p$ (*Xem lại [[Statistics_Covariance#3.2. Ma trận Hiệp phương sai|Ma trận hiệp phương sai]] nếu chưa hiểu $\mathbf{X}_{c}$*). Ở đây, mỗi hàng của ma trận $\mathbf{X}_c$  chính là một điểm dữ liệu nằm ngang dạng $\mathbf{x}_i^T$.

Để chiếu toàn bộ $n$ điểm này lên trục $\mathbf{u}$ (kích thước $p \times 1$), ta gom tất cả các tích vô hướng riêng lẻ lại thông qua một phép nhân ma trận đồng loạt:

> [!info]+ Phép chiếu trực giao 
> $$\mathbf{z} = \mathbf{X}_c \mathbf{u}$$

- **Về mặt kích thước:** $(n \times p) \times (p \times 1) \implies n \times 1$.
- **Về mặt ý nghĩa:** Kết quả $\mathbf{z}$ là một vector cột chứa chính xác $i$ giá trị vô hướng. Mỗi giá trị $z_i$ chính là tọa độ mới của điểm dữ liệu thứ $i$ chiếu xuống trục $\mathbf{u}$.

### 3.2. Phương sai trên trục mới

Mục tiêu cốt lõi của *PCA* là tìm hướng $\mathbf{u}$ sao cho sự phân tán (phương sai) của dữ liệu sau khi chiếu lên $\mathbf{u}$ là lớn nhất.

Vì ma trận gốc $\mathbf{X}_c$ đã được ly sai (trung bình các cột bằng 0), vector tọa độ hình chiếu $\mathbf{z}$ cũng sẽ có giá trị trung bình bằng 0. Khi đó, theo đúng định nghĩa thống kê, **Phương sai mẫu** của tập dữ liệu sau khi chiếu trên trục $\mathbf{u}$ là:
$$\operatorname{Var}(\mathbf{u}) = \frac{1}{n-1} \sum_{i=1}^n (z_i - 0)^2 = \frac{1}{n-1} \mathbf{z}^T \mathbf{z}$$

Bây giờ, ta thế $\mathbf{z} = \mathbf{X}_c \mathbf{u}$ vào công thức phương sai:
$$\operatorname{Var}(\mathbf{u}) = \frac{1}{n-1} (\mathbf{X}_c \mathbf{u})^T (\mathbf{X}_c \mathbf{u})$$

Sử dụng tính chất chuyển vị ma trận $(\mathbf{A}\mathbf{B})^T = \mathbf{B}^T\mathbf{A}^T$:
$$\operatorname{Var}(\mathbf{u}) = \frac{1}{n-1} \mathbf{u}^T \mathbf{X}_c^T \mathbf{X}_c \mathbf{u}$$

Vì $\mathbf{u}$ là vector chỉ hướng cố định, ta có thể nhóm phần dữ liệu lại với nhau:
$$\operatorname{Var}(\mathbf{u}) = \mathbf{u}^T \left( \frac{1}{n-1} \mathbf{X}_c^T \mathbf{X}_c \right) \mathbf{u}$$

Thật kỳ diệu, đại lượng nằm trong ngoặc $\frac{1}{n-1} \mathbf{X}_c^T \mathbf{X}_c$ chính xác là **Ma trận Hiệp phương sai mẫu** $\mathbf{S}$ của bộ dữ liệu gốc! Do đó, ta thu được phương trình hàm mục tiêu của *PCA*:

> [!note]+ Phương trình Phương sai chiếu
> $$\operatorname{Var}(\mathbf{u}) = \mathbf{u}^T \mathbf{S} \mathbf{u}$$
> *(Trong đó $\mathbf{S}$ là ma trận hiệp phương sai kích thước $p \times p$).*

### 3.3. Bài toán Tối ưu hóa 

> [!abstract] Bản chất của quá trình giải
> Trong thực tế tính toán, máy tính không đi tìm từng trục một cách thủ công. Bằng cách giải một phương trình duy nhất ở **3.3.1** và **3.3.2**, ta sẽ thu được toàn bộ Trị riêng và Vector riêng cùng một lúc. 
> **3.3.3** được đề cập chỉ mang tính chất chứng minh toán học để giải thích lý do tại sao những nghiệm dư ra ở **3.3.1** và **3.3.2** lại hoàn toàn hợp lệ để làm các trục *PC2, PC3* tiếp theo mà không vi phạm tính trực giao.

#### 3.3.1 Lập hàm mục tiêu và Tính toán toàn bộ Trị riêng

Ta cần tối đa hóa phương sai chiếu $V(\mathbf{u}_1) = \mathbf{u}_1^T mathbf{S} \mathbf{u}_1$ dưới ràng buộc độ dài vector chỉ hướng phải bằng 1 ($\mathbf{u}_1^T \mathbf{u}_1 = 1$). Ta thiết lập **Hàm Lagrangian**  $\tilde{J}_1$ với nhân tử Lagrange $\lambda_1$:

$$\tilde{J}_1 = \mathbf{u}_1^T \mathbf{S} \mathbf{u}_1 + \lambda_1(1 - \mathbf{u}_1^T \mathbf{u}_1)$$

Lấy đạo hàm riêng của $\tilde{J}_1$ theo vector $\mathbf{u}_1$ và cho bằng vector $\mathbf{0}$:

$$\frac{\partial \tilde{J}_1}{\partial \mathbf{u}_1} = 2\mathbf{S}\mathbf{u}_1 - 2\lambda_1\mathbf{u}_1 = \mathbf{0} \implies \mathbf{S}\mathbf{u}_1 = \lambda_1\mathbf{u}_1$$

> [!info]+ Phương trình Đặc trưng 
> Để phương trình $\mathbf{S}\mathbf{u}_1 = \lambda_1\mathbf{u}_1$ có nghiệm không tầm thường, định thức của ma trận hệ số phải bằng 0:
> $$\operatorname{det}(\mathbf{S} - \lambda\mathbf{I}) = 0$$
> Cái hay ở đây là với ma trận hiệp phương sai $\mathbf{S}$ kích thước $p \times p$, phương trình định thức này là một đa thức bậc $p$. Khi giải nó, ta không chỉ tìm được một $\lambda$ duy nhất, mà sẽ thu được toàn bộ $p$ nghiệm **Trị riêng** ($\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_p$) cùng một lúc!

Trị riêng lớn nhất $\lambda_1$ chính là lượng phương sai lớn nhất mà trục *PC1* có thể giữ lại.

#### 3.3.2 Tìm Vector riêng từ Trị riêng tương ứng

Chỉ có lượng phương sai ($\lambda$) thì chưa đủ để vẽ trục, ta cần hướng của trục đó trong không gian gốc. Hướng này chính là các **Vector riêng** (*Eigenvectors*).

Với mỗi một Trị riêng $\lambda_j$ vừa tìm được ở **3.3.1**, ta thế ngược nó lại vào hệ phương trình tuyến tính thuần nhất:

$$(\mathbf{S} - \lambda_j\mathbf{I})\mathbf{u}_j = \mathbf{0}$$

Giải hệ phương trình này, ta sẽ tìm được tọa độ của vector $\mathbf{u}_j$. Sau đó, ta chuẩn hóa nó về độ dài đơn vị:

$$\mathbf{u}_j = \frac{\mathbf{u}_j}{\|\mathbf{u}_j\|_2}$$

Cứ làm tương tự với $p$ Trị riêng, ta sẽ thu được một tập hợp gồm $p$ Vector riêng ($\mathbf{u}_1, \mathbf{u}_2, \dots, \mathbf{u}_p$). Tập hợp các vector này chính là nguồn nguyên liệu để ta thành lập Ma trận chuyển đổi ở **Mục 3.4**.

#### 3.3.3 Tại sao ta được quyền lấy các trị riêng tiếp theo? *(đọc thêm)*

**Câu hỏi đặt ra:** Ta đã có sẵn $\lambda_2, \lambda_3$ và các vector $\mathbf{u}_2, \mathbf{u}_3$ nằm chờ sẵn từ **3.3.1** và **3.3.2** Nhưng liệu việc tùy tiện lấy $\mathbf{u}_2$ làm trục Thành phần chính thứ hai (*PC2*) thì có thỏa mãn được ràng buộc "phải vuông góc với *PC1*" không?

Để chứng minh, ta thiết lập bài toán tìm trục $\mathbf{u}_2$ với hai ràng buộc:
- **Ràng buộc độ dài đơn vị:** $\mathbf{u}_2^T \mathbf{u}_2 = 1$.
- **Ràng buộc trực giao:** Trục mới phải vuông góc với trục cũ, tức là $\mathbf{u}_2^T \mathbf{u}_1 = 0$.

Lập hàm Lagrangian $\tilde{J}_2$ chứa 2 nhân tử Lagrange ($\lambda_2$ và $\phi$):

$$\tilde{J}_2 = \mathbf{u}_2^T \mathbf{S} \mathbf{u}_2 + \lambda_2(1 - \mathbf{u}_2^T \mathbf{u}_2) - \phi(\mathbf{u}_2^T \mathbf{u}_1)$$

Lấy đạo hàm theo $\mathbf{u}_2$ và cho bằng $\mathbf{0}$:

$$\frac{\partial \tilde{J}_2}{\partial \mathbf{u}_2} = 2\mathbf{S}\mathbf{u}_2 - 2\lambda_2\mathbf{u}_2 - \phi\mathbf{u}_1 = \mathbf{0}$$

Nhân vô hướng $\mathbf{u}_1^T$ vào bên trái toàn bộ phương trình:

$$2\mathbf{u}_1^T\mathbf{S}\mathbf{u}_2 - 2\lambda_2\mathbf{u}_1^T\mathbf{u}_2 - \phi\mathbf{u}_1^T\mathbf{u}_1 = 0$$

Áp dụng các ràng buộc:
- Do trực giao: $\mathbf{u}_1^T\mathbf{u}_2 = 0$.
- Do độ dài đơn vị: $\mathbf{u}_1^T\mathbf{u}_1 = 1$.
- Vì $\mathbf{S}$ đối xứng ($\mathbf{S}^T = \mathbf{S}$) và tính chất *PC1*: $\mathbf{u}_1^T\mathbf{S}\mathbf{u}_2 = (\mathbf{S}\mathbf{u}_1)^T\mathbf{u}_2 = \lambda_1(\mathbf{u}_1^T\mathbf{u}_2) = 0$.

Phương trình triệt tiêu hoàn toàn thành:

$$0 - 0 - \phi(1) = 0 \implies \phi = 0$$

> [!note]+ Kết luận Toán học Quy nạp
> Khi $\phi = 0$, ràng buộc trực giao bị triệt tiêu khỏi phương trình đạo hàm. Phương trình sụp đổ về lại dạng cơ bản:
> $$\mathbf{S}\mathbf{u}_2 = \lambda_2\mathbf{u}_2$$
> Việc thiết lập bài toán tìm một trục mới vuông góc với trục cũ thực chất hoàn toàn tương đương với việc lấy trực tiếp Trị riêng và Vector riêng tiếp theo đã được giải sẵn ở Bước 1 và Bước 2. Tính trực giao đã được toán học tự động bảo đảm!

### 3.4. Ma trận Chuyển đổi 

Sau khi giải quyết xong bài toán tối ưu bằng quy nạp toán học ở Mục 3.3, ta đã có trong tay tập hợp $p$ vector riêng $\mathbf{u}_j$ xếp tương ứng với $p$ trị riêng $\lambda_j$ giảm dần. Giờ là lúc thực hiện bước cuối cùng của thuật toán **Phân tích Thành phần chính** (*PCA*): nén toàn bộ tập dữ liệu.

#### Bước 1: Sắp xếp và Lựa chọn số chiều mong muốn 

Mỗi trị riêng $\lambda_j$ đại diện cho lượng phương sai (lượng thông tin) mà trục đặc trưng đó nắm giữ. 

- **Sắp xếp:** Ta tiến hành sắp xếp các vector riêng $\mathbf{u}_i$ theo thứ tự trị riêng $\lambda_i$ giảm dần: $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_p$. Trục ứng với $\lambda_1$ giữ nhiều thông tin nhất được gọi là **Thành phần chính thứ nhất** (*1st Principal Component - PC1*), trục tiếp theo là PC2, PC3,...
- **Chọn lọc:** Thay vì giữ lại toàn bộ $p$ chiều, ta chỉ chọn ra $k$ vector đầu tiên ($k < p$) sao cho tổng lượng phương sai tích lũy chiếm đại đa số thông tin (ví dụ: giữ lại 95% phương sai của toàn bộ dữ liệu ban đầu).

> [!note]+ Ma trận Chuyển đổi Không gian con ($\mathbf{U}_k$)
> Ta gộp $k$ vector đơn vị đã chọn lọc lại với nhau theo hàng dọc để thành lập một **Ma trận chuyển đổi** $\mathbf{U}_k$ có kích thước $p \times k$:
> $$\mathbf{U}_k = \begin{bmatrix} | & | & & | \\ \mathbf{u}_1 & \mathbf{u}_2 & \dots & \mathbf{u}_k \\ | & | & & | \end{bmatrix}$$

#### Bước 2: Chiếu dữ liệu ly sai sang không gian con mới

Để nén tập dữ liệu, ta mang toàn bộ ma trận dữ liệu ly sai gốc $\mathbf{X}_c$ (kích thước $n \times p$) nhân trực tiếp với ma trận chuyển đổi $\mathbf{U}_k$ vừa thiết lập.

> [!info]+ Phương trình nén giảm chiều dữ liệu
> Ma trận dữ liệu nén $\mathbf{Z}$ trong không gian con mới được tính toán đồng loạt bằng một phép nhân ma trận trực giao:
> $$\mathbf{Z} = \mathbf{X}_c \mathbf{U}_k$$

**Kiểm tra chiều không gian (Dimension Check):**
$$\mathbf{Z} = (n \times p) \times (p \times k) \implies \mathbf{(n \times k)}$$

Tới đây là xong! Vậy là từ ma trận dữ liệu có $p$ cột đặc trưng ban đầu, ta đã ép nó xuống thành ma trận $\mathbf{Z}$ chỉ còn $k$ cột (với $k < p$ ban đầu). Mỗi hàng trong ma trận $\mathbf{Z}$ chính là tập hợp các tọa độ mới của điểm dữ liệu tương ứng khi biểu diễn trên hệ trục tọa độ nén mới.

---


## 4. Bài tập tính tay 
> [!example]+ Ví dụ: Tính tay PCA
> Giả sử ta có 3 điểm dữ liệu 2D biểu diễn 1 đường thẳng hoàn hảo (tương quan cực mạnh): $\mathbf{x}_1 = \begin{bmatrix} 1 \\ 2 \end{bmatrix}$, $\mathbf{x}_2 = \begin{bmatrix} 3 \\ 4 \end{bmatrix}$, $\mathbf{x}_3 = \begin{bmatrix} 5 \\ 6 \end{bmatrix}$. Khi đó bộ dữ liệu được biểu diễn: $$\mathbf{X} = \begin{bmatrix} \mathbf{x}_1^T \\ \mathbf{x}_{2}^T \\ \mathbf{x}_{3}^T \end{bmatrix} = \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{bmatrix}$$
>
> **Bước 1: Tính trung bình và Ly sai**
> $\mathbf{\bar{x}} = \begin{bmatrix} \frac{1+3+5}{3} \\ \frac{2+4+6}{3} \end{bmatrix} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}$
> Ma trận ly sai: $\mathbf{X_{c}} = \begin{bmatrix} 1-3 & 2-4 \\ 3-3 & 4-4 \\ 5-3 & 6-4 \end{bmatrix} = \begin{bmatrix} -2 & -2 \\ 0 & 0 \\ 2 & 2 \end{bmatrix}$
>
>**Bước 2: Tính Ma trận Hiệp phương sai $\mathbf{S}$**
>Lấy ước lượng theo $n-1=2$:
>$$\mathbf{S} = \frac{1}{2} \mathbf{X}_{c}^T \mathbf{X}_{c} = \frac{1}{2} \begin{bmatrix} -2 & 0 & 2 \\ -2 & 0 & 2 \end{bmatrix} \begin{bmatrix} -2 & -2 \\ 0 & 0 \\ 2 & 2 \end{bmatrix} = \frac{1}{2} \begin{bmatrix} 8 & 8 \\ 8 & 8 \end{bmatrix} = \begin{bmatrix} 4 & 4 \\ 4 & 4 \end{bmatrix}$$
>**Bước 3: Tìm Trị riêng $\lambda$ và Vector riêng $\mathbf{u}$**
>Giải phương trình đặc trưng $\det(\mathbf{S} - \lambda\mathbf{I}) = 0$:
$$\left(4 - \lambda\right)^2 - 4^2 = 0 \implies \lambda^2 - 8\lambda = 0$$
>Ta có $\lambda_1 = 8$ và $\lambda_2 = 0$. (Toàn bộ phương sai dồn vào PC1, PC2 không chứa thông tin do các điểm thẳng hàng).
>Với $\lambda_1 = 8$, thế vào $\mathbf{S}\mathbf{u}_1 = \lambda_1\mathbf{u}_1$:
$$4u_1 + 4u_2 = 8u_1 \implies u_1 = u_2$$
>Chuẩn hóa vector độ dài 1 ($\mathbf{u}_1^T \mathbf{u}_1 = 1$): $\mathbf{u}_1 = \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix}$
>**Bước 4: Chiếu dữ liệu xuống 1D (PC1)**
>$$\mathbf{Z} = \mathbf{X}_{c} \mathbf{u}_1 = \begin{bmatrix} -2 & -2 \\ 0 & 0 \\ 2 & 2 \end{bmatrix} \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} -2\sqrt{2} \\ 0 \\ 2\sqrt{2} \end{bmatrix}$$
>Không gian 2D gốc đã bị ép xuống thành 1 trục hoành duy nhất mà bảo toàn 100% phương sai.
### 4.2. Bài tập luyện thêm
> [!example]+ Bài tập làm thêm 1: Tối đa hóa Phương sai 
> **Đề bài:** Bằng phương pháp quy nạp toán học, hãy chứng minh rằng phép chiếu tuyến tính (*linear projection*) xuống không gian $M$ chiều giúp tối đa hóa phương sai của dữ liệu chiếu chính là phép chiếu lên $M$ vector riêng (*eigenvectors*) của ma trận Hiệp phương sai $\mathbf{S}$ ứng với $M$ trị riêng (*eigenvalues*) lớn nhất.
> 
> **Lời giải:**
> - **Trường hợp $M=1$:** Phương sai chiếu là $\mathbf{u}_1^T \mathbf{S} \mathbf{u}_1$. Ta cần cực đại hóa hàm này dưới ràng buộc độ dài $\mathbf{u}_1^T \mathbf{u}_1 = 1$. Lập hàm Lagrange: 
>   $$J_1 = \mathbf{u}_1^T \mathbf{S} \mathbf{u}_1 + \lambda_1(1 - \mathbf{u}_1^T \mathbf{u}_1)$$
>   Lấy đạo hàm theo $\mathbf{u}_1$ và cho bằng $\mathbf{0}$, ta có $\mathbf{S}\mathbf{u}_1 = \lambda_1\mathbf{u}_1$. Nghĩa là $\mathbf{u}_1$ phải là vector riêng của $\mathbf{S}$. Phương sai đạt được chính là $\lambda_1$, nên ta chọn $\lambda_1$ lớn nhất.
> - **Giả sử đúng tới $M$:** Đã chọn được $M$ vector riêng lớn nhất $\mathbf{u}_1, \dots, \mathbf{u}_M$.
> - **Trường hợp $M+1$:** Ta cần tối đa hóa $\mathbf{u}_{M+1}^T \mathbf{S} \mathbf{u}_{M+1}$ dưới ràng buộc $\mathbf{u}_{M+1}^T \mathbf{u}_{M+1} = 1$ và $\mathbf{u}_{M+1}$ phải trực giao với các vector trước đó ($\mathbf{u}_{M+1}^T \mathbf{u}_i = 0$). Dùng nhân tử Lagrange để giải quyết các ràng buộc này, tương tự ta sẽ thu được phương trình $\mathbf{S}\mathbf{u}_{M+1} = \lambda_{M+1}\mathbf{u}_{M+1}$.

> [!example]+ Bài tập làm thêm 2: Tối thiểu hóa Sai số 
> **Đề bài:** Andrew Ng có đề cập trong Problem Set 4 và Bishop đưa ra bài tập 12.2: "Hãy chứng minh rằng cực tiểu hóa độ đo sai số tái tạo (*reconstruction error*) $J = \sum_{i=M+1}^{D} \mathbf{u}_i^T \mathbf{S} \mathbf{u}_i$ dưới ràng buộc trực chuẩn sẽ thu được nghiệm $\mathbf{u}_i$ là các vector riêng của $\mathbf{S}$".
> 
> **Lời giải:**
> Ta cần tối thiểu hóa phần phương sai bị vứt bỏ trên các trục $i = M+1 \dots D$. Xét ví dụ cực tiểu hóa một hướng bị vứt bỏ $\mathbf{u}_2$ (khi $M=1, D=2$). Ta tối thiểu hóa $J = \mathbf{u}_2^T \mathbf{S} \mathbf{u}_2$ với ràng buộc $\mathbf{u}_2^T \mathbf{u}_2 = 1$. Lập hàm Lagrange: 
> $$\tilde{J} = \mathbf{u}_2^T \mathbf{S} \mathbf{u}_2 + \lambda_2(1 - \mathbf{u}_2^T \mathbf{u}_2)$$
> Lấy đạo hàm theo $\mathbf{u}_2$ cho bằng $\mathbf{0}$, ta có $\mathbf{S}\mathbf{u}_2 = \lambda_2\mathbf{u}_2$. Giá trị sai số đạt cực tiểu khi $J = \lambda_2$. Do đó, để sai số nhỏ nhất, ta phải vứt bỏ vector riêng ứng với trị riêng nhỏ nhất. Nghĩa là, ta giữ lại các vector riêng ứng với trị riêng lớn nhất.

> [!example]+ Bài tập làm thêm 3: Sự liên hệ giữa PCA và thuật toán EM 
> **Đề bài:** Đặt bài toán xấp xỉ dữ liệu bằng một hàm tuyến tính $\mathbf{W}\mathbf{z}_n + \boldsymbol{\mu}$. Ta cần cực tiểu hóa hàm chi phí tái tạo $J = \sum_{n=1}^{N} \|\mathbf{x}_n - \boldsymbol{\mu} - \mathbf{W}\mathbf{z}_n\|^2$. Hãy chứng minh rằng việc cực tiểu hóa luân phiên (*Alternating Minimization*) hàm $J$ này sẽ dẫn đến các bước tương đương với thuật toán *Expectation-Maximization* (*EM*) cho *PCA*.
> 
> **Lời giải:**
> - Tối thiểu hóa $J$ theo $\boldsymbol{\mu}$ cho ra $\boldsymbol{\mu} = \bar{\mathbf{x}}$ (trung bình dữ liệu). Từ đó ta có thể chuyển sang dùng dữ liệu đã ly sai $\tilde{\mathbf{x}}_n = \mathbf{x}_n - \bar{\mathbf{x}}$.
> - **Tương đương *E-step*:** Giữ cố định ma trận không gian con $\mathbf{W}$, cực tiểu hóa $J$ theo biến tiềm ẩn $\mathbf{z}_n$. Bằng cách lấy đạo hàm, ta thu được phép chiếu trực giao: 
>   $$\mathbf{z}_n = (\mathbf{W}^T \mathbf{W})^{-1} \mathbf{W}^T \tilde{\mathbf{x}}_n$$
> - **Tương đương *M-step*:** Giữ cố định tọa độ chiếu $\mathbf{z}_n$, cực tiểu hóa $J$ theo ma trận $\mathbf{W}$. Đây là một bài toán hồi quy tuyến tính nhiều biến, cho ra nghiệm: 
>   $$\mathbf{W}_{new} = \tilde{\mathbf{X}}^T \mathbf{Z} (\mathbf{Z}^T \mathbf{Z})^{-1}$$
> 
> Việc lặp lại liên tục *E-step* và *M-step* này cho phép tìm ra không gian *PCA* trong các bài toán có số chiều $D$ cực kỳ lớn mà không cần tính trực tiếp ma trận Hiệp phương sai $\mathbf{S}$.

---

## 5. Triển khai Code

Phần này sẽ hiện thực hóa toàn bộ các phương trình toán học ở Mục 3 thành mã nguồn thực tế. Ta sẽ bắt đầu bằng việc tự xây dựng *PCA* từ from scratch bằng `pytorch` để hiểu rõ luồng di chuyển của các ma trận, sau đó sử dụng các thư viện học máy tiêu chuẩn như `scikit-learn` để phục vụ cho các dự án thực tế.

> [!example]+ Triển khai PCA from scratch bằng PyTorch
> 
> ```python
> import torch
> 
> # 1. Tạo: 5 quan sát, 2 biến (2D)
> # Đẩy thẳng tensor lên GPU (nếu khả dụng)
> device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
> X = torch.tensor([
>     [2.5, 2.4],
>     [0.5, 0.7],
>     [2.2, 2.9],
>     [1.9, 2.2],
>     [3.1, 3.0]
> ], dtype=torch.float32, device=device)
> 
> n_samples = X.shape[0]
> 
> # Bước 1: Ly sai dữ liệu (Mean-centering)
> # broadcast vector mean cho toàn bộ ma trận
> X_mean = torch.mean(X, dim=0)
> X_c = X - X_mean
> 
> # Bước 2: Tính Covariance Matrix
> # Dùng tích vô hướng ma trận thay vì vòng lặp
> S = (X_c.T @ X_c) / (n_samples - 1)
> 
> # Bước 3: Phân rã Trị riêng & Vector riêng
> # Sử dụng eigh vì Sigma luôn là ma trận đối xứng 
> eigenvalues, eigenvectors = torch.linalg.eigh(Sigma)
> 
> # Hàm eigh trả về trị riêng tăng dần, ta cần sắp xếp giảm dần (PC1, PC2...)
> idx = torch.argsort(eigenvalues, descending=True)
> eigenvalues = eigenvalues[idx]
> eigenvectors = eigenvectors[:, idx]
> 
> # Bước 4: Chiếu dữ liệu xuống không gian mới 
> # Z = X_c * U
> Z = X_c @ eigenvectors
> 
> print("Ma trận Hiệp phương sai (Sigma):\n", Sigma)
> print("\nVector riêng (Eigenvectors - Các trục PC):\n", eigenvectors)
> print("\nTọa độ dữ liệu trên không gian PCA (Z):\n", Z)
> ```

> [!example]+ So sánh với thư viện Học máy Scikit-learn
> Trong môi trường *Production*, ta không cần phải tự phân rã trị riêng mà sẽ gọi trực tiếp lớp `PCA` từ `scikit-learn`. Thuật toán cốt lõi bên dưới của `scikit-learn` thường dùng phân rã SVD (*Singular Value Decomposition*) để tối ưu độ ổn định số học, nhưng bản chất hình học vẫn hoàn toàn trùng khớp.
> 
> ```python
> from sklearn.decomposition import PCA
> import numpy as np
> 
> # Chuyển tensor từ PyTorch CPU về NumPy
> X_np = X.cpu().numpy()
> 
> # Khởi tạo và fit mô hình PCA
> pca = PCA(n_components=2)
> Z_sklearn = pca.fit_transform(X_np)
> 
> print("Tỷ lệ phương sai được giải thích (Explained Variance Ratio):")
> print(pca.explained_variance_ratio_) 
> # Đầu ra sẽ cho thấy PC1 nắm giữ >95% lượng thông tin (phương sai)
> ```


---

## 6. Những đánh đổi & Ứng dụng Thực tế

**Những đánh đổi:**
*   **Mất đi tính diễn dịch trực tiếp**: Các trục mới (PC1, PC2) là sự kết hợp tuyến tính của *tất cả* các biến ban đầu, khiến việc giải thích ý nghĩa kinh tế học / vật lý của từng trục trở nên cực kỳ khó khăn.
*   **Giới hạn phi tuyến** : PCA thuần túy sử dụng biến đổi tuyến tính, nó sẽ thất bại trước các tập dữ liệu có cấu trúc phi tuyến phức tạp. Để vượt qua giới hạn này, phải sử dụng *Kernel PCA*, hay các kỹ thuật *Manifold Learning* (như t-SNE, UMAP).

**3 Ứng dụng Thực tế:**
1. **Computer Vision & Pattern Recognition:** PCA ứng dụng mạnh mẽ trong nhận dạng khuôn mặt (Face Recognition). Thay vì lưu trữ hàng nghìn pixel, hình ảnh khuôn mặt được chiếu lên một không gian nhỏ hơn chứa các *Eigenfaces* giúp nén ảnh và giảm chi phí tính toán mà không mất các đặc điểm nhận dạng cốt lõi.
2. **Signal Processing - Independent Component Analysis (ICA):** Trong phân tích tín hiệu, ICA thường dùng PCA hoặc SVD làm bước tiền xử lý  để làm trắng dữ liệu, giúp loại bỏ sự tương quan chéo giữa các biến trước khi tiến hành tách các thành phần độc lập (Ví dụ: bài toán Cocktail Party Problem).
3. **Data Science - Tiền xử lý dữ liệu:** PCA hoạt động như một bộ lọc giảm nhiễu. Bằng cách vứt bỏ các trục có phương sai quá nhỏ (xem như nhiễu), PCA giúp giải quyết *Curse of Dimensionality*, cải thiện đáng kể tốc độ hội tụ và tránh overfitting cho các mô hình Machine Learning cho các *downstream task*.

## 7. Câu hỏi thường gặp
> [!faq]- Vậy làm sao biết chọn bao nhiêu $\lambda$ là đủ ?

---

🔗 [[MOC_Data_Mining]], [[MOC_Statistics]], [[MOC_Linear_Algebra]], [[MOC_Probability]]


