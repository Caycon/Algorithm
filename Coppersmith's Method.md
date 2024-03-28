# Coppersmith's Method
## Introduction
**Đa thức mod N:**
- Giả sử ta có đa thức sau: $f(x)= \sum_{i= 0}^n{a_ix^i}$ trong đó $a_n \neq 0$ (hệ số của lũy thừa bậc $n$ của $x$ khác 0). Bậc của đa thức $f(x)$, ký hiệu là $n$, chính là số mũ cao nhất của $x$ xuất hiện trong đa thức với hệ số khác 0.
- Chúng ta có thể giới hạn miền của $x$ và các hệ số là các số nguyên theo modulo $n$ (ký hiệu là $mod\ n$).
- Điều này cho phép bàn về nghiệm của đa thức f(x) theo modulo $n$, nghĩa là tìm các giá trị của $x$ thỏa mãn $f(x)$ chia hết cho $n$.
**Nghiệm của đa thức:**
- Nghiệm tổng quát:
    - Không tồn tại công thức tổng quát với các phép toán cơ bản để tìm nghiệm của đa thức bậc năm trở lên (tức là đa thức bậc $n$ lớn hơn hoặc bằng 5). Tuy nhiên đôi với các nghiệm nguyên, luôn có thể sử dụng phương pháp [**Newton**](https://en.wikipedia.org/wiki/Newton%27s_method) để xấp xỉ nghiệm, sau đó làm tròn lên giá trị gần nhất.
- Nghiệm với n là số nguyên tố:
    - Là vấn đề tìm nghiệm của $f(x)\pmod{n}$ (nghiệm theo modulo $n$, ký hiệu là $mod\ n$) khi $n$.
    - Hiện nay có một số thuật toán hiệu quả: [fast algorithms](https://en.wikipedia.org/wiki/Cantor%E2%80%93Zassenhaus_algorithm) để tìm tất cả các nghiệm trong trường hợp này.
- Nghiệm với n là lũy thừa của số nguyên tố:
    - Đối với n dạng lũy thừa của một số nguyên tố $n = p^m$, trước tiên có thể tìm nghiệm của $f(x)\equiv 0\pmod{p}$.
    - Sau đó, sử dụng Định lý nâng của Hensel để "nâng cấp" nghiệm lên modulo $p^m$.
- Nghiệm với n là hợp số tổng quát:
    - Với n là một hợp số tổng quát (n = tích của các lũy thừa của các số nguyên tố khác nhau, ký hiệu là: $\prod {p_i^{n_i}}$, có thể sử dụng Định lý Thừa số Trung Hoa để kết hợp tất cả các nghiệm theo từng modulo riêng lẻ $mod\ p_i^{n_i}$
- Việc giải các đa thức theo modulo n (ký hiệu mod n) thường khó khăn nếu chúng ta không biết cách phân tích n thành thừa số nguyên tố.
- Xét phương trình: $$x^2 \equiv 1\ mod\ n(n= pq)$$
    - Phương trình này có 4 nghiệm. Giả sử a là một nghiệm của đa thức $f(x) = x^2 - 1$ theo modulo $pq$.
    - Khi đó: $$a^2- 1 \equiv 0\ mod\ (pq)$$ hay: $$(a- 1)(a+ 1) \equiv 0\ mod\ (pq)$$
    - Điều này có nghĩa là $(a- 1)\ \vdots\ p$ hoặc $(a- 1)\ \vdots\ q$ (nhưng không thể chia hết cho cả p và q). Như vậy, từ việc tìm được nghiệm $a$ của đa thức, ta có thể phân tích được $n = pq$.
    - Như phân tích trên, việc giải phương trình đa thức theo modulo n thường khó khăn và tương đương với việc phân tích n thành thừa số nguyên tố - một vấn đề cũng chưa có thuật toán nhanh.
    - Lý giải về việc tại sao phương trình lại có 4 nghiệm như trên:
        - Xét phương trình: $$x^2 \equiv 1\ mod\ p$$ sẽ luôn có 2 nghiệm là $(1; -1)$.
        - Sử dụng kết quả ở trên: Ta có phương trình $x^2 - 1 ≡ 0 (mod\ p)$ có hai nghiệm: $x ≡ 1 (mod\ p)$ và $x ≡ -1 (mod\ p)$. Tương tự, nó cũng có hai nghiệm: $x ≡ 1 (mod\ q)$ và $x ≡ -1 (mod\ q)$.
        - Định lý thặng dư Trung Hoa (CRT): Bây giờ, ta có thể sử dụng Định lý số dư Trung Hoa (CRT) để kết hợp các nghiệm này modulo n. CRT nói rằng nếu $a ≡ b (mod\ m)$ và $a ≡ c (mod\ n)$, trong đó m và n là nguyên tố cùng nhau (không có ước số chung nào khác ngoài 1), thì tồn tại một nghiệm duy nhất a modulo bội số chung nhỏ nhất (LCM) của $m$ và $n$. Trong trường hợp của chúng ta, $p$ và $q$ là các số nguyên tố cùng nhau, và $n = pq$ là LCM của chúng.
        - Áp dụng CRT: Do $x ≡ 1 (mod\ p)$ và $x ≡ 1 (mod\ q)$, theo CRT, tồn tại một nghiệm duy nhất $x\ modulo\ n = pq$ thỏa mãn cả hai điều kiện. Giải pháp này đại diện cho một trong bốn giải pháp mà chúng ta đang tìm kiếm.
        - Tương tự, có các nghiệm $x ≡ -1 (mod\ p)$ và $x ≡ 1 (mod\ q)$, $x ≡ 1 (mod\ p)$ và $x ≡ -1 (mod\ q)$, và $x ≡ -1 (mod\ p)$ và $x ≡ -1 (mod\ q)$. Bốn nghiệm này tương ứng với bốn kết hợp có thể xảy ra của x đồng dư với 1 hoặc -1 modulo $p$ và $q$.

## Định lý Coppersmith
- Xét đa thức $F(x)$ với $F(x) \equiv 0\ mod\ n$ và $F(x)$ có các đặc điểm sau:
    - Hệ số của đa thức là số nguyên.
        > Là đa thức có toàn bộ các hệ số trong đã thức phải là số nguyên.
    - Là đa thức đơn vị. 
        > Đa thức đơn vị là đa thức có hệ số của bậc cao nhất bằng  1.
    - Không thể phân tích thành tích các đa thức.
        >  Một đa thức $F(x)$ với hệ số nguyên được coi là không phân tích nếu bất cứ khi nào bạn có thể biểu diễn nó dưới dạng tích của hai đa thức khác $g(x)$ và $h(x)$, thì ít nhất một trong $g(x)$ hoặc $h(x)$ phải là đa thức hằng (tức là 1 số hoặc một tham số, không thể chứa biến ở đây được).
        >  
**Định lý Coppersmith:**
- Giả thiết:
    > * $0 < \varepsilon < \min\{0.18, \frac{1}{d}\}$
    > * $F(x)$ là đa thức đơn vị, không phân tích với hệ số nguyên
    > * $F(x)$ có nghiệm $x_0$ modulo $N$
    > * $|x_0| < \frac{1}{2} N^{\frac{1}{d} - \varepsilon}$
 
- Kết luận:
    > Nghiệm $x_0$ của $F(x)$ có thể tìm được trong thời gian đa thức phụ thuộc vào $d$, $\frac{1}{\varepsilon}$ và $\log N$.

- Lưu ý:

    > * Thời gian đa thức nghĩa là thời gian thực hiện thuật toán tăng theo mức độ tương đối "chậm" khi kích thước đầu vào tăng lên.

**Ví dụ:**

* $d = 10$, $\varepsilon = 0.01$, $N = 1000$
* Thời gian tìm nghiệm $x_0$ có thể được tính toán bằng thuật toán với độ phức tạp O($d^3 \log N / \varepsilon^2$)

# Ứng dụng
## RSA
- Đầu tiên ta sẽ nói về RSA cơ bản:
    - Yếu tố cơ bản:
        > * $n = pq$
        > * $de ≡ 1\ (mod\ φ(n))$
        > * $e = 3$
    - Encrypt và decrypt:
        > * Encrypt: $c = m^3\ (mod\ N)$
        > * Decrypt: $m = c^(1/3)\ (mod\ N)$
- Vấn đề ở đây là RSA này rất yếu và dễ bị tấn công nếu kẻ tấn công có thể lấy căn bậc ba của c.
- Ta có một đề xuất sau để việc tấn công RSA trở nên khó hơn như sau:
    > * Bổ sung bit '1' vào bên trái m cho đến khi $|m| ≈ |N|$.
	> * Gọi phần bổ sung là $P$.
	> * Phương trình: $(P + m)^3 ≡ c\ (mod\ N)$
- Đồng thời khi làm như thế ta sẽ phải có chút biến đổi cách thức decrypt để tìm được m:
    > * Ta sẽ khai triển $(P + m)^3$ (với các bậc cao hơn ta có thể sử dụng nhị thức Newton để khai triển cho nhanh).
    > * Sau đó ta sẽ dựa vào P đã biết để giải phương trình tìm ra m. P có thể biết trước, hoặc tìm được theo quy tắc nào đó, hoặc P là số nhỏ có thể brute force.

**Ví dụ:**
- Cho phương trình sau: $(111000_2 + m)^3 - 1001001_2 ≡ 0\ (mod\ 101)$ ($a_2$ tức là số a cơ số 2).
- Khai triển và thu gọn, ta được: $15m^3 + 63m^2 + 21m + 1 ≡ 0\ (mod\ 101)$
- Giải phương trình, ta tìm được nghiệm $m = 3$.
 
## Hastad’s broadcast attack
- Tấn công này nhắm vào hệ thống RSA sử dụng số mũ (exponent) nhỏ cho khóa công khai.
    - Tấn công với message ngắn:
        > * Nếu message được gửi đi là ngắn, kẻ tấn công có thể bẻ khóa message chỉ cần  ít nhất e ciphertext được mã hóa từ cùng một message đó (với e là số mũ của khóa công khai).
    - Tấn công với message dài:
        > * Nếu message dài, kẻ tấn công vẫn có thể bẻ khóa được nếu message được padding tuyến tính (chẳng hạn như thêm hoặc đặt trước các bit được biết). Điều kiện cần là kẻ tấn công có được ít nhất e ciphertext được mã hóa từ cùng một message.
- **Định lý:** Cho $N_1,\cdots N_k$ là các số nguyên nguyên tố cùng nhau và $g_i(x)$ nhiều nhất là đa thức bậc $q$. Nếu $M< \min\{N_1,\cdots,N_k\}$ và $g_i(M)\equiv 0\pmod{N_i}$ với mỗi i và $k> q$, thì tồn tại một thuật toán hiệu quả để tính $M$.

- **Chứng minh:** Ta sử dụng thặng dư Trung Hoa để xây dựng $g(x)$ sao cho $g(M)\equiv 0\pmod{N_1 N_2\cdots N_k}$, khi đó $M$ và $g$ thỏa mãn yêu cầu của định lý Coppersmith. Sử dụng phương pháp của Coppersmith để phục hồi $M$.
# Định lý Bivariate Coppersmith
**Định lý:** 
-  Cho $F(x,y)$ là đa thức có hệ số nguyên và (d) là số tự nhiên sao cho cả $\deg_x F, \deg_y F \leq d$. Viết $F(x,y)=\sum_{0\leq i,j\leq d} F_{i,j} x^i y^j$ và định nghĩa $W=\max\limits_{0\leq i,j\leq d} \vert F_{i,j}\vert X^i Y^j$ cho mỗi $X$ và $Y$ là số tự nhiên.
- Nếu $XY< W^{\frac{2}{3d}}$ thì ta có thể tìm được nghiệm của $F\ mod\ N$ sao cho nghiệm $(x_0,y_0)$ thỏa mãn $\vert x_0\vert \leq X$ và $\vert y_0\vert \leq Y$ trong thời gian đa thức của $\log W$ và $2^d$.
**Mã giả:**
```Python
# Định lý Bivariate Coppersmith

# Hàm tìm nghiệm của đa thức hai biến F(x, y) mod N
def tim_nghiem(F, N, X, Y, d):

  # Khởi tạo hệ số và trọng số tối đa
  he_so = [[0] * (d + 1) for _ in range(d + 1)]
  W = 0

  # Trích xuất hệ số và tính trọng số tối đa
  for i in range(d + 1):
    for j in range(d + 1):
      he_so[i][j] = F[i][j]  # Giả sử F là mảng 2 chiều biểu diễn hệ số
      W = max(W, abs(he_so[i][j]) * X**i * Y**j)

  # Kiểm tra điều kiện nghiệm nhỏ
  if (X * Y) >= W**(2 / (3 * d)):
    print("Điều kiện nghiệm nhỏ không thỏa mãn. Không đảm bảo tìm được nghiệm.")
    return None

  # Triển khai thuật toán tìm nghiệm (thay thế bằng thuật toán cụ thể)
  # Phần này có thể liên quan đến các phép toán toán học phức tạp
  # và kỹ thuật đại số tuyến tính
  nghiem = tim_nghiem_thuat_toan(he_so, N, X, Y, d)

  return nghiem

# Ví dụ sử dụng (thay thế F bằng hệ số đa thức thực tế)
F = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
N = 1000
X = 10
Y = 20
d = 2

nghiem = tim_nghiem(F, N, X, Y, d)

if nghiem is not None:
  print("Tìm thấy nghiệm:", nghiem)
else:
  print("Tìm nghiệm thất bại.")

```
## Boneh-Durfee Attack
- Boneh-Durfee Attack là một phương pháp tấn công hệ thống mã hóa RSA dựa trên mối quan hệ giữa khóa công khai e và khóa bí mật d với các số nguyên tố p và q.

- Giả thiết:
> * $de = 1 + k\phi(n)$ (Đây là mối quan hệ giữa d, e và hàm Euler totient phi(n))
> * $\phi(n)=n-p-q+1$ (Hàm Euler totient được tính dựa trên các số nguyên tố p và q)
- Giải:
> * Từ hai biểu thức trên ta có: $de = 1+ k(n-p-q+1)$
> * Quy tắc cả hai vế theo modulo e: $de \equiv 1+ k(n-p-q+1) \pmod{e}$
> * Biến đổi: $2k(\frac{n+1}{2} - \frac{p+q}{2})+1\equiv 0\pmod{e}$
> * Qua các bước trên, ta thu được một đa thức hai biến $f(x, y)$: $f(x,y)=2x(A+y)+1\pmod{e}$ với $A$ là một hằng số phụ thuộc vào $n$.
> * Đa thức này có nghiệm nhỏ là $(x_0,y_0)=\left(k,-\frac{p+q}{2}\right)$.
> * Tấn công bằng định lý Bivariate Coppersmith:
    - Điều kiện cần để sử dụng phương pháp này là bậc của đa thức d phải nhỏ hơn $N^{0.292}$.
    - Sử dụng định lý Bivariate Coppersmith để tìm nghiệm nhỏ của đa thức $f(x, y)$.
    - Từ nghiệm nhỏ $(x_0, y_0)$, có thể phục hồi giá trị của k và do đó tìm ra được d.
# Định lý Howgrave-Graham
- Định lý Howgrave-Graham là một định lý liên quan mật thiết đến định lý Coppersmith. Định lý Howgrave-Graham giúp đơn giản hóa quá trình chứng minh và cho kết quả tốt hơn so với định lý Coppersmith.
- Ta có các khái niệm sau:
    - $F(x) = \sum\limits_{i=0}^d a_i x^i$: Đa thức với các hệ số nguyên, bậc d (a_d khác 0).
    - $x_0$: Nghiệm của phương trình $F(x) \equiv 0 \pmod{N}$.
    - $X$: Một số nguyên dương.
    - $b_F = (a_0, a_1X, a_2X^2, \cdots, a_d X^d)$: Vector được tạo ra từ các hệ số của F với bội số của X.
    - $\lvert\lvert v\rvert\rvert = \sqrt{\sum\limits_{i=1}^n v_i^2}$: Norm (độ dài) của vector v.

- **Định lý (Howgrave-Graham):** Nếu $\lvert\lvert b_F\rvert\rvert < \frac{N}{\sqrt{d+1}}$, thì $F(x_0) = 0$ trên tập số nguyên (không chỉ đúng theo modulo N).
- **Chứng minh:**
    - Sử dụng bất đẳng thức Cauchy-Schwarz:
    $$\sum\limits_{i=1}^n x_i \leq \sqrt{n \cdot \sum\limits_{i=1}^n x_i^2}$$

    - Áp dụng bất đẳng thức này vào việc tính giá trị tuyệt đối của $F(x_0)$:
$$\lvert F(x_0)\rvert = \left\lvert \sum\limits_{i=0}^d a_i x_0^i\right\rvert$$ $$\left\lvert \sum\limits_{i=0}^d a_i x_0^i\right\rvert \leq \sum\limits_{i=0}^d \lvert a_i\rvert\ \lvert x_0^i\rvert$$ $$\sum\limits_{i=0}^d \lvert a_i\rvert\ \lvert x_0^i\rvert < \sum\limits_{i=0}^d \lvert a_i\rvert X^i$$ $$\sum\limits_{i=0}^d \lvert a_i\rvert X^i \leq \sqrt{d+1} \lvert\lvert b_F\rvert\rvert$$ $$\sqrt{d+1} \lvert\lvert b_F\rvert\rvert\ \leq \sqrt{d+1}\frac{N}{\sqrt{d+1}}$$ $$\sqrt{d+1}\frac{N}{\sqrt{d+1}}= N$$
    - Từ bước 2, ta biết $-N < F(x_0) < N$. Do $F(x) \equiv 0 \pmod{N}$ thì điều này ngầm chỉ $F(x_0) = 0$ (không theo modulo).
## Phân tích N= pq khi biết một phần của p
- Giả thiết:
    - $N = pq$: Số cần phân tích, là tích của hai số nguyên tố p và q.
    - Có một ước lượng $\hat{p}$ của $p$ sao cho $p = \hat{p} + x_0$ với $\lvert x_0\rvert < X$.
    - Ví dụ: $p$ là số nguyên $k-bit$ và $\hat{p}$ có $k$ bit "cao" (MSB) giống với $p$ (nghĩa là biết nửa bit đầu tiên của $p$), do đó $\left\lvert p-\hat{p}\right\rvert < 2^k$.
- Ý tưởng:
    - Xác định đa thức bậc 1 $f(x) = \hat{p} + x$. Tìm nghiệm nhỏ của $f(x)$ theo modulo $p$ sẽ giúp phục hồi $p$.
    - Tuy nhiên, vì không biết chính xác $p$, ta cần "nâng cấp" đa thức $f(x)$ lên một đa thức khác $G$. Đa thức $G$ phải có các tính chất:
    - Có nghiệm nhỏ theo modulo $p^h$ ($h \in \mathbb{Z^+}$ ).
    - Thỏa mãn điều kiện của định lý Howgrave-Graham.
    - Bằng cách tìm nghiệm nhỏ $x_0$ của đa thức $G$ (thỏa mãn $G(x_0) = 0$), ta có thể suy ra nghiệm nhỏ của $f(x)$ theo modulo $p^h$ (tức là $f(x_0)\equiv 0\pmod{p^h}$).
    - Cuối cùng, sử dụng thuật toán Euclid tìm ước chung lớn nhất (GCD) của $N$ và $f(x_0)$ để phục hồi $p:\ p=\gcd(N, f(x_0))$.

- Định lý (tương tự định lý Coppersmith, được cải tiến bởi Howgrave-Graham):
    - Giả sử ta có các điều kiện sau: $N=pq$, $p< q< 2p$, $0< \varepsilon < \frac 14$, và $\hat{p}$ là một số tự nhiên sao cho $\left\lvert p-\hat{p}\right\rvert < \frac{1}{2\sqrt 2} N^{\frac 14 - \varepsilon}$. Khi đó $N$ có thể được phân tích thừa số trong thời gian đa thức của $\log N$ và $\frac 1\varepsilon$.


