# Dự án Dự đoán Khả năng Vỡ Nợ Tín Dụng (Credit Default Prediction)

Dự án này tập trung vào việc xây dựng các mô hình dự đoán khả năng khách hàng vỡ nợ, bao gồm mô hình scorecard truyền thống và các mô hình machine learning hiện đại như XGBoost và LightGBM. Dự án bao gồm các bước khám phá dữ liệu, xử lý biến, lựa chọn đặc trưng và đánh giá mô hình.

---

## 🔍 Khám phá Dữ liệu (EDA)

- Thực hiện phân tích đơn biến (univariate) và phân tích hai biến (bivariate).
- Vẽ biểu đồ phân phối và heatmap tương quan giữa các biến.
- Phát hiện:
  - Một số biến có tỷ lệ thiếu dữ liệu (missing) đáng kể, có dấu hiệu thuộc dạng **MNAR** (Missing Not At Random).
  - Có mối tương quan cao giữa hai biến → loại bỏ một biến để tránh đa cộng tuyến.
- Cách xử lý missing:
  - Tạo **bin riêng cho giá trị thiếu** khi thực hiện binning.
  - Tạo **biến (missing flag)** để đánh dấu sự hiện diện của dữ liệu thiếu.

---

## 🧮 Xây dựng Mô hình Scorecard Tín dụng

- Thực hiện **binning** các biến đầu vào.
- Tính **WOE (Weight of Evidence)** cho các bin và sử dụng WOE làm đầu vào cho mô hình.
- Huấn luyện mô hình **logistic regression** trên các biến đã WOE.
- Kết quả cho thấy đây là mô hình scorecard tốt: 
  - **AUROC**: 0.9025
  - **KS Statistic**: 0.6578
  - **Gini**: 0.8049
  - **PSI (Population Stability Index)**: 0.0022 → cho thấy mô hình ổn định theo thời gian.
- Thử loại bỏ các biến có giá trị **IV thấp** nhưng không cải thiện được các chỉ số → giữ nguyên tập biến ban đầu.

---

## 🤖 Xây dựng Mô hình Machine Learning (XGBoost và LightGBM)

- Xây dựng mô hình phân loại sử dụng **XGBoost** và **LightGBM**.
- Thực hiện **lựa chọn đặc trưng** bằng phương pháp **backward feature selection**.
- Sử dụng **Optuna** để tối ưu siêu tham số.
- Kết quả:
  - **XGBoost**:
    - AUROC: 0.96  
    - Brier Score: 0.060  
  - **LightGBM**:
    - AUROC: 0.95  
    - Brier Score: 0.064  

→ Cả hai mô hình đều có khả năng phân loại tốt và độ dự đoán xác suất đáng tin cậy.

---


