# 🛒 PHÂN CỤM KHÁCH HÀNG DỰA TRÊN LUẬT KẾT HỢP (RULE-BASED CLUSTERING)

## 👥 Thông tin Nhóm
- **Nhóm:** 6
- **Môn học:** Data Mining (Khai phá dữ liệu)
- **Thành viên:**
  - Ngô Hoàng Huy
  - Mai Văn Tiến
  - Nguyễn Trí Dũng
  - Chu Ngọc Hân

---

## 1. Giới thiệu bài toán và Mục tiêu nhóm

### 📌 Bài toán đặt ra
Các phương pháp phân cụm truyền thống (như RFM) chỉ cho biết khách hàng "chi nhiều hay ít", nhưng **không cho biết họ mua những gì**. Điều này khiến doanh nghiệp gặp khó khăn khi muốn thiết kế các gói combo sản phẩm cụ thể.

### 🎯 Mục tiêu của nhóm
Xây dựng một mô hình phân khúc khách hàng mới, kết hợp giữa:
1.  **Khai phá luật kết hợp (Association Rules):** Tìm ra các thói quen mua sắm đi kèm nhau (Ví dụ: Mua A thường mua B).
2.  **Phân cụm (Clustering):** Gom nhóm những khách hàng có cùng thói quen mua các combo đó.

=> **Kết quả:** Định danh chính xác chân dung khách hàng để đề xuất chiến lược Marketing cá nhân hóa.

---

## 2. Kết quả trọng tâm

Dựa trên thuật toán **FP-Growth** và **K-Means**, hệ thống đã phân loại khách hàng thành **3 nhóm** với đặc điểm hành vi khác biệt:

| Nhóm (Cluster) | Số lượng | Đặc điểm hành vi nổi bật |
| :--- | :--- | :--- |
| **Cluster 1** | **125 khách** | **Nhóm "Tín đồ Combo":** Đây là nhóm khách hàng tuân thủ tuyệt đối các luật mua sắm. Họ mua trọn bộ sưu tập *Herb Marker* (Parsley, Thyme, Basil...). |
| **Cluster 2** | **10 khách** | **Nhóm "Khách hàng Ngách":** Nhóm rất nhỏ nhưng mua sắm tập trung vào các sản phẩm đặc thù (Rosemary, Mint) với tần suất lặp lại cao. |
| **Cluster 0** | **4204 khách** | **Nhóm "Khách đại trà":** Chiếm đa số (96%). Mua sắm ngẫu nhiên, rời rạc và không theo quy luật combo cố định nào. |

---

## 3. Diễn giải các biểu đồ kỹ thuật

Dưới đây là các phân tích kỹ thuật chứng minh độ hiệu quả của mô hình nhóm đã xây dựng:

### 📊 Biểu đồ 1: Xác định số cụm tối ưu (Elbow & Silhouette)
*(Phương pháp giúp nhóm quyết định chọn K=3)*
![Elbow Method](images/elbow_method.png)
> **Phân tích:**
> - Đường màu xanh (Inertia) tạo thành "khuỷu tay" rõ rệt tại **K=3**.
> - Đường màu cam (Silhouette Score) đạt đỉnh cao nhất (~0.99) tại K=3.
> -> **Kết luận:** Chia khách hàng thành 3 nhóm là tối ưu nhất.

### 🧩 Biểu đồ 2: Trực quan hóa không gian cụm (PCA)
*(Hình ảnh các điểm dữ liệu sau khi phân nhóm)*
![PCA Clustering](images/pca_plot.png)
> **Phân tích:**
> - Các điểm dữ liệu (đại diện cho khách hàng) được tách thành các đám màu riêng biệt trên không gian 2 chiều.
> - **Cluster 1 (Xanh)** và **Cluster 2 (Vàng)** tách biệt hoàn toàn so với phần còn lại, chứng tỏ đặc điểm mua sắm của họ rất đặc trưng và khác biệt.

### ⚖️ Biểu đồ 3: So sánh hiệu quả mô hình (Binary vs Weighted)
*(So sánh 2 phương pháp tạo đặc trưng: Nhị phân và Trọng số)*
![Model Comparison](images/model_comparison.png)
> **Phân tích:**
> - Cả hai phương pháp đều cho kết quả Silhouette Score rất cao (> 0.98).
> - Phương pháp **Weighted (Trọng số Lift)** cho kết quả tương đương với Binary, chứng tỏ mô hình hoạt động ổn định dù có tính thêm trọng số độ mạnh của luật hay không.

---

## 4. Kết luận và Đề xuất hành động

Dựa trên chân dung khách hàng đã định danh, nhóm đề xuất chiến lược:

### ✅ Đối với Cluster 1 (125 khách - Tín đồ Combo)
* **Chiến lược:** Bán theo gói (Bundling).
* **Hành động:** Tạo gói sản phẩm **"Herb Collection"** (Gồm Parsley + Thyme + Basil).
* **Ưu đãi:** Giảm 10-15% khi mua trọn bộ thay vì mua lẻ.

### ✅ Đối với Cluster 2 (10 khách - Khách hàng Ngách)
* **Chiến lược:** Chăm sóc cá nhân hóa (Personalization).
* **Hành động:** Gửi thông báo riêng (SMS/Email) khi có các dòng sản phẩm thảo mộc mới hoặc hàng hiếm về kho.

### ✅ Đối với Cluster 0 (4204 khách - Đại trà)
* **Chiến lược:** Kích cầu diện rộng.
* **Hành động:** Gửi mã Freeship hoặc Voucher giảm giá theo giá trị đơn hàng để khuyến khích họ quay lại và mua nhiều hơn.

---
### ⚙️ Cách chạy dự án
1. Cài đặt thư viện: `pip install -r requirements.txt`
2. Chạy Dashboard: `streamlit run src/app.py`
