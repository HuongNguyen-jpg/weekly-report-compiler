# 🤖 Trợ lý biên tập báo cáo tuần

**Agent AI tự động tổng hợp thông tin công việc, tạo báo cáo tuần có cấu trúc và lưu thành tài liệu Feishu.**

## Định nghĩa ngắn

Mỗi chiều thứ Sáu, Agent tổng hợp thông tin trong tuần từ các nhóm chat Feishu, bảng theo dõi dự án, biên bản họp và ghi chú công việc; sắp xếp theo dự án, tạo báo cáo tuần trong tài liệu Feishu và gửi đường dẫn để người dùng xem.

Agent giúp giảm thời gian tìm lại tin nhắn, kiểm tra bảng và định dạng báo cáo. Người dùng vẫn xem xét nội dung và xác nhận trước khi sử dụng.

## Thời gian dự kiến mỗi tuần

| Công việc | Tự làm | Có Agent hỗ trợ |
|---|---:|---:|
| Xem lại tin nhắn nhóm | 15 phút | Tự động trích xuất |
| Kiểm tra bảng theo dõi dự án | 10 phút | Tự động đọc |
| Xem biên bản họp | 15 phút | Tự động tóm tắt |
| Viết và định dạng báo cáo | 15 phút | Tự động tạo |
| **Tổng cộng** | **Khoảng 60 phút/tuần** | **Khoảng 5 phút để rà soát** |

*Đây là ước tính trong mô tả dự án, chưa được xác minh độc lập.*

## Công cụ sử dụng

- **ZCode:** phát triển và gỡ lỗi Agent.
- **Hermes Agent:** quản lý cấu hình người dùng, lịch chạy và quy trình thực thi.
- **Feishu CLI và Bot:** kết nối Feishu để đọc hoặc ghi tài liệu, bảng biểu và gửi kết quả.
- **DeepSeek:** hiểu yêu cầu và tạo nội dung báo cáo.

## Nguồn dữ liệu đầu vào

- Tin nhắn trong các nhóm Feishu của dự án.
- Bảng đa chiều Feishu, gồm tiến độ dự án và trạng thái công việc con.
- Biên bản hoặc bản ghi cuộc họp từ Feishu Minutes hay Tencent Meeting.
- Ghi chú công việc người dùng gửi trực tiếp cho Bot.

## Quy trình xử lý

1. **Bắt buộc:** Trích xuất tin nhắn công việc trong nhóm có từ khóa trạng thái như “đã hoàn thành”, “đã bàn giao”.
2. **Bắt buộc:** Đọc các hàng trong bảng đa chiều có cập nhật trong tuần hiện tại.
3. **Khuyến nghị:** Trích xuất kết luận, việc cần làm và người phụ trách từ biên bản họp.
4. **Tùy chọn:** Tổng hợp ghi chú công việc người dùng gửi Bot mỗi ngày.
5. **Bắt buộc:** Sắp xếp nội dung theo dự án hoặc chủ đề, phân biệt kết quả đã bàn giao với kế hoạch tiếp theo.
6. **Bắt buộc:** Dùng bảng đa chiều làm căn cứ chính để đối chiếu trạng thái và kiểm tra tính nhất quán.
7. **Bắt buộc:** Tạo báo cáo có cấu trúc gồm kết quả, kế hoạch, vấn đề và nguồn tài liệu đính kèm.
8. **Bắt buộc:** Tạo tài liệu Feishu, kiểm tra quyền truy cập và cung cấp liên kết tài liệu.

## Cấu trúc báo cáo tuần

### 📊 Kết quả trong tuần

Liệt kê các việc đã hoàn thành theo từng dự án và trạng thái hiện tại.

### 📅 Kế hoạch tuần tới

Tổng hợp việc chưa hoàn thành và các kế hoạch đã được xác nhận.

### ⚠️ Vấn đề gặp phải

Ghi lại trở ngại, rủi ro và phương án xử lý đã có.

### 📎 Tài liệu và nguồn

Đính kèm liên kết cuộc họp, bảng dự án và tài liệu liên quan.

## Agent có thể làm

- Tự động trích xuất cập nhật công việc từ nhóm Feishu.
- Đọc bảng đa chiều dự án và tổng hợp trạng thái.
- Tóm tắt biên bản họp và danh sách việc cần làm.
- Phân loại nội dung theo dự án hoặc chủ đề.
- Tạo báo cáo tuần Feishu theo mẫu thống nhất.

## Giới hạn

- Không tự tạo thông tin tiến độ không có trong nguồn.
- Không sửa dữ liệu gốc trong bảng đa chiều.
- Không gửi bản nháp chưa được rà soát cho bên thứ ba nếu chưa có xác nhận.
- Không thay thế đánh giá của người quản lý.
- Khi dữ liệu thiếu nghiêm trọng, phải hỏi người dùng xác nhận.

## Cách sử dụng

Tìm Bot **Weekly Report Compiler** trong Feishu và gửi:

> Tạo báo cáo tuần

Có thể cấu hình để Agent tự chạy vào **17:00 mỗi thứ Sáu**.

## Lưu ý

- Người dùng cần kiểm tra và xác nhận nội dung tự động tạo trước khi sử dụng.
- Cần cấu hình sẵn các trường theo dõi dự án trong bảng đa chiều.
- Hiện chưa kết nối nội dung từ WeChat; tính năng này dự kiến hỗ trợ ở phiên bản sau.
- Không dùng Agent cho các quyết định nhân sự nhạy cảm.
- Báo cáo chỉ tổng hợp thông tin đã có. Nếu dữ liệu thiếu, trạng thái mâu thuẫn hoặc không rõ nguồn, cần ghi rõ và chuyển người dùng xác nhận; không suy đoán hoặc tự bổ sung tiến độ.

---

*Xây dựng trên Hermes Agent + Feishu Bot + DeepSeek · Tháng 8 năm 2026*
