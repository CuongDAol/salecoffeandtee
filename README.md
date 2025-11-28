# Báo cáo phân tích hiệu suất kinh doanh quán coffee

## 0. GIỚI THIỆU VỀ BỘ DỮ LIỆU (DATASET OVERVIEW)

Báo cáo này được xây dựng dựa trên kết quả phân tích dữ liệu bán hàng thực tế của hệ thống **Coffee & Tea**, nhằm cung cấp cái nhìn toàn diện về tình hình kinh doanh và hành vi khách hàng.

### 📂 Nguồn Dữ Liệu
Quá trình phân tích sử dụng 02 tập dữ liệu chính:
* **`accounting_sale.xlsx`**: Dữ liệu giao dịch chi tiết tại cửa hàng đơn lẻ (Specific Store).
* **`tatca.xlsx`**: Dữ liệu tổng hợp doanh thu của toàn bộ hệ thống cửa hàng (All Stores).

### ⏳ Phạm Vi Thời Gian (Timeframe)
* Dữ liệu bao gồm toàn bộ các giao dịch phát sinh trong **4 tháng**, từ ngày **01/03/2023** đến hết ngày **30/06/2023**.

### 🔍 Các Chỉ Số Phân Tích Chính
Báo cáo tập trung khai thác các chiều thông tin sau:
* **Sản phẩm (Product):** Tên món, Nhóm món (Category), Số lượng tiêu thụ.
* **Tài chính (Finance):** Tổng doanh thu (Total Revenue), Giá trị đơn hàng trung bình (AOV).
* **Thời gian (Time):** Xu hướng theo Tháng, Thứ trong tuần và Khung giờ trong ngày.
* **Vận hành (Operations):** Phương thức thanh toán, Nguồn đơn hàng (Tại chỗ/App).

### ⚠️ Ghi Chú Về Xử Lý Dữ Liệu
* Dữ liệu thô đã trải qua quy trình **Làm sạch (Data Cleaning)**: chuẩn hóa tên cột tiếng Việt sang tiếng Anh, xử lý định dạng ngày tháng và chuyển đổi dữ liệu tiền tệ.
* **Lưu ý:** Các trường thông tin định danh khách hàng (*Tên, Số điện thoại*) bị trống trong phần lớn giao dịch, do đó phân tích về khách hàng thân thiết (Retention) sẽ bị hạn chế.

---
# TỔNG HỢP PHÂN TÍCH SO SÁNH & CÁC INSIGHT QUAN TRỌNG

Dựa trên sự so sánh trực tiếp giữa dữ liệu của cửa hàng cụ thể (`df_specific_store`) và toàn bộ hệ thống (`df_all_stores`), dưới đây là báo cáo chi tiết kèm biểu đồ minh họa.

## 1. Phân Tích Hiệu Suất Sản Phẩm (Product Performance)

### 🏆 Top 10 Sản Phẩm Bán Chạy Nhất (Theo Số Lượng & Doanh Thu)
* **Sự Tương Đồng Đáng Kinh Ngạc:** Có sự tương đồng gần như tuyệt đối trong bảng xếp hạng Top 10 sản phẩm bán chạy nhất giữa cửa hàng lẻ và toàn chuỗi.
* **Sản Phẩm "Ngôi Sao":** Các món như **"CÀ PHÊ SỮA" ĐÁ**, **"CÀ PHÊ ĐEN" ĐÁ**, **"BẠC XỈU" ĐÁ**, và **BỮA TRƯA NO NÊ** liên tục giữ vững vị trí dẫn đầu.
* **Mối Tương Quan Dữ Liệu:** Tổng số lượng và doanh thu của hầu hết các mặt hàng gần như giống hệt nhau ở cả hai tập dữ liệu.

![Biểu đồ Top 10 Sản phẩm Bán chạy nhất](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/b%C3%A1n%20ch%E1%BA%A1yythoe%20s%E1%BB%91%20l%C6%B0%E1%BB%A3ng.png)
![Chi tiết doanh thu theo từng món](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/B%C3%A1n%20ch%E1%BA%A1y%20theo%20doanh%20thu.png)

### 📂 Top 5 Danh Mục Bán Chạy Nhất (Theo Tổng Doanh Thu)
* **Danh Mục Dẫn Đầu:** Tương tự như sản phẩm lẻ, thứ hạng của 5 danh mục hàng đầu cũng trùng khớp hoàn toàn. **COFFEE**, **TEA**, **Combo**, **ĐỒ ĂN TRƯA**, và **ICED-BLENDED/SMOOTHIES** là những nhóm đóng góp doanh thu lớn nhất.
* **Kết Luận:** Cơ cấu doanh thu theo danh mục của cửa hàng lẻ mang tính đại diện cao cho toàn bộ mạng lưới.

![Biểu đồ Tỷ trọng Doanh thu theo Danh mục](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/5%20m%E1%BB%A5c%20b%C3%A1n%20ch%E1%BA%A1yynhaats%20theo%20doanh%20thu.png)

---

## 2. Xu Hướng Kinh Doanh & Hành Vi Khách Hàng (Sales Trends & Behavior)

