---
aliases:
  - Covariance
  - Hiệp phương sai
  - Covariance Matrix
---

# Covariance - Hiệp Phương Sai - Ma trận Hiệp Phương Sai

> [!abstract]+ Ý nghĩa thuật ngữ
> Thuật ngữ **Covariance** = **"Co-"** (Cùng nhau / hiệp) + **"Variance"** (Phương sai). Trong tiếng Việt là **Hiệp phương sai** đo lường sự "hiệp lực" trong cách mà hai biến số cùng rời xa vị trí cân bằng của chúng. Nghe hơi mơ hồ, mời bạn xem tiếp bài viết dưới đây! 

---

## 1. Trực giác về Covariance trong Thống kê


> [!abstract]+ Giới thiệu
> Phần này sẽ xây dựng trực giác hình học và thống kê về **Hiệp phương sai** (*Covariance*). Ta sẽ đi từ sự suy biến của dữ liệu 1 chiều (1D) khi giải thích không gian đa chiều, từ đó đưa ra giải pháp chia góc phần tư để "cân đo đong đếm" mối quan hệ tương hỗ giữa các biến.

### 1.1. Bắt đầu ở không gian đơn giản nhất - 1 Chiều (1D)

Giả sử ta đi thu thập dữ liệu về Chiều cao của 100 người. Khi biểu diễn trên trục số, tất cả các điểm dữ liệu chỉ nằm dọc theo một đường thẳng duy nhất.

![[Pasted image 20260516160825.png]]

> [!note]+ Phương sai mẫu
> Lúc này, bằng cách tính trung bình bình phương độ lệch thông qua **Phương sai mẫu** (*Sample Variance*): 
> $$S_X^2 = \frac{1}{n-1}\sum_{i=1}^{n} (x_i - \bar{x})^2$$
> Ta dễ dàng biết được dữ liệu đang phân bố tập trung hay phân tán rộng ra xung quanh giá trị trung bình $\bar{x}$. 

### 1.2. Với dữ liệu nhiều chiều 

Vấn đề là bộ dữ liệu của ta hiếm khi chỉ có một biến. Nếu ta đo thêm biến Cân nặng của 100 người đó, bộ dữ liệu lập tức trở thành 2 chiều. Hãy nhìn vào phân phối dưới đây:

![[Pasted image 20260516160746.png]]

Phản xạ của ta là ngay lập tức tính toán các thống kê cơ bản như trung bình, phương sai của từng biến trong bộ dữ liệu và nghĩ: *"OK, cuối cùng cũng tính xong phương sai cho Chiều cao và Cân nặng rồi... Thế giờ làm gì nữa?!?"* 

Việc chỉ nhìn vào phương sai đơn lẻ khiến ta vô tình bỏ lỡ yếu tố vô cùng quan trọng của dữ liệu đa chiều: **Mối quan hệ qua lại giữa chúng**. Đó cũng chính là vấn đề mà các nhà khoa học dữ liệu đời đầu gặp phải. Họ cần một công cụ mới đo lường được sự tương tác này.

### 1.3. Giải pháp -  Chia không gian 2 biến bằng 4 Góc phần tư

Để đo sự liên quan giữa hai biến ngẫu nhiên, các nhà toán học đã vẽ hai đường thẳng biểu diễn giá trị trung bình $\bar{x}$ và $\bar{y}$ cắt ngang đồ thị, chia không gian thành 4 góc phần tư:

![[Pasted image 20260516160802.png]]


Lúc này họ tô màu xanh lá cho góc phần tư thứ 1 và 3, màu đỏ cho 2 và 4. Bấy giờ, họ có nhận xét rằng:
- **Vùng Xanh lá**: Là nơi chứa các điểm dữ liệu mà cả hai biến đều cùng lớn hơn hoặc cùng bé hơn giá trị trung bình. Lúc này, tích khoảng cách $(x_i - \bar{x})(y_i - \bar{y})$ mang dấu dương ($>0$).
- **Vùng Đỏ**: Là nơi chứa các điểm mà biến này lớn hơn trung bình, nhưng biến kia lại bé hơn trung bình. Lúc này, tích khoảng cách $(x_i - \bar{x})(y_i - \bar{y})$ mang dấu âm ($<0$).

Bằng mắt thường, ta thấy dữ liệu tập trung ở Vùng Xanh nhiều hơn hẳn Vùng màu đỏ. Với ý tưởng đó, họ tiến hành tính toán tích khoảng cách của toàn bộ các điểm dữ liệu và cộng dồn tất cả chúng lại, chia cho số lượng quan sát để lấy trung bình.

> [!info]+ Hiệp phương sai mẫu (Lý thuyết thống kê)
> Đại lượng sinh ra từ phép toán đó chính là **Hiệp phương sai mẫu** (*Sample Covariance*), ký hiệu là $S_{XY}$:
> $$S_{XY} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})$$
> *(Về bản chất xác suất của khái niệm này sẽ được trình bày ở một mục khác, ở đây ta chỉ quan tâm đến góc nhìn thống kê).*

### 1.4. Ý nghĩa sinh ra từ con số Covariance

Trực giác từ phép cộng dồn các góc phần tư cho ta 3 trường hợp có thể xảy ra đối với đại lượng *Covariance*:

- **Covariance dương mạnh ($>0$)**: Số điểm ở các vùng màu xanh chiếm đại đa số làm các tích số dương áp đảo. Cặp biến ngẫu nhiên $X$ và $Y$ có xu hướng tăng cùng nhau ($X$ lớn hơn trung bình thì $Y$ cũng lớn hơn trung bình, và ngược lại).
- **Covariance âm mạnh ($<0$)**: Ngược lại với trường hợp trên, số điểm màu đỏ chiếm đại đa số làm các tích số âm chiếm áp đảo. Cặp biến ngẫu nhiên $X$ và $Y$ có xu hướng giảm cùng nhau ($X$ lớn hơn trung bình thì $Y$ lại bé hơn trung bình hoặc ngược lại).
- **Covariance xấp xỉ $0$**: Dữ liệu phân bố đều đặn ở cả 4 góc phần tư, các tích số âm dương triệt tiêu lẫn nhau. 

