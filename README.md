# Tiểu luận cuối kỳ - Môn Mạng cảm biến (ELE1421)

## Đề tài: Phát hiện dụng cụ y tế (ống tiêm, nhiệt kế, khẩu trang, gạc) sử dụng TinyML

**Học viện:** Học viện Công nghệ Bưu chính Viễn thông (PTIT) - Cơ sở TP. Hồ Chí Minh

**Giảng viên hướng dẫn:** ThS. Hồ Nhựt Minh

**Sinh viên thực hiện:** Cao Phong

**MSSV:** N23DCCI058

**Lớp:** D23CQCI01-N

---

## Giới thiệu đề tài

Dự án ứng dụng mô hình học sâu (Deep Learning) dựa trên kiến trúc **FOMO (Faster Objects, More Objects)** kết hợp **MobileNetV2** làm backbone và phương pháp **Transfer Learning** trên nền tảng **Edge Impulse** nhằm phát hiện (Object Detection) 4 loại dụng cụ y tế:

* 🩹 Gạc y tế (Gauze)
* 😷 Khẩu trang y tế (Mask)
* 💉 Kim tiêm (Syringe)
* 🌡️ Nhiệt kế (Thermometer)

Mô hình sau khi huấn luyện được lượng tử hóa sang định dạng **INT8**, đóng gói dưới dạng **WebAssembly (WASM)** và **C++ Library**, cho phép thực thi suy luận trực tiếp trên trình duyệt hoặc thiết bị nhúng mà không cần kết nối Internet.

### Mục tiêu

* Xây dựng hệ thống nhận diện dụng cụ y tế sử dụng TinyML.
* Tối ưu mô hình cho thiết bị có tài nguyên hạn chế.
* Đảm bảo khả năng xử lý thời gian thực (Real-time Inference).
* Bảo vệ quyền riêng tư thông qua xử lý trực tiếp trên thiết bị (On-device AI).

---

## Bộ dữ liệu

Bộ dữ liệu gồm **173 ảnh** được thu thập và gán nhãn thủ công bằng Bounding Box.

| Nhãn        | Số lượng |
| ----------- | -------- |
| Gauze       | ~35      |
| Mask        | ~35      |
| Syringe     | ~35      |
| Thermometer | ~35      |
| Background  | ~33      |

### Chia dữ liệu

* Training Set: 83%
* Testing Set: 17%

### Tiền xử lý

* Kích thước ảnh: 96 × 96 pixels
* Color Depth: RGB
* Resize Mode: Fit Shortest Axis
* Data Augmentation: Enabled

---

## Kết quả huấn luyện

### Hiệu năng tổng thể

| Chỉ số    | Giá trị |
| --------- | ------- |
| F1-Score  | 83.7%   |
| Precision | 98%     |
| Recall    | 54%     |

### Kết quả theo từng lớp

| Lớp             | F1-Score |
| --------------- | -------- |
| 😷 Mask         | 100%     |
| 🌡️ Thermometer | 83%      |
| 💉 Syringe      | 81%      |
| 🩹 Gauze        | 78%      |
| ⬜ Background    | 100%     |

---

## Hiệu năng triển khai

Sau khi lượng tử hóa INT8:

| Thông số       | Giá trị |
| -------------- | ------- |
| Inference Time | 7 ms    |
| RAM Usage      | 4.0 KB  |
| Flash Usage    | 81.4 KB |

Mô hình có khả năng chạy trên các vi điều khiển ARM Cortex-M và các nền tảng TinyML tương tự.

---

## Cấu trúc thư mục

```text
.
├── edge-impulse-sdk/
├── model-parameters/
├── tflite-model/
├── browser/
│   ├── index.html
│   └── app.js
├── .gitignore
└── README.md
```

> Nếu export dưới dạng C++ Library thì có thể xuất hiện thêm các tệp như `CMakeLists.txt` hoặc thư mục dành cho Arduino.

---

## Hướng dẫn chạy dự án

### Yêu cầu

* Google Chrome / Microsoft Edge
* Visual Studio Code
* Extension Live Server

### Khởi chạy

1. Clone repository:

```bash
git clone <repository-url>
```

2. Mở thư mục dự án bằng VS Code.

3. Mở file:

```text
browser/index.html
```

4. Chọn:

```text
Open with Live Server
```

5. Truy cập:

```text
http://127.0.0.1:5500/browser/index.html
```

6. Dán chuỗi Raw Features từ Edge Impulse hoặc sử dụng camera để kiểm thử thời gian thực.

---

## Đóng góp của đề tài

* Xây dựng quy trình TinyML hoàn chỉnh từ thu thập dữ liệu đến triển khai thực tế.
* Chứng minh khả năng triển khai Object Detection trên thiết bị nhúng tài nguyên thấp.
* Ứng dụng thành công WebAssembly để kiểm thử mô hình AI trên trình duyệt.
* Đảm bảo quyền riêng tư nhờ xử lý hoàn toàn trên thiết bị.
* Tạo nền tảng cho các ứng dụng y tế thông minh chi phí thấp.

---

## Liên kết

**Edge Impulse Project**

https://studio.edgeimpulse.com/public/89078/latest

**GitHub Repository**

https://github.com/<your-repository>

---

## Tài liệu tham khảo

1. Edge Impulse Documentation
2. FOMO - Faster Objects, More Objects
3. MobileNetV2: Inverted Residuals and Linear Bottlenecks
4. TensorFlow Lite for Microcontrollers

---

## Giấy phép

Dự án được thực hiện cho mục đích học tập và nghiên cứu tại Học viện Công nghệ Bưu chính Viễn thông (PTIT).