### 📅 Xu Hướng Doanh Thu Theo Tháng
* **Biến Động Đồng Nhất:** Xu hướng doanh thu qua các tháng 3, 4, 5, 6 là gần như y hệt nhau ở cả hai tập dữ liệu.
* **Thứ Tự Hiệu Suất:** Tháng 3 > Tháng 5 > Tháng 6 > Tháng 4.
* **Insight:** Có một mô hình kinh doanh mang tính chu kỳ hoặc mùa vụ nhất quán trên toàn hệ thống.

![Biểu đồ Xu hướng Doanh thu theo Tháng](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/xu%20h%C6%B0%E1%BB%9Bng%20h%C3%A0ng%20th%C3%A1ng.png)

### 🗓️ Hiệu Suất Theo Ngày Trong Tuần (Day of Week Analysis)
* **Mô Hình "Văn Phòng":** Doanh thu cao nhất vào **Thứ Tư**, theo sau là Thứ Ba, Thứ Năm, Thứ Sáu.
* **Cuối Tuần Thấp Điểm:** Thứ Bảy và Chủ Nhật ghi nhận mức doanh thu thấp hơn.
* **Insight:** Hành vi khách hàng rất đồng nhất: tập trung mua sắm vào giữa tuần (phục vụ công việc) và giảm vào cuối tuần.

![Biểu đồ Phân bổ Doanh thu theo Thứ trong Tuần](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/hi%E1%BB%87u%20su%E1%BA%A5t%20b%C3%A1n%20h%C3%A0ng%20ng%C3%A0y%20trong%20tu%E1%BA%A7n.png)

### 💳 Phương Thức Thanh Toán & Nguồn Đơn Hàng
* **Thanh Toán:** Cơ cấu thanh toán giống hệt nhau với sự thống trị của **CASH (Tiền mặt)**, theo sau là ATM, TRANSFER, và MOMO.
* **Nguồn Đơn:** **"TẠI CHỖ" (On-site)** chiếm tỷ trọng áp đảo, tiếp đến là "MANG VỀ" và "GOJEK".

![Biểu đồ Tỷ lệ Phương thức Thanh toán](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/Ph%C6%B0%C6%A1ng%20th%E1%BB%A9c%20thanh%20to%C3%A1n%20ph%E1%BB%95%20bi%E1%BA%BFn.png)
![Biểu đồ Nguồn đơn hàng](https://github.com/CuongDAol/salecoffeandtee/blob/02b53e2735187a68fbd8de920c52992aabf7ce4d/Ngu%E1%BB%93n%20h%C3%A0ng%20ph%E1%BB%95%20bi%E1%BA%BFn.png)

### 🏷️ Tác Động Của Khuyến Mãi (Promotions Impact)
* **Hiệu Quả Tích Cực:** Giá trị trung bình đơn hàng (AOV) có áp dụng khuyến mãi (~44,419 VND) cao hơn một chút so với đơn hàng không khuyến mãi (~43,144 VND).
* **Kết Luận:** Chiến lược khuyến mãi có hiệu quả tích cực và nhất quán trong việc nâng cao giá trị giao dịch.

![BieudoBieudo](https://github.com/CuongDAol/salecoffeandtee/blob/a1c45594af7d42f7400ff5acc987e1ad5fb41160/Gi%C3%A1%20tr%E1%BB%8B%20giao%20d%E1%BB%8Bchhtrung%20%20b%C3%ACnh.png)
---

## 💡 ĐỀ XUẤT HÀNH ĐỘNG CỤ THỂ (ACTION PLAN)

Dựa trên các insight trên, dưới đây là các đề xuất chiến lược để tối ưu hóa hoạt động và tăng trưởng doanh thu:

### 1. 🚀 Chiến Lược Sản Phẩm (Product Strategy)
* **Củng Cố "Sản Phẩm Lõi":** Đảm bảo nguồn cung ứng không bao giờ gián đoạn cho bộ tứ "Best-sellers": *Cà phê Sữa đá, Cà phê Đen đá, Bạc Xỉu đá, Bữa Trưa No Nê*.
* **Khai Thác Danh Mục Tiềm Năng:** Phát triển thêm các biến thể mới hoặc Combo hấp dẫn trong các nhóm chủ lực (Coffee, Tea, Smoothie) để đa dạng hóa lựa chọn cho khách hàng.

### 2. ⚙️ Tối Ưu Hóa Vận Hành & Nhân Sự (Operations Optimization)
* **Quản Lý Tồn Kho Thông Minh:** Điều chỉnh mức tồn kho linh hoạt theo xu hướng tháng (giảm nhập hàng vào tháng 4, 6; tăng vào tháng 3, 5) để tối ưu dòng tiền và giảm lãng phí.
* **Nhân Sự Theo Nhu Cầu:**
    * **Tăng cường:** Bố trí nhân sự tối đa vào **Giữa tuần (Thứ 3, 4, 5)** để đảm bảo tốc độ phục vụ.
    * **Tinh gọn:** Giảm bớt nhân sự vào **Cuối tuần (Thứ 7, CN)** để tiết kiệm chi phí.

### 3. 🤝 Chiến Lược Khách Hàng & Khuyến Mãi (Customer & Promo)
* **Mở Rộng Khuyến Mãi:** Tiếp tục và đẩy mạnh các chương trình Voucher/Khuyến mãi vào các giai đoạn thấp điểm.
* **Xây Dựng Loyalty Program (Cấp Thiết):** Triển khai ngay chương trình thành viên để thu thập data (Tên, SĐT), làm cơ sở cho việc chăm sóc khách hàng và tăng tỷ lệ quay lại.