> [!danger]+ Sai lầm
> Khi *Covariance* xấp xỉ $0$, ***tuyệt đối không được vội kết luận hai biến độc lập với nhau***. Điều này chỉ có nghĩa là ***không có xu hướng TUYẾN TÍNH nào rõ rệt*** giữa chúng.

---
## 2. Cơ sở lý thuyết trong gian Xác suất (đọc thêm)

 Để hiểu sâu hơn, ta cần xem xét bản chất lý thuyết của *Covariance*, trong Lý thuyết Xác Suất. Lúc này ta không làm việc với các giá trị ngẫu nhiên mà phải xem xét trên một **không gian xác suất** $(\Omega, \mathscr{M}, P)$. Ở đây $X$ và $Y$ được xem là thành phần của một **vector ngẫu nhiên**.

### 2.1. Định nghĩa chính thức và ràng buộc tồn tại
Xét **vector ngẫu nhiên** $V = (X, Y)$ trên **không gian xác suất** $(\Omega, \mathscr{M}, P)$. Điều kiện để định nghĩa **hiệp phương sai** là các kỳ vọng $E[X]$ và $E[Y]$ phải tồn tại hữu hạn.

> [!info]+ Định nghĩa chính thức Hiệp phương sai (Lý thuyết xác suất)
> Khi đó, kỳ vọng của biến số ngẫu nhiên $(X - E[X])(Y - E[Y])$ được gọi là **hiệp phương sai** (*Covariance*) của $X$ và $Y$, ký hiệu là $\operatorname{Cov}(X, Y)$ :
> $$\operatorname{Cov}(X, Y) = E[\ (X - E[X])\ (Y - E[Y])\ ]$$
> Từ định nghĩa này và tính tuyến tính của kỳ vọng, ta có thêm một số mệnh đề sau: 
> $$\operatorname{Cov}(X, Y) = E[XY] - E[X] \cdot E[Y]$$
> $$\operatorname{Var}[X] = \operatorname{Cov}(X, X)$$

Chứng minh: 
$$\begin{align}
\operatorname{Cov}(X, Y) &= E[\ (X - E[X])\ (Y - E[Y]) \ ] \\
&= E[\ XY - X \cdot E[Y] - Y \cdot E[X] + E[X] \cdot E[Y]\ ] \\
&= E[XY] - E[X\cdot E[Y]] - E[Y \cdot E[X]] + E[\ E[X]\cdot E[Y]\ ] \\
&= E[XY] - E[Y]\cdot E[X] - E[X]\cdot E[Y] + E[X] \cdot E[Y] \\
&= E[XY] - E[X]E[Y] \\ \\
\rightarrow \operatorname{Cov}(X,Y) &= E[XY] - E[X]E[Y]
\end{align}$$

Khi $Y = X$: 
$$\operatorname{Cov}(X,Y) = E[XX] - E[X]E[X] = \operatorname{Var}(X)$$

Tùy thuộc vào bản chất của **vector ngẫu nhiên** $V = (X,Y)$ là rời rạc hay liên tục, định nghĩa trên có thể được cụ thể hóa thành hai trường hợp thông qua các hàm phân phối.

### 2.2. Với Vector ngẫu nhiên rời rạc
Nếu $V=(X,Y)$ là **vectơ ngẫu nhiên rời rạc**, ta biểu diễn mối quan hệ của chúng thông qua **hàm mật độ xác suất đồng thời** (hay **hàm khối xác suất** - *joint pmf*) $f_{X,Y}(x_i, y_j) = P(X=x_i, Y=y_j)$. 

> [!info]+ Hiệp phương sai cho cặp biến Rời rạc (Lý thuyết xác suất)
> Khi đó, hiệp phương sai được tính thông qua chuỗi kép :
> $$\operatorname{Cov}(X, Y) = \sum_{i}\sum_{j} (x_i - \mu_X)(y_j - \mu_Y) f_{X,Y}(x_i, y_j)$$
> Viết dưới dạng rút gọn:
> $$\operatorname{Cov}(X, Y) = \left( \sum_{i}\sum_{j} x_i y_j f_{X,Y}(x_i, y_j) \right) - E[X]E[Y]$$

### 2.3. Đối với Vectơ ngẫu nhiên liên tục
Nếu $V=(X,Y)$ là **vectơ ngẫu nhiên liên tục**, phân phối của chúng được đặc trưng bởi **hàm mật độ xác suất đồng thời** (*joint pdf*). Phép tổng lúc này được chuyển thành tích phân bội trên $\mathbb{R}^2$.

> [!info]+ Hiệp phương sai cho cặp biến Liên tục (Lý thuyết xác suất)
> Hiệp phương sai của vectơ ngẫu nhiên liên tục được phát biểu dưới dạng:  
> $$\operatorname{Cov}(X, Y) = \iint_{\mathbb{R}^2} xy \cdot f_{X,Y}(x, y) \,dxdy - \left(\iint_{\mathbb{R}^2} x \cdot f_{X,Y}(x,y) \,dxdy\right)\left(\iint_{\mathbb{R}^2} y \cdot f_{X,Y}(x,y) \,dxdy\right)$$

### 2.4. Không tương quan, Độc lập và Độc lập tuyến tính
Nếu hai biến ngẫu nhiên **độc lập** thì:
$$E[XY] = E[X]E[Y] \quad (1)$$

Hai biến ngẫu nhiên $X$ và $Y$ được gọi là **không tương quan** khi và chỉ khi:
$$\operatorname{Cov}(X, Y) = 0 \iff E[XY] = E[X]E[Y] \quad (2)$$

Từ (1) và (2) suy ra:
$$\text{Độc lập} \implies E[XY] = E[X]E[Y] \iff \text{Không tương quan}$$

