# Territorial Scope

## Giả định làm bài

Tôi dùng **phạm vi sản phẩm hiện tại** từ Day 17 + Day 20-21: `AI Career Advisor Assistant` phục vụ chủ yếu cho **career advisors / HR tại Việt Nam**.  
Day 16 có phiên bản sớm nhắm đến sinh viên IT, nhưng các tài liệu sau đó đã pivot khá rõ sang nhóm cố vấn nghề nghiệp và tổ chức tại Việt Nam.

---

## 1. Câu hỏi 1: User EU?

**Có 1 user EU không?**  
Hiện **chưa thấy bằng chứng** trong PRD, pitch, risk register hay codebase rằng sản phẩm đang có user EU.

**Có kế hoạch mở rộng EU trong 12 tháng tới không?**  
Hiện **không thấy** kế hoạch go-to-market EU. Tất cả tài liệu gần nhất đều nói đến:
- trường đại học / career center / HR tại Việt Nam
- dữ liệu thị trường việc làm Việt Nam
- domain và messaging phục vụ thị trường Việt Nam

**Kết quả: EU AI Act áp dụng – KHÔNG (ở trạng thái hiện tại).**  
Lập luận: theo phạm vi hiện tại, sản phẩm chưa được đặt lên thị trường EU, chưa nhắm tới user ở EU, và chưa có dấu hiệu output đang được dùng trong EU.  
**Cảnh báo:** nếu trong 12 tháng tới có pilot với trường, advisor hoặc user ở EU, hoặc output của hệ thống được dùng trong EU, kết luận này phải mở lại ngay.

---

## 2. Câu hỏi 2: Dữ liệu Việt Nam?

### 5 loại dữ liệu cá nhân đang xử lý

1. **Tên người dùng**  
   Dấu vết: `domain/user/models.py`

2. **Email người dùng**  
   Dấu vết: `domain/user/models.py`, `domain/user/service.py`

3. **Mã định danh tài khoản / Cognito sub / user_id**  
   Dấu vết: `domain/user/models.py`, `domain/chat/models.py`, `domain/cv/models.py`

4. **Nội dung hội thoại và hành vi sử dụng**  
   Dấu vết: `domain/chat/models.py`, audit/chat session models

5. **Dữ liệu hồ sơ nghề nghiệp / CV / kỹ năng / kỳ vọng lương**  
   Dấu vết: `domain/cv/models.py`, `domain/user/models.py`

**Có thêm dấu hiệu xử lý dữ liệu vị trí** trong luồng matching/job profile, nên nếu feature này bật thật thì vị trí nên được đưa vào data inventory chính thức.

### Có chuyển dữ liệu ra nước ngoài không?

**Có, khả năng cao là CÓ.**

Lý do:
- `llm_client.py` gọi **Gemini**, **OpenRouter** và **OpenAI**
- auth dùng **AWS Cognito**
- theo cách định nghĩa của PDPL, dùng hệ thống đặt ngoài lãnh thổ Việt Nam để xử lý dữ liệu cá nhân của công dân Việt Nam được xem là **chuyển dữ liệu cá nhân ra nước ngoài**

### Kết quả

- **PDPL áp dụng: CÓ**
- **Có cần đánh giá tác động chuyển dữ liệu ra nước ngoài: CÓ**

Lập luận ngắn: sản phẩm xử lý dữ liệu cá nhân của người dùng Việt Nam, và một phần xử lý đang đi qua nhà cung cấp/hệ thống nước ngoài, nên không nên giả định đây chỉ là “dùng API” đơn thuần.

---

## 3. Câu hỏi 3: Tầng rủi ro Luật AI VN?

**Kết quả: CAO**

**1 câu lập luận:**  
Theo heuristic của workshop, hệ thống này chạm **giáo dục / hướng nghiệp** vì nó hỗ trợ career advisors tại trường đại học đưa ra insight và định hướng cho sinh viên; do đó nên xếp **rủi ro cao**, dù chưa chạm y tế hay tài chính.

**Note thực hành:**  
Nếu sau này sản phẩm thu hẹp đúng nghĩa thành công cụ “market insight aggregate only”, không can dự vào tư vấn cá nhân hay quyết định học tập cụ thể, mức rủi ro thực tế có thể cần đánh giá lại. Nhưng với mô tả sản phẩm hiện tại, nên chọn phương án bảo thủ là **Cao**.

---

## 4. Lịch: 4 deadline cụ thể

1. **12/05/2026** – Chốt territorial scope bản nội bộ: `Vietnam-first, not launching to EU in next 12 months`
2. **15/05/2026** – Hoàn thành data inventory + map 5 loại dữ liệu cá nhân đang xử lý
3. **20/05/2026** – Hoàn thành hồ sơ draft đánh giá tác động chuyển dữ liệu cá nhân ra nước ngoài theo PDPL
4. **27/05/2026** – Chốt risk tier AI nội bộ + cập nhật disclaimer, consent và human-in-the-loop note trên sản phẩm

---

## Nguồn tham chiếu nhanh

- PRD Day 17: `2A202600346_VuQuangPhuc_Lab17/submission.md`
- Customer scope Day 16: `2A202600346_VuQuangPhuc_Lab16/Day16_Submission.md`
- Stack hiện tại: `2A202600346_VuQuangPhuc_Lab21/risk_register_v2.md`, `A20-App-116/src/backend/app/ml/llm_client.py`
- EU AI Act scope: Regulation (EU) 2024/1689, Article 2  
  https://eur-lex.europa.eu/eli/reg/2024/1689/
- Vietnam PDPL: Decree 13/2023/ND-CP, especially Article 25 on cross-border transfer  
  https://thuvienphapluat.vn/van-ban/EN/Cong-nghe-thong-tin/Decree-No-13-2023-ND-CP-dated-April-17-2023-on-protection-of-personal-data/564343/tieng-anh.aspx
- Vietnam AI Law status / risk-based management:
  https://vanban.chinhphu.vn/?classid=1&docid=216334&pageid=27160&typegroupid=3
  https://xaydungchinhsach.chinhphu.vn/nhung-noi-dung-dang-chu-y-cua-luat-tri-tue-nhan-tao-119260212091614393.htm

> Đây là bản trả lời workshop để ra quyết định sản phẩm, không phải legal opinion chính thức.
