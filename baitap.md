# BÁO CÁO THIẾT LẬP KHÔNG GIANG CỘNG TÁC DOANH NGHIỆP (ENTERPRISE WORKSPACE)
> **Dự án:** Bãi Đỗ Xe Thông Minh (Smart Parking System)  

---

## 1. Sơ đồ kiến trúc kênh (Channel / Topic Architecture)

Hệ thống được thiết lập trên **Lark / Slack** nhằm phân tách rõ ràng luồng thông tin, loại bỏ tình trạng trôi tin nhắn và nhiễu dữ liệu kỹ thuật:

| Tên Kênh / Topic | Loại Kênh | Quy định Nội dung & Phạm vi Sử dụng |
| :--- | :---: | :--- |
| **`#announcements`** | *Read-Only* | **Chỉ dành cho Lead/Admin:** Thông báo quan trọng về dự án, lịch họp, thay đổi quy trình, chốt deadline. Thành viên không nhắn tin tán gẫu tại đây. |
| **`#tech-hardware-sensor`** | *Public* | **Thảo luận Kỹ thuật Cảm biến:** Luồng dữ liệu cảm biến, tín hiệu IoT, sơ đồ mạch, kết nối phần cứng bãi đỗ xe. |
| **`#tech-software-dev`** | *Public* | **Thảo luận Phần mềm:** Source code, API backend/frontend, xử lý lỗi (bugs), tích hợp hệ thống quản lý xe. |
| **`#general-discussion`** | *Public* | **Thảo luận chung:** Các vấn đề liên quan đến vận hành nhóm, trao đổi bất đồng bộ không thuộc riêng mảng kỹ thuật. |
| **`#watercooler-memes`** | *Public* | **Giải trí & Tán gẫu:** Chia sẻ tin tức ngoài lề, meme hài hước, giao lưu thư giãn. **Tuyệt đối không bàn công việc/kỹ thuật tại đây.** |

---

## 2. Bản quy ước giao tiếp bất đồng bộ (Asynchronous Communication Rules)

Áp dụng **3 Quy Tắc Vàng** giúp duy trì sự tập trung tối đa cho đội ngũ phát triển (Developers):

### 📌 Quy tắc 1: Khai tử bẫy "No-Hello" (No-Hello Trap)
* **Nội dung:** Không nhắn các câu chào hỏi trống không như *"Hi"*, *"Anh ơi"*, *"Alo"* rồi chờ đối phương trả lời mới nói tiếp.
* **Thực hành:** Gộp **Chào hỏi + Bối cảnh + Nội dung cần hỗ trợ/câu hỏi + Tài liệu đính kèm (nếu có)** vào trong **01 tin nhắn duy nhất**. Người nhận sẽ đọc và phản hồi đầy đủ ngay khi họ hoàn thành công việc đang dở dang.

### 📌 Quy tắc 2: Kỷ luật dùng Reply in Thread & Gắn nhãn Mức độ Khẩn cấp
* **Reply in Thread:** 100% thảo luận chi tiết cho một vấn đề, thông báo lỗi cảm biến hoặc câu hỏi kỹ thuật **phải** được thực hiện qua tính năng **Reply in Thread** (Trả lời theo luồng) của tin nhắn gốc. Giữ cho khung chat chính luôn gọn gàng.
* **Gắn nhãn mức độ (Prefixing):** Đặt tiền tố ở đầu tin nhắn để người nhận chủ động sắp xếp thời gian phản hồi:
  * `[FYI]` (For Your Information): Tin nhắn đọc để biết, không cần rep.
  * `[Non-Urgent]`: Câu hỏi/góp ý, xử lý khi rảnh.
  * `[URGENT]`: Vấn đề sự cố nghiêm trọng (Hotfix/Blocker), cần xử lý ưu tiên.

### 📌 Quy tắc 3: Kiểm soát thông báo & Sử dụng `@mention` có trách nhiệm
* **Cấm spam `@all` / `@channel`:** Chỉ Trưởng nhóm (Leader) mới được dùng `@all` / `@channel` cho các thông báo khẩn cấp tại kênh `#announcements`.
* **Tôn trọng Focus Time:** Khuyến khích lập trình viên bật chế độ **Do Not Disturb (DND)** hoặc **Focus Mode** khi gõ code. Đội ngũ mặc định làm việc bất đồng bộ (Asynchronous): Tin nhắn gửi đi không bắt buộc phải nhận lại phản hồi lập tức, thời gian phản hồi tiêu chuẩn là trong vòng **2–4 giờ làm việc**.

---

## 3. Kịch bản giải quyết Bẫy dữ liệu (Edge Case / Data Trap)

* **Vấn đề bẫy:** Tình trạng ép rep lập tức (Real-time pressure) làm đứt gãy luồng tư duy (Context Switching) của Developer khi đang viết code.
* **Giải pháp xử lý:**
  1. **Quy định khung giờ Focus Time:** Thiết lập cố định 2 khoảng thời gian trong ngày (VD: `09:00 - 11:30` và `14:00 - 16:30`) là thời gian tập trung cao độ, tắt toàn bộ thông báo ứng dụng chat.
  2. **Quy trình Escalate cho sự cố khẩn cấp:** Nếu hệ thống/cảm biến gặp sự cố sập thực sự (`[URGENT]`), thay vì nhắn tin spam trên kênh chat, thành viên sẽ kích hoạt kênh liên lạc dự phòng khẩn cấp bằng cách **Gọi điện trực tiếp**. Nếu không có cuộc gọi, mặc định mọi tin nhắn chat được xử lý theo cơ chế bất đồng bộ.