> [!danger]+ Sai lầm
> Do đó, ta hiểu được rằng khi hai biến ngẫu nhiên được gọi là **độc lập**, điều đó có nghĩa là chúng **không tương quan**. ***Ngược lại khi hai biến ngẫu nhiên không tương quan, không thể suy ra chúng độc lập.***

Nói thêm về **không tương quan**, hiểu một cách đơn giản, hai biến $X$ và $Y$ được gọi là **không tương quan** nếu chúng không có mối quan hệ đường thẳng với nhau. Tức là nếu bạn cố tình vẽ một đường thẳng để dự đoán xu hướng của $X$ theo $Y$ thì nó sẽ bị sai hoàn toàn. Vậy điều này có tương đương với **độc lập tuyến tính** không? 

Câu trả lời là không chắc và không nên so sánh như thế. Vốn dĩ hai khái niệm này thuộc về hai phạm trù khác nhau của toán học. Khái niệm **không tương quan** thuộc về Lý thuyết Xác suất, còn **độc lập tuyến tính** thuộc về Đại số tuyến tính. **Độc lập tuyến tính** trong đại số tuyến tính được định nghĩa như sau:
$$aX + bY = 0 \iff a = b = 0$$

Điều này có nghĩa là không thể tạo ra biến này bằng cách lấy một con số nhân với biến kia (tức là không tồn tại số $k$ để $Y = kX$). Dưới góc nhìn hình học, hai vector $X$ và $Y$ không nằm trên cùng một đường thẳng đi qua gốc tọa độ.

Một số ví dụ về việc hai khái niệm này không tương đương:

> [!example]+ Độc lập tuyến tính nhưng VẪN tương quan
> Giả sử $X$ là một biến ngẫu nhiên có phương sai $\operatorname{Var}(X) > 0$. Ta định nghĩa biến $Y$ như sau:
> $$Y = 2X + Z$$
> (Trong đó $Z$ là một biến nhiễu **độc lập** với $X$ và có phương sai khác 0).
> 
> - **Về mặt đại số:** $X$ và $Y$ **độc lập tuyến tính**. Bạn không thể tìm được một hằng số $k$ nào để $Y = kX$ vì biểu thức của $Y$ luôn bị vướng biến ngẫu nhiên $Z$.
> - **Về mặt xác suất:** Ta tính hiệp phương sai:
>   $$\operatorname{Cov}(X,Y) = \operatorname{Cov}(X, 2X + Z) = 2\operatorname{Var}(X) + \operatorname{Cov}(X,Z) = 2\operatorname{Var}(X) \neq 0$$
> 
> **Kết luận:** $X$ và $Y$ **độc lập tuyến tính** nhưng chúng có tương quan rất mạnh với nhau.

> [!example]+ Không tương quan nhưng LẠI phụ thuộc tuyến tính
> Giả sử biến $Y$ là một biến hằng số và luôn bằng 0 (hầu chắc chắn), còn $X$ là một biến ngẫu nhiên bất kỳ.
> 
> - **Về mặt xác suất:** Vì $Y = 0$ là hằng số nên nó không biến thiên, kéo theo:
>   $$\operatorname{Cov}(X,Y) = \operatorname{Cov}(X,0) = 0$$
>   Suy ra $X$ và $Y$ **không tương quan**.
> - **Về mặt đại số:** Ta xét phương trình tuyến tính: $aX + bY = 0$. Kế thừa từ việc $Y=0$, ta chỉ cần chọn $a = 0$ và $b = 5$ (một nghiệm không tầm thường), phương trình $0 \cdot X + 5 \cdot 0 = 0$ luôn đúng. Do đó, $X$ và $Y$ **phụ thuộc tuyến tính**.

---
## 3. Mô hình hóa Toán học bằng Đại số tuyến tính 
Để hệ thống hóa cho quá trình tính toán các mô hình *Machine Learning* hay *Deep Learning*, ta không thể dùng vòng lặp `for` hay tổng $\Sigma$. Ta phải chuyển mọi kiến thức đã biết về giải tích sang dạng ma trận.

### 3.1. Hiệp phương sai 2 biến

Đầu tiên ta xem xét lại công thức Hiệp phương sai mẫu đã biết trong giải tích:
$$S_{XY} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y})$$

Bây giờ ta hãy nhìn kĩ lại các thành phần để chuyển công thức trên sang dạng đại số tuyến tính. Xét hai vector dữ liệu $\mathbf{x}$ và $\mathbf{y}$ gồm $n$ quan sát:
$$\mathbf{x} = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix}; \quad \mathbf{y} = \begin{bmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{bmatrix}$$

Khi đó người ta gọi $\mathbf{x}_c$ và $\mathbf{y}_c$ lần lượt là **vector ly sai** (*Deviation Vector*) của biến $X$ và $Y$, trong đó:
$$\mathbf{x}_c = \mathbf{x} - \bar{x} \mathbf{1}_{n} = \begin{bmatrix} x_1 - \bar{x} \\ x_2 - \bar{x} \\ \vdots \\ x_n - \bar{x} \end{bmatrix}; \quad \mathbf{y}_c = \mathbf{y} - \bar{y} \mathbf{1}_{n} = \begin{bmatrix} y_1 - \bar{y} \\ y_2 - \bar{y} \\ \vdots \\ y_n - \bar{y} \end{bmatrix}$$

Trong đại số tuyến tính, tổng các tích của hai vector chính là **Tích vô hướng** (*Dot Product*):
$$\sum_{i=1}^{n}a_{i} \cdot b_{i} = a_{1}\cdot b_{1} + a_{2}\cdot b_{2} + \dots + a_{n} \cdot b_{n} = \begin{bmatrix} a_1 & a_{2} & \dots & a_{n} \end{bmatrix} \cdot \begin{bmatrix} b_1 \\ b_{2} \\ \vdots \\ b_{n} \end{bmatrix} = \mathbf{a}^T \mathbf{b}$$

Áp dụng biến đổi trên, ta thực hiện tương tự với *Covariance*:
$$\sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y}) = \begin{bmatrix} x_1 - \bar{x} & x_2 - \bar{x} & \dots & x_n - \bar{x} \end{bmatrix} \cdot \begin{bmatrix} y_1 - \bar{y} \\ y_2 - \bar{y} \\ \vdots \\ y_n - \bar{y} \end{bmatrix} = \mathbf{x}_{c}^T \mathbf{y}_{c}$$

