# Marketing Claims Audit

## Ghi chú phạm vi

- `Trang giới thiệu chính`: dùng copy từ `A20-App-116/src/frontend/src/pages/Landing.tsx` và `src/frontend/index.html`.
- `Bài pin trên MXH`: dùng `2A202600346_VuQuangPhuc_Lab19/twitter_pitch.md`.
- `Slide "What we do" Day 19`: không thấy file slide riêng trong workspace, nên dùng phần `THE SOLUTION` trong `2A202600346_VuQuangPhuc_Lab20/milestone1_package.md` làm proxy gần nhất.

## Bảng audit

| Câu gốc | Mức | Evidence | Honest version |
|---|---|---|---|
| `[Landing] "AI Career Advisor Assistant tổng hợp dữ liệu công khai từ các nền tảng tuyển dụng, cung cấp insight aggregate có nguồn tham khảo và cập nhật hàng tuần"` | B | Landing/FAQ nói như vậy, nhưng repo cho thấy `marketData.ts` và `CitedSourcesPanel.tsx` còn dùng mock; `roadmap_nnl.md` cũng ghi chat + pipeline thật vẫn đang hoàn thiện. | AI Career Advisor Assistant là MVP đang hướng tới việc tổng hợp dữ liệu công khai thành insight aggregate có nguồn; chu kỳ cập nhật tuần là mục tiêu vận hành khi pipeline ổn định. |
| `[Landing stat] "7 ngày Chu kỳ cập nhật"` | C | `FAQ.tsx` nói pipeline chạy mỗi tuần, nhưng `roadmap_nnl.md` ghi pipeline scheduled còn cần khoảng 2-3 tháng để chạy ổn định. | Mục tiêu hiện tại là refresh theo chu kỳ tuần; bản demo chưa chứng minh được lịch chạy ổn định 7 ngày/lần trên dữ liệu thật. |
| `[Landing stat] "100% Có nguồn tham khảo"` | C | Có UI cho citation, nhưng `CitedSourcesPanel.tsx` đang dùng `MOCK_CITATIONS`; chưa có đo lường chứng minh mọi output đều có nguồn. | Chúng tôi ưu tiên gắn nguồn cho câu trả lời khi có thể; độ phủ nguồn trên toàn bộ output vẫn cần kiểm chứng trên dữ liệu thật. |
| `[Landing stat] "4+ Nền tảng"` | C | UI/FAQ nhắc 4 nguồn, footer PDF còn nhắc 5 nguồn, nhưng backend hiện chỉ thấy rõ 3 crawler source: `topcv`, `linkedin`, `indeed`. | Demo hiện tham chiếu nhiều nguồn tuyển dụng công khai; repo hiện thể hiện rõ 3 crawler backend và kế hoạch mở rộng thêm nguồn sau khi pipeline ổn định. |
| `[Landing] "AI Career Advisor Assistant tự động tổng hợp, chuẩn hoá và phân tích dữ liệu công khai"` | B | Repo có ingestion/processing pipeline và Medallion flow, nhưng `roadmap_nnl.md` nói end-to-end integration vẫn đang làm. | Chúng tôi đang xây pipeline để tự động tổng hợp và chuẩn hoá dữ liệu công khai; bản hiện tại mới chứng minh được một phần luồng đó. |
| `[Landing] "Mỗi con số có nguồn tham khảo"` | C | Chat có panel nguồn, nhưng dashboard dùng số mock trong `marketData.ts`; chưa có bằng chứng mọi KPI/biểu đồ đều truy vết được về nguồn thật. | Ở phần chat, sản phẩm được thiết kế để trả lời kèm nguồn; các KPI và dashboard demo vẫn cần nối provenance dữ liệu thật trước khi có thể hứa "mỗi con số". |
| `[Landing] "Pipeline minh bạch... Không hộp đen"` | B | Trong repo có mô tả rõ các bước `fetch -> normalize -> aggregate`, nhưng chưa thấy user-facing audit trail hoàn chỉnh trong sản phẩm. | Kiến trúc pipeline đã được mô tả rõ trong repo; trải nghiệm audit cho người dùng cuối vẫn cần hoàn thiện thêm. |
| `[Landing anti-pitch] "Chúng tôi cung cấp insight aggregate đã được phân tích để cố vấn nghề nghiệp ra quyết định - không thay thế quyết định đó."` | A | Claim này nhất quán với Landing, FAQ và `Lab17/submission.md` phần non-goals/human-in-the-loop. | Chúng tôi cung cấp insight aggregate để hỗ trợ quyết định của cố vấn nghề nghiệp, không thay thế quyết định đó. |
| `[Pinned post] "ChatGPT gives uncited answers"` | C | Đây là so sánh sweeping với sản phẩm khác nhưng không có test, benchmark, hay điều kiện sử dụng cụ thể trong repo. | Các công cụ chat chung thường chưa cho advisor lớp nguồn và mốc cập nhật đủ rõ để dùng ngay trong tư vấn. |
| `[Pinned post] "AI Career Advisor Assistant turns 4+ public platforms into weekly refreshed, source-cited market insight in 1-5 minutes"` | C | Gộp 4 claim mạnh cùng lúc (`4+ platforms`, `weekly refreshed`, `source-cited`, `1-5 minutes`) trong khi repo vẫn còn mock data và roadmap ghi nhiều phần đang hoàn thiện. | AI Career Advisor Assistant hướng tới việc giúp advisor tra cứu insight từ nhiều nguồn công khai nhanh hơn cách tổng hợp thủ công; thời gian thực tế và độ phủ nguồn cần được đo thêm trong pilot. |
| `[What we do] "Chatbot Agent trả lời bằng ngôn ngữ tự nhiên, kèm trích dẫn nguồn JD gốc (link, platform badge)"` | B | UI citation đã có thật trong `CitedSourcesPanel.tsx`, nhưng `roadmap_nnl.md` nói vẫn đang thay mock citations bằng structured JSON từ hybrid search engine. | Bản demo đã có giao diện citation; chúng tôi đang hoàn thiện luồng để citation lấy từ kết quả tìm kiếm thật thay vì dữ liệu mẫu. |
| `[What we do] "Chúng tôi có pipeline crawl JD thật từ 5 nền tảng, aggregate insight có nguồn"` | C | Investor package nói 5 nền tảng, nhưng backend source hiện thấy rõ 3 crawler; thêm nữa dữ liệu dashboard/chat vẫn chưa nối full với dữ liệu thật. | Khác biệt hiện tại là chúng tôi đang xây pipeline aggregate từ dữ liệu JD công khai; độ phủ nguồn và mức vận hành đa nền tảng vẫn đang được hoàn thiện. |
| `[What we do] "Hybrid Search (0.7 Vector + 0.3 Keyword) + Reranker cho kết quả chính xác"` | B | `test_hybrid_search.py` xác nhận weighting 0.7/0.3 có trong code; tuy vậy chưa có benchmark người dùng hay evaluation set nào chứng minh chữ "chính xác". | Hệ thống đã có hybrid search và reranker; độ chính xác thực tế vẫn cần benchmark với truy vấn thật của career advisor. |
| `[Pitch memo] "The current product promise is a 7-day refresh cycle, 100% cited outputs, coverage across 4+ job platforms, and 1-5 minute time-to-insight"` | C | Đây là promise tốt để pitch, nhưng evidence trong repo cho thấy scheduled pipeline, citation thật, multi-source coverage và timing thực tế đều chưa được validate end-to-end. | Phiên bản hiện tại mới ở mức promise của MVP: muốn đạt refresh theo tuần, trả lời có nguồn, mở rộng đa nguồn và rút ngắn time-to-insight; các điểm này cần được xác thực qua pilot. |

## Tự kiểm tra conversion

Có, trang giới thiệu sau khi sửa vẫn có thể convert nếu giữ 3 ý mạnh sau:

- Nỗi đau rất rõ: advisor vẫn mất nhiều giờ tổng hợp thủ công.
- Giá trị vẫn rõ: insight aggregate có nguồn, dành riêng cho một nhóm người dùng cụ thể.
- Sự tin cậy tăng lên: bỏ các tuyệt đối như `100%`, `1-5 phút`, `4+/5 nền tảng`, thay bằng ngôn ngữ minh bạch sẽ làm pitch bớt rủi ro pháp lý và đáng tin hơn.