> [!info]+ Hiệp phương sai mẫu (Đại số tuyến tính)
> Vậy **Hiệp phương sai mẫu** giữa hai biến trong Đại số tuyến tính được biểu diễn gọn gàng dưới dạng: 
> $$S_{XY} = \frac{1}{n-1}\mathbf{x}_{c}^T \mathbf{y}_{c}$$

### 3.2. Ma trận Hiệp phương sai

Trong thực tế, bộ dữ liệu có $p$ biến (rất nhiều biến). Giả sử ta có **ma trận dữ liệu gốc** $\mathbf{X}$ kích thước $n \times p$ được biểu diễn dưới dạng các vector cột như sau:

$$
\mathbf{X} = \begin{bmatrix} 
| & | & & | \\ 
\mathbf{x}_1 & \mathbf{x}_2 & \dots & \mathbf{x}_p \\ 
| & | & & | 
\end{bmatrix}
$$

Trong đó, mỗi $\mathbf{x}_j$ (với $j = 1, 2, \dots, p$) là một vector cột kích thước $n \times 1$ chứa toàn bộ $n$ giá trị của biến thứ $j$.

**Ma trận dữ liệu ly sai** $\mathbf{X}_c$ được tạo ra bằng cách lấy từng phần tử của ma trận gốc $\mathbf{X}$ trừ đi giá trị trung bình của cột tương ứng. Nói cách khác, ta thực hiện phép tịnh tiến (dịch tâm) từng cột $\mathbf{x}_j$ về trung điểm 0. 

Vector ly sai của cột thứ $j$ được tính chi tiết như sau:

$$
\mathbf{x}_{c,j} = \mathbf{x}_j - \bar{x}_j \mathbf{1}_n = 
\begin{bmatrix} 
x_{1j} - \bar{x}_j \\ 
x_{2j} - \bar{x}_j \\ 
\vdots \\ 
x_{nj} - \bar{x}_j 
\end{bmatrix}
$$
*(Với $\mathbf{1}_n$ là vector cột gồm $n$ phần tử đều có giá trị bằng 1).*

Khi đó, ta có thể biểu diễn ma trận ly sai $\mathbf{X}_c$ (kích thước $n \times p$) một cách tổng quát bằng các vector cột đã được trừ trung bình:

$$
\mathbf{X}_c = \begin{bmatrix} 
| & | & & | \\ 
\mathbf{x}_{c,1} & \mathbf{x}_{c,2} & \dots & \mathbf{x}_{c,p} \\ 
| & | & & | 
\end{bmatrix} \quad \text{và} \quad
\mathbf{X}_c^T = \begin{bmatrix} 
- & \mathbf{x}_{c,1}^T & - \\ 
- & \mathbf{x}_{c,2}^T & - \\ 
& \vdots & \\ 
- & \mathbf{x}_{c,p}^T & - 
\end{bmatrix}$$

Bây giờ lấy dòng $\mathbf{X}_c^T$ nhân với cột của $\mathbf{X}_c$, ta có toàn bộ tích vô hướng của mọi cặp biến có thể:
$$\mathbf{X}_c^T \mathbf{X}_c = \begin{bmatrix} 
\mathbf{x}_{c,1}^T \mathbf{x}_{c,1} & \mathbf{x}_{c,1}^T \mathbf{x}_{c,2} & \dots & \mathbf{x}_{c,1}^T \mathbf{x}_{c,p} \\ 
\mathbf{x}_{c,2}^T \mathbf{x}_{c,1} & \mathbf{x}_{c,2}^T \mathbf{x}_{c,2} & \dots & \mathbf{x}_{c,2}^T \mathbf{x}_{c,p} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
\mathbf{x}_{c,p}^T \mathbf{x}_{c,1} & \mathbf{x}_{c,p}^T \mathbf{x}_{c,2} & \dots & \mathbf{x}_{c,p}^T \mathbf{x}_{c,p} 
\end{bmatrix}$$

Vì tích vô hướng chia cho bậc tự do chính là Hiệp phương sai $\left(\frac{1}{n-1}\mathbf{x}_{c,i}^T \mathbf{x}_{c,j} = \operatorname{Cov}(X_i, X_j)\right)$ và tích vô hướng với chính nó là Phương sai $\left(\frac{1}{n-1}\mathbf{x}_{c,i}^T \mathbf{x}_{c,i} = \operatorname{Var}(X_i)\right)$, nên khi nhân toàn bộ ma trận $\mathbf{X}_c^T\mathbf{X}_c$ với vô hướng $\frac{1}{n-1}$, ta thu được đại lượng cốt lõi.

> [!info]+ Ma trận hiệp phương sai (Đại số tuyến tính)
> Ma trận thu được gọi là **Ma trận Hiệp phương sai** (*Covariance Matrix*), ký hiệu là $\Sigma$ (*Sigma*):
> $$\Sigma = \frac{1}{n-1} \mathbf{X}_c^T \mathbf{X}_c = \begin{bmatrix} 
\operatorname{Var}(X_1) & \operatorname{Cov}(X_1, X_2) & \dots & \operatorname{Cov}(X_1, X_p) \\ 
\operatorname{Cov}(X_2, X_1) & \operatorname{Var}(X_2) & \dots & \operatorname{Cov}(X_2, X_p) \\ 
\vdots & \vdots & \ddots & \vdots \\ 
\operatorname{Cov}(X_p, X_1) & \operatorname{Cov}(X_p, X_2) & \dots & \operatorname{Var}(X_p) 
\end{bmatrix}$$

Về mặt chiều không gian toán học:
*   Ma trận $\mathbf{X}_c$ có kích thước $(n \times p)$
*   Ma trận $\mathbf{X}_c^T$ có kích thước $(p \times n)$
*   $\implies \Sigma = (p \times n) \times (n \times p) = \mathbf{(p \times p)}$

Đây là một ma trận vuông kích thước $p \times p$ **đối xứng**  rất đẹp. Đường chéo chính chứa các giá trị phương sai đơn lẻ. Tất cả các ô ngoài đường chéo chứa hiệp phương sai thể hiện mối quan hệ tương hỗ giữa các cặp biến khác nhau. Ứng dụng của ma trận này sẽ được đề cập sau.

---

## 4. Ví dụ tính tay 

Đến đây, chúng ta đã nắm trong tay 3 góc nhìn toàn cảnh về *Covariance*. Để thực sự hiểu kiến thức này, ta cần tự tay thực hiện các phép tính  trên các tập dữ liệu thu nhỏ để cảm nhận được luồng đi của dữ liệu.
### 4.1. Ví dụ đơn giản
> [!example]+ Ví dụ 1: Tính tay theo góc nhìn Thống kê (Dữ liệu mẫu)
> Giả sử ta thu thập được một tập dữ liệu nhỏ của $n=3$ học sinh, bao gồm hai biến: Số giờ ôn thi $X$ (giờ) và Điểm bài kiểm tra $Y$ (điểm).
> Dữ liệu được cho như sau: 
> $X = [2, 4, 6]$
> $Y = [3, 5, 10]$
> 
> **Bước 1: Tính trung bình mẫu $\bar{x}$ và $\bar{y}$**
> $$\bar{x} = \frac{2 + 4 + 6}{3} = 4$$
> $$\bar{y} = \frac{3 + 5 + 10}{3} = \frac{18}{3} = 6$$
> 
> **Bước 2: Tính độ lệch từng điểm dữ liệu so với trung bình**
> - Biến $X$: $(x_1 - \bar{x}) = -2$; $(x_2 - \bar{x}) = 0$; $(x_3 - \bar{x}) = 2$
> - Biến $Y$: $(y_1 - \bar{y}) = -3$; $(y_2 - \bar{y}) = -1$; $(y_3 - \bar{y}) = 4$
> 
> **Bước 3: Tính tổng tích các độ lệch và chia cho bậc tự do $(n-1)$**
> $$S_{XY} = \frac{1}{3-1} [(-2)(-3) + (0)(-1) + (2)(4)]$$
> $$S_{XY} = \frac{1}{2} [6 + 0 + 8] = \frac{14}{2} = 7$$
> 
> **Nhận xét:** $S_{XY} = 7 > 0$. Điều này cho thấy mối quan hệ đồng biến mạnh: học càng nhiều giờ thì điểm có xu hướng càng cao.

> [!example]+ Ví dụ 2: Tính tay theo góc nhìn Xác suất (Hệ rời rạc)
> Xét một vector ngẫu nhiên $V=(X,Y)$ với **hàm khối xác suất** (*Joint PMF*) cho trong bảng sau:
> 
> | $X \setminus Y$ | $Y=1$ | $Y=2$ | Hàm biên $P_X(x)$ |
> | :--- | :---: | :---: | :---: |
> | **$X=0$** | $0.2$ | $0.3$ | $0.5$ |
> | **$X=1$** | $0.4$ | $0.1$ | $0.5$ |
> | **Hàm biên $P_Y(y)$** | $0.6$ | $0.4$ | $1.0$ |
> 
> **Bước 1: Tính kỳ vọng biên $E[X]$ và $E[Y]$**
> $$E[X] = \sum x \cdot P_X(x) = 0(0.5) + 1(0.5) = 0.5$$
> $$E[Y] = \sum y \cdot P_Y(y) = 1(0.6) + 2(0.4) = 0.6 + 0.8 = 1.4$$
> 
> **Bước 2: Tính kỳ vọng đồng thời $E[XY]$**
> $$E[XY] = \sum_{x}\sum_{y} xy \cdot P(x,y)$$
> $$E[XY] = (0\cdot 1)(0.2) + (0\cdot 2)(0.3) + (1\cdot 1)(0.4) + (1\cdot 2)(0.1) = 0 + 0 + 0.4 + 0.2 = 0.6$$
> 
> **Bước 3: Áp dụng công thức hiệp phương sai**
> $$\operatorname{Cov}(X,Y) = E[XY] - E[X]E[Y] = 0.6 - (0.5)(1.4) = 0.6 - 0.7 = -0.1$$

> [!example]+ Ví dụ 3: Tính tay Ma trận *Covariance* bằng Đại số tuyến tính
> Quay lại tập dữ liệu ở Ví dụ 1, ta hãy trình bày nó dưới dạng Ma trận dữ liệu $\mathbf{X}$ (kích thước $3 \times 2$):
> $$\mathbf{X} = \begin{bmatrix} 2 & 3 \\ 4 & 5 \\ 6 & 10 \end{bmatrix}$$
> 
> **Bước 1: Tìm ma trận dữ liệu ly sai $\mathbf{X}_c$ (Mean-centered Matrix)**
> Ta đã biết vector trung bình là $\begin{bmatrix} 4 & 6 \end{bmatrix}$. Trừ mỗi cột của $\mathbf{X}$ cho trung bình tương ứng:
> $$\mathbf{X}_c = \begin{bmatrix} 2-4 & 3-6 \\ 4-4 & 5-6 \\ 6-4 & 10-6 \end{bmatrix} = \begin{bmatrix} -2 & -3 \\ 0 & -1 \\ 2 & 4 \end{bmatrix}$$
> 
> **Bước 2: Lấy chuyển vị $\mathbf{X}_c^T$ và nhân ma trận $\mathbf{X}_c^T \mathbf{X}_c$**
> $$\mathbf{X}_c^T = \begin{bmatrix} -2 & 0 & 2 \\ -3 & -1 & 4 \end{bmatrix}$$
> $$\mathbf{X}_c^T \mathbf{X}_c = \begin{bmatrix} -2 & 0 & 2 \\ -3 & -1 & 4 \end{bmatrix} \begin{bmatrix} -2 & -3 \\ 0 & -1 \\ 2 & 4 \end{bmatrix} = \begin{bmatrix} (-2)^2 + 0^2 + 2^2 & (-2)(-3) + 0(-1) + (2)(4) \\ (-3)(-2) + (-1)(0) + (4)(2) & (-3)^2 + (-1)^2 + 4^2 \end{bmatrix}$$
> $$\mathbf{X}_c^T \mathbf{X}_c = \begin{bmatrix} 8 & 14 \\ 14 & 26 \end{bmatrix}$$
> 
> **Bước 3: Chia cho bậc tự do $(n-1 = 2)$ để ra Ma trận $\Sigma$**
> $$\Sigma = \frac{1}{2} \begin{bmatrix} 8 & 14 \\ 14 & 26 \end{bmatrix} = \begin{bmatrix} 4 & 7 \\ 7 & 13 \end{bmatrix}$$
> **Đọc hiểu ma trận $\Sigma$:** Phương sai của $X$ là $\operatorname{Var}(X) = 4$. Phương sai của $Y$ là $\operatorname{Var}(Y) = 13$. Hiệp phương sai $\operatorname{Cov}(X,Y) = 7$ (Khớp hoàn toàn với kết quả Ví dụ 1!).



### 4.2. Phân biệt Covariance vs. Correlation (Hệ số tương quan)

Có thể bạn đọc thắc mắc tại sao lại có mục con phân biệt *Covariance* và *Correlation* trong mục ví dụ. Tôi nghĩ nếu tôi nêu ra vấn đề **sau khi** bạn đọc đã có một chút cảm giác về con số *Covariance* qua các ví dụ tính tay, sẽ giúp bạn đọc dễ hình dung được vấn đề hơn. Quay lại,  một trong những vấn đề lớn nhất của **Hiệp phương sai** (*Covariance*) là giá trị của nó phụ thuộc vào **đơn vị đo lường**. 

Ví dụ, nếu chiều cao đo bằng mét (m) thay vì centimet (cm), con số $\operatorname{Cov}(X,Y)$ sẽ nhỏ đi hàng nghìn lần, dù bản chất xu hướng dữ liệu không hề thay đổi. Do đó, ta không thể nhìn vào con số $S_{XY} = 7$ hay $S_{XY} = 7000$ để nói rằng mối quan hệ này "mạnh" hay "yếu", ta chỉ biết nó mang dấu dương (cùng chiều) hay âm (ngược chiều).

> [!danger]+ Sai lầm thường gặp
> Tuyệt đối không dùng *Covariance* để so sánh cường độ tương quan giữa các cặp biến khác nhau. Để giải quyết điểm yếu này, các nhà thống kê sinh ra **Hệ số tương quan Pearson** (*Pearson Correlation Coefficient* - ký hiệu là $\rho$ hoặc $r$).

Về bản chất, **Tương quan** (*Correlation*) chính là *Covariance* đã được chuẩn hóa (*Standardized*). Bằng cách chia *Covariance* cho tích của độ lệch chuẩn hai biến, ta ép không gian giá trị khổng lồ của nó về một cái lồng chật hẹp từ $[-1, 1]$.

> [!note]+ Hệ số tương quan **Correlation**
$$\rho_{X,Y} = \frac{\operatorname{Cov}(X,Y)}{\sigma_X \sigma_Y}$$

**Tóm tắt phân biệt:**
*   **Covariance:** Từ $(-\infty, +\infty)$. Đo lường *hướng* (dấu âm/dương) của mối quan hệ tuyến tính. Bị ảnh hưởng bởi thang đo.
*   **Correlation:** Ràng buộc chặt trong $[-1, 1]$. Đo lường cả *hướng* và *cường độ* (mạnh/yếu) của mối quan hệ tuyến tính. Miễn nhiễm với sự thay đổi của thang đo.

Tuy nhiên bài viết này đã khá dài, **Hệ số tương quan** sẽ được trình bày ở một bài viết khác.


### 4.3. Bài tập luyện thêm

Ở đây có một số ví dụ tính tay, nếu có thời gian hãy làm thử để hiểu sâu hơn bản chất của *Covariance*

> [!example]+ Bài tập 1: Hiệp phương sai của Vectơ ngẫu nhiên rời rạc
> Xét vectơ ngẫu nhiên $V = (X, Y)$ có tập giá trị $D_X = D_Y = \{0, 1\}$. Biết kỳ vọng của mỗi biến là $\mu_X = 0.2$ và $\mu_Y = 0.3$. Phân phối xác suất đồng thời $f_{X,Y}(x,y)$ cho ra các giá trị sau: 
> * $f_{X,Y}(0,0) = 0.5$
> * $f_{X,Y}(1,0) = 0.2$
> * $f_{X,Y}(0,1) = 0.3$
> * $f_{X,Y}(1,1) = 0$
> 
> **Yêu cầu:**
> 1. Áp dụng công thức định nghĩa $\operatorname{Cov}(X, Y) = E[(X - \mu_X)(Y - \mu_Y)]$ để tính hiệp phương sai của $X$ và $Y$.
> 2. Áp dụng Mệnh đề 2.2.5 để tính lại $\operatorname{Cov}(X, Y)$ thông qua $E[XY]$ và kiểm chứng kết quả.
> 3. **Chứng minh lý thuyết:** Giả sử ta có một chuỗi các biến ngẫu nhiên $X_1, X_2, ..., X_n$ không tương quan từng đôi một (tức là $\operatorname{Cov}(X_i, X_j) = 0$ với mọi $i \neq j$). Hãy chứng minh rằng phương sai của tổng bằng tổng các phương sai:
>    $$\operatorname{Var}\left(\sum_{j=1}^n X_j\right) = \sum_{j=1}^n \operatorname{Var}(X_j)$$

> [!example]+ Bài tập 2: Tìm Ma trận Hiệp phương sai cho phân phối mới
> Trong giáo trình, ma trận hiệp phương sai $\operatorname{Cov}(V)$ đã được xác định cho phân phối n-thức (Multinomial). Bây giờ, ta xét một dạng phân phối khác dạng toàn phương là **Phân phối Chuẩn 2-chiều (*Bivariate Normal Distribution*)**.
> 
> Xét vectơ ngẫu nhiên $V = (X, Y)$ có hàm mật độ xác suất tổng quát chứa biểu thức dạng ma trận:
> $$\mathbf{x}^T \mathbf{\Sigma}^{-1} \mathbf{x}$$
> Với ma trận hiệp phương sai cấp 2 được định nghĩa là:
> $$\mathbf{\Sigma} = \begin{pmatrix} \sigma_X^2 & \rho\sigma_X\sigma_Y \\ \rho\sigma_X\sigma_Y & \sigma_Y^2 \end{pmatrix}$$
> 
> **Yêu cầu:**
> 1. Giả sử $X$ và $Y$ là hai biến ngẫu nhiên đã được chuẩn hóa để có phương sai bằng 1 ($\sigma_X^2 = \sigma_Y^2 = 1$). Hãy viết lại ma trận Hiệp phương sai $\mathbf{\Sigma}$.
> 2. Tính định thức $\det(\mathbf{\Sigma})$ theo hệ số tương quan $\rho$. Điều kiện nào của $\rho$ để ma trận này xác định dương?

> [!example]+ Bài tập 3: Hiệp phương sai của Phân phối liên tục bằng Tích phân
> Xét vectơ ngẫu nhiên liên tục $V = (X, Y)$ có phân phối chuẩn 2-chiều tổng quát với hàm mật độ xác suất (pdf) đồng thời là:
> $$f_{X,Y}(x, y) = \frac{1}{2\pi\sqrt{1-\rho^2}} \exp\left\{ -\frac{1}{2(1-\rho^2)} \left[ x^2 - 2\rho xy + y^2 \right] \right\}$$
> với $-1 < \rho < 1$. 
> 
> **Yêu cầu:**
> 3. Hãy thiết lập biểu thức tích phân kép để tính $\operatorname{Cov}(X, Y) = \iint_{\mathbb{R}^2} xy \cdot f_{X,Y}(x, y) \,dxdy$.
> 4. Sử dụng phép đổi biến số $u = \frac{x - \rho y}{\sqrt{1-\rho^2}}$ và $v = y$, hãy tính định thức Jacobian $\frac{\partial(x,y)}{\partial(u,v)}$.
> 5. Giải tích phân sau khi đổi biến để chứng minh rằng $\operatorname{Cov}(X, Y) = \rho$.

> [!example]+ Bài tập 4: Đọc hiểu Ma trận Hiệp phương sai và Tính độc lập
> Xét vectơ ngẫu nhiên phân phối chuẩn nhiều chiều $V = (X, Y) \sim mnorm(\mathbf{\mu}, \mathbf{\Sigma})$.
> Cho ma trận hiệp phương sai:
> $$\mathbf{\Sigma} = \begin{pmatrix} 1 & \rho \\ \rho & 1 \end{pmatrix}$$
> 
> **Yêu cầu:**
> 6. Nếu thay $\rho = 0$, ma trận $\mathbf{\Sigma}$ trở thành ma trận đơn vị $\mathbf{I}$. Lúc này, hãy xác định $\operatorname{Cov}(X, Y)$.
> 7. Dựa vào kết quả trên, có thể kết luận gì về tính độc lập của $X$ và $Y$ khi phân phối của chúng là $mnorm(\mathbf{0}, \mathbf{I})$? (Gợi ý: Nhắc lại mối quan hệ đặc biệt giữa "không tương quan" và "độc lập" trong phân phối chuẩn đa chiều).

> [!example]+ Bài tập 5: Covariance trong các Quá trình Ngẫu nhiên
> Xét một quá trình Wiener (ứng dụng trong mô hình hóa chứng khoán hoặc chuyển động Brown), ký hiệu là hàm $W(t, \omega)$ (thường viết tắt là $W(t)$). 
> Biết quá trình này thỏa mãn các tính chất:
> * $W(0) = 0$
> * Với mọi $0 \le a < b \le c < d$, số gia $(W(b) - W(a))$ độc lập với số gia $(W(d) - W(c))$.
> * Số gia có phân phối chuẩn: $W(b) - W(a) \sim N(0, b - a)$.
> 
> **Yêu cầu:**
> 1. Hãy tìm kỳ vọng $E[W(3)]$ và $E[W(6)]$.
> 2. Khai triển $W(6) = W(3) + [W(6) - W(3)]$. Từ tính chất độc lập của các số gia, hãy tính hiệp phương sai $\operatorname{Cov}(W(3), W(6))$. 
> *(Gợi ý: Áp dụng tính chất song tuyến tính của Covariance: $\operatorname{Cov}(A, B+C) = \operatorname{Cov}(A, B) + \operatorname{Cov}(A, C)$).*

> [!example]+ Bài tập 6: Ứng dụng Covariance để tính Phương sai tổng
> Một nhóm nghiên cứu gồm 200 người, trong đó có đúng 100 nam và 100 nữ. Ta chọn ngẫu nhiên ra 100 người (lấy mẫu không hoàn lại).
> Gọi $X_i$ là biến chỉ báo nhận giá trị $X_i = 1$ nếu người thứ $i$ được chọn là nữ, và $X_i = 0$ nếu là nam. Tổng số nữ được chọn là $X = \sum_{i=1}^{100} X_i$.
> 
> **Yêu cầu:**
> 1. Tính kỳ vọng $E[X_i]$ và phương sai $\operatorname{Var}[X_i]$ đối với một lượt rút thứ $i$ bất kỳ.
> 2. Với hai lượt rút khác nhau $i \neq j$, hãy tính $E[X_i X_j]$ (Gợi ý: Đây là xác suất để cả 2 người được rút đều là nữ trong nhóm 100 nữ / 200 người).
> 3. Tính hiệp phương sai $\operatorname{Cov}(X_i, X_j)$. Tại sao hiệp phương sai này lại mang dấu âm?
> 4. Sử dụng công thức: 
>    $$\operatorname{Var}[X] = \sum_{i=1}^{100} \operatorname{Var}[X_i] + 2 \sum_{i < j}^{100} \operatorname{Cov}(X_i, X_j)$$
>    Hãy tính phương sai của tổng số nữ được rút $\operatorname{Var}[X]$.

---

## 5.  Triển khai bằng Code 

Đã hiểu tường tận về lý thuyết và bài tập, ta bắt tay code thử một vài bài đơn giản ứng dụng những thứ vừa học. Ở đây, ta tuyệt đối tránh xa vòng lặp `for` và dùng tư duy Vector hóa để tận dụng khả năng tính toán song song.

### PyTorch
```python
import torch

# Dữ liệu: Cột 1 là Chiều cao, Cột 2 là Cân nặng
X = torch.tensor([[160.0, 50.0], 
                  [170.0, 60.0], 
                  [180.0, 70.0]])

# Bước 1: Centering (Trừ đi trung bình của từng cột)
n = X.shape[0]
X_c = X - torch.mean(X, dim=0)

# Bước 2: Tích vô hướng toàn ma trận
cov_matrix = (X_c.T @ X_c) / (n - 1)
print(f"Covariance Matrix:\n{cov_matrix}")
```

### R / Tidyverse
```R
library(tidyverse)

df <- tibble(height = c(160, 170, 180), weight = c(50, 60, 70))

# Phản ánh đúng bản chất Thống kê từng bước
df_cov <- df %>%
  mutate(h_err = height - mean(height), 
         w_err = weight - mean(weight)) %>%
  summarize(cov_val = sum(h_err * w_err) / (n() - 1))

print(df_cov)
```

---

## 6. Ứng dụng Thực tế 

Trực giác từ không gian 2D (như Chiều cao - Cân nặng) chính là nền tảng cốt lõi để chúng ta kiểm soát các hệ thống đa biến phức tạp trong Khoa học Dữ liệu, Tài chính và Thống kê:

### 6.1. Machine Learning - Giảm chiều dữ liệu PCA
Khi xử lý một bức ảnh có kích thước 64x64 pixels, máy tính đang nhìn vào một không gian 4096 chiều. Trong thực tế, các pixels liền kề nhau thường có màu sắc rất giống nhau (tức là *Covariance* giữa chúng cực kỳ lớn).

Thuật toán **PCA** (Principal Component Analysis) sử dụng chính Ma trận Hiệp phương sai $\Sigma$ để tìm ra các trục biến thiên mạnh nhất (Vector riêng - *Eigenvectors* có trị riêng - *Eigenvalues* $\lambda$ lớn nhất). Nó sẽ nhóm các pixels đồng điệu này lại, giúp nén bức ảnh từ 4096 chiều xuống chỉ còn vài chục chiều (trục chính) mà hầu như không làm mất đi thông tin quan trọng.

### 6.2. Quantitative Finance (Tối ưu Danh mục & Quản trị Rủi ro)
Thay vì chiều cao và cân nặng, hãy tưởng tượng $X$ và $Y$ là lợi suất của 2 mã cổ phiếu. Trong tài chính, **Rủi ro** của một danh mục đầu tư (gồm cổ phiếu $X$ và cổ phiếu $Y$) được đo bằng Phương sai tổng. Theo Lý thuyết xác suất, phương sai của một tổng được tính bằng công thức:

$$\operatorname{Var}(X + Y) = \operatorname{Var}(X) + \operatorname{Var}(Y) + 2\operatorname{Cov}(X, Y)$$

**Bí quyết của các Quỹ đầu tư (Hedging):** Một nhà quản lý quỹ giỏi sẽ không chỉ tìm cổ phiếu lợi nhuận cao, mà họ sẽ chủ đích tìm kiếm các cặp tài sản có *Covariance* âm ($\operatorname{Cov}(X,Y) < 0$).

Nhìn vào công thức trên, phần $+ 2\operatorname{Cov}(X,Y)$ mang dấu âm sẽ trừ đi rủi ro tổng thể. Trực giác là: Khi cổ phiếu $X$ sập giá, cổ phiếu $Y$ sẽ có xu hướng tăng lên để bù đắp, giúp tài sản của bạn luôn ở mức an toàn.

### 6.3. Đánh giá sai số trong Lấy mẫu diện rộng (Sampling)
Khi tiến hành khảo sát diện rộng (ví dụ khảo sát 100 người từ 200 người để dự đoán kết quả bầu cử), kết quả của người được lấy mẫu sau thường bị ảnh hưởng bởi người được lấy mẫu trước (rút không hoàn lại). Lúc này, các biến khảo sát $X_i$ và $X_j$ không hề độc lập mà có *Covariance* khác $0$ (thường là mang dấu âm).

*Covariance* giúp các nhà thống kê tính toán chính xác phương sai (sai số) của toàn bộ cuộc khảo sát thông qua công thức:

$$\operatorname{Var}\left(\sum X\right) = \sum \operatorname{Var}(X_i) + 2\sum_{i<j} \operatorname{Cov}(X_i, X_j)$$

---

## 7. Câu hỏi thường gặp

---

🔗 [[MOC_Statistics]], [[MOC_Linear_Algebra]], [[MOC_Probability]]


