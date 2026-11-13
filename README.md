# HCM-KS26-CNTT1_KNPromtingAl_Session02_Ex0Ẽ05
BÀI 5 – CƠ CHẾ IN-CONTEXT LEARNING TRONG PHÂN LOẠI REVIEW KHÁCH HÀNG

Họ và tên: Phạm Thành Đạo
Lớp: HCM-KS26-CNTT1
Môn học: Prompt Engineering

⸻

PHẦN 1. PHÂN TÍCH CƠ CHẾ IN-CONTEXT LEARNING (ICL)

1.1. In-Context Learning là gì?

In-Context Learning (ICL) là cơ chế cho phép mô hình AI học cách thực hiện một nhiệm vụ thông qua những thông tin, hướng dẫn và ví dụ được cung cấp trực tiếp trong Prompt mà không cần cập nhật trọng số hoặc huấn luyện lại mô hình.

Thay vì chỉ đưa ra một yêu cầu chung chung, người dùng cung cấp cho AI một số ví dụ đầu vào và kết quả đầu ra tương ứng. Từ đó, AI nhận diện quy luật và áp dụng cách xử lý tương tự cho dữ liệu mới.

1.2. Cơ chế hoạt động của ICL

ICL hoạt động thông qua các bước:

1. Tiếp nhận ngữ cảnh: AI đọc yêu cầu, hướng dẫn và các ví dụ được cung cấp trong Prompt.
2. Nhận diện quy luật: AI phân tích mối quan hệ giữa nội dung đầu vào và nhãn phân loại trong các ví dụ.
3. Học trong ngữ cảnh: AI sử dụng những quy luật vừa nhận diện để hiểu cách phân loại và sắc thái ngôn ngữ.
4. Dự đoán kết quả: Khi nhận được review mới, AI áp dụng quy luật đã nhận diện để đưa ra kết quả phù hợp.

1.3. Tại sao ICL không cần Train lại Model?

Điểm đặc biệt của ICL là mô hình không cần thay đổi các trọng số (Weights) đã được học trong quá trình huấn luyện trước đó.

Các ví dụ chỉ đóng vai trò là ngữ cảnh tạm thời được đưa vào đầu vào của mô hình. AI dựa vào ngữ cảnh này để điều chỉnh cách dự đoán trong lần phản hồi hiện tại.

Quá trình này không làm thay đổi kiến thức đã được lưu trong trọng số mô hình và không phải là một lần huấn luyện lại.

1.4. Vai trò của Few-shot Prompting

Few-shot Prompting là kỹ thuật cung cấp một số ví dụ mẫu trong Prompt để hướng dẫn AI thực hiện nhiệm vụ.

Trong bài toán TechShop, nếu chỉ sử dụng Zero-shot, AI có thể nhìn thấy các từ tích cực như “đẹp mê ly”, “đầm tay” và phân loại nhầm thành TÍCH CỰC.

Khi sử dụng Few-shot, AI được cung cấp những ví dụ về cách khách hàng dùng lời khen để thể hiện sự không hài lòng.

Nhờ đó, AI có thêm căn cứ để nhận diện:

* Mỉa mai: Nói ngược với ý nghĩa thực sự muốn truyền đạt.
* Nghĩa bóng: Sử dụng hình ảnh hoặc cách diễn đạt gián tiếp để thể hiện cảm xúc.
* Tiếng lóng công nghệ: Những cách diễn đạt như “nóng như lò”, “pin tụt như tụt quần”, “ship tốc độ rùa bò”.

Kết luận phần 1: In-Context Learning giúp AI thích nghi với nhiệm vụ thông qua ngữ cảnh và ví dụ mẫu. Few-shot Prompting là một cách ứng dụng ICL hiệu quả, đặc biệt trong các bài toán phân loại cảm xúc có chứa mỉa mai và nghĩa bóng.

⸻

PHẦN 2. THIẾT KẾ GIẢI PHÁP FEW-SHOT PROMPTING

2.1. Xây dựng 3 cặp ví dụ mẫu

Ví dụ 1 – Mỉa mai về nhiệt độ thiết bị

Input:

“Máy chạy mát thật đấy, mới mở game 10 phút mà CPU đã lên 98 độ, chắc có thể dùng thay lò sưởi mùa đông.”

Output:

* Sentiment: TIÊU CỰC.
* Reason: Khách hàng mỉa mai tình trạng máy quá nóng, dù sử dụng những từ ngữ có vẻ khen ngợi. Cụm từ “chạy mát thật đấy” mang ý nghĩa trái ngược với thực tế.

Ví dụ 2 – Mỉa mai về thời lượng pin

Input:

“Pin trâu quá shop ơi, vừa rút sạc được 30 phút đã phải cắm lại, đúng là công nghệ tiết kiệm pin đỉnh cao!”

Output:

* Sentiment: TIÊU CỰC.
* Reason: Khách hàng châm biếm thời lượng pin ngắn, không đáp ứng nhu cầu sử dụng. Những từ “pin trâu” và “đỉnh cao” chỉ là lời khen mỉa mai.

Ví dụ 3 – Mỉa mai về thời gian giao hàng

Input:

“Shop giao hàng nhanh như tên lửa, đặt từ tuần trước đến tuần này mới thấy shipper gọi, tốc độ phục vụ tuyệt vời!”

Output:

* Sentiment: TIÊU CỰC.
* Reason: Khách hàng mỉa mai vì thời gian giao hàng quá lâu. Cụm từ “nhanh như tên lửa” được sử dụng với ý nghĩa trái ngược thực tế.

⸻

PHẦN 3. PROMPT FEW-SHOT HOÀN CHỈNH

PROMPT FEW-SHOT – PHÂN LOẠI CẢM XÚC REVIEW KHÁCH HÀNG TECHSHOP
1. ROLE – VAI TRÒ
Bạn là chuyên viên Đảm bảo Chất lượng (QA) của công ty TechShop,
chuyên phân tích và phân loại cảm xúc trong các đánh giá sản phẩm công nghệ.
Bạn có khả năng nhận diện ngôn ngữ tự nhiên, lời nói mỉa mai,
nghĩa bóng, tiếng lóng và những cách diễn đạt cảm xúc gián tiếp.
2. CONTEXT – BỐI CẢNH
TechShop đang xử lý 5.000 đánh giá sản phẩm từ khách hàng.
Nhiệm vụ là phân loại mỗi đánh giá thành một trong hai nhãn:
- TÍCH CỰC: Khách hàng thực sự hài lòng với sản phẩm hoặc dịch vụ.
- TIÊU CỰC: Khách hàng không hài lòng, phàn nàn hoặc sử dụng lời khen
  mang tính mỉa mai.
3. TASK – NHIỆM VỤ
Đọc và phân tích nội dung review, xác định cảm xúc thực sự của khách hàng
thay vì chỉ dựa vào những từ ngữ tích cực hoặc tiêu cực xuất hiện trong câu.
Đặc biệt chú ý:
- Những câu khen nhưng mang hàm ý chê bai.
- Những câu sử dụng nghĩa bóng hoặc nói ngược.
- Tiếng lóng trong lĩnh vực công nghệ.
- Sự đối lập giữa lời nói và tình huống thực tế.
4. FEW-SHOT EXAMPLES – VÍ DỤ MẪU
Ví dụ 1: Nhiệt độ thiết bị
Input:
"Máy chạy mát thật đấy, mới mở game 10 phút mà CPU đã lên 98 độ,
chắc có thể dùng thay lò sưởi mùa đông."
Output:
{
  "sentiment": "TIÊU CỰC",
  "reason": "Khách hàng mỉa mai tình trạng máy quá nóng,
  dù sử dụng những từ ngữ có vẻ khen ngợi."
}
Ví dụ 2: Thời lượng pin
Input:
"Pin trâu quá shop ơi, vừa rút sạc được 30 phút đã phải cắm lại,
đúng là công nghệ tiết kiệm pin đỉnh cao!"
Output:
{
  "sentiment": "TIÊU CỰC",
  "reason": "Khách hàng châm biếm thời lượng pin ngắn,
  không đáp ứng nhu cầu sử dụng."
}
Ví dụ 3: Thời gian giao hàng
Input:
"Shop giao hàng nhanh như tên lửa, đặt từ tuần trước đến tuần này
mới thấy shipper gọi, tốc độ phục vụ tuyệt vời!"
Output:
{
  "sentiment": "TIÊU CỰC",
  "reason": "Khách hàng mỉa mai vì thời gian giao hàng quá lâu."
}
5. RULES – QUY TẮC PHÂN LOẠI
1. Phải xác định cảm xúc thực sự của khách hàng.
2. Không được chỉ dựa vào những từ tích cực như
   "đẹp", "tốt", "tuyệt vời", "đỉnh cao".
3. Nếu lời khen đi kèm tình huống thể hiện sự cố hoặc bất mãn
   thì phải xem xét khả năng mỉa mai.
4. Nếu khách hàng phàn nàn về nhiệt độ, pin hoặc giao hàng
   thì phân loại TIÊU CỰC.
5. Nếu khách hàng thực sự hài lòng và không có dấu hiệu phàn nàn
   thì phân loại TÍCH CỰC.
6. Không tự suy diễn những thông tin không xuất hiện trong review.
7. Nếu câu review không rõ nghĩa hoặc thiếu ngữ cảnh,
   vẫn chọn nhãn phù hợp nhất và ghi rõ mức độ không chắc chắn.
6. EXPECTED OUTPUT – ĐỊNH DẠNG ĐẦU RA
Trả kết quả dưới dạng JSON hợp lệ:
{
  "review": "Nội dung đánh giá",
  "sentiment": "TÍCH CỰC hoặc TIÊU CỰC",
  "reason": "Giải thích ngắn gọn lý do phân loại",
  "confidence": "CAO, TRUNG BÌNH hoặc THẤP"
}
Không thêm nội dung bên ngoài JSON.
7. INPUT – REVIEW CẦN PHÂN LOẠI
"Máy thiết kế đẹp mê ly, cầm rất đầm tay, mùa đông ôm máy chơi game
thì khỏi cần bật lò sưởi vì nhiệt độ CPU lên hẳn 98 độ C!"

⸻

PHẦN 4. KẾT QUẢ CHẠY THỬ VÀ ĐÁNH GIÁ

4.1. Kết quả phân loại mong đợi

{
  "review": "Máy thiết kế đẹp mê ly, cầm rất đầm tay, mùa đông ôm máy chơi game thì khỏi cần bật lò sưởi vì nhiệt độ CPU lên hẳn 98 độ C!",
  "sentiment": "TIÊU CỰC",
  "reason": "Khách hàng mỉa mai tình trạng máy quá nóng. Cụm từ khỏi cần bật lò sưởi thể hiện việc CPU đạt nhiệt độ 98 độ C, gây bất tiện khi sử dụng.",
  "confidence": "CAO"
}

4.2. Nhận xét kết quả

* AI nhận diện được sự mỉa mai trong câu đánh giá.
* Không bị đánh lừa bởi những từ ngữ tích cực như “đẹp mê ly” và “đầm tay”.
* Hiểu được ý nghĩa thực sự của cụm từ “khỏi cần bật lò sưởi”.
* Phân loại chính xác cảm xúc của khách hàng là TIÊU CỰC.

4.3. So sánh Zero-shot và Few-shot

Tiêu chí	Zero-shot	Few-shot
Ví dụ mẫu	Không có	Có 3 ví dụ
Nhận diện mỉa mai	Dễ nhầm	Được định hướng cụ thể
Hiểu nghĩa bóng	Hạn chế hơn	Có thêm ngữ cảnh
Nhận diện tiếng lóng	Có thể sai lệch	Được định hướng bằng ví dụ
Khả năng phân loại review	Phụ thuộc hướng dẫn chung	Có thêm mẫu tham chiếu

Nhận xét: Zero-shot dễ bị đánh lừa bởi những từ ngữ tích cực xuất hiện trong câu. Few-shot cung cấp các tình huống mẫu giúp AI nhận diện sự đối lập giữa lời khen và ý nghĩa thực tế, từ đó đưa ra kết quả phù hợp hơn.

⸻

PHẦN 5. KẾT LUẬN

Thông qua bài tập, em hiểu được cơ chế In-Context Learning cho phép AI thích nghi với nhiệm vụ mới thông qua ngữ cảnh và ví dụ được cung cấp trong Prompt mà không cần cập nhật trọng số mô hình.

Kỹ thuật Few-shot đặc biệt hữu ích trong việc phân loại cảm xúc khách hàng vì ngôn ngữ thực tế không phải lúc nào cũng thể hiện đúng cảm xúc thông qua những từ ngữ được sử dụng.

Đối với hệ thống TechShop, việc cung cấp các ví dụ về mỉa mai liên quan đến nhiệt độ CPU, thời lượng pin và thời gian giao hàng giúp AI hiểu rõ hơn những tình huống khách hàng đang thực sự phàn nàn.

Qua đó, em nhận thấy rằng việc lựa chọn ví dụ mẫu phù hợp có vai trò rất quan trọng trong việc nâng cao chất lượng phản hồi của AI.

⸻

PHẦN 6. CHUẨN BỊ NỘP BÀI LÊN GITHUB

6.1. Tên Repository

HCM-KS26-CNTT1_AI_Session02_Ex05

6.2. Cấu trúc thư mục

HCM-KS26-CNTT1_AI_Session02_Ex05/
│
├── README.md
└── images/
    ├── few-shot-prompt.png
    └── result-test.png

6.3. Các lệnh đẩy bài lên GitHub

git init
git add .
git commit -m "Submit Session02 Exercise 05"
git branch -M main
git remote add origin <GitHub-repository-URL>
git push -u origin main

Nếu repository đã được tạo và kết nối remote từ trước thì không cần chạy lại git init hoặc git remote add origin.

6.4. Checklist trước khi nộp

* [ ]	Có giải thích cơ chế In-Context Learning.
* [ ]	Có phân tích Zero-shot và Few-shot.
* [ ]	Có đủ 3 cặp ví dụ về nhiệt độ, pin và giao hàng.
* [ ]	Có Prompt Few-shot hoàn chỉnh.
* [ ]	Có kết quả chạy thử review CPU 98°C.
* [ ]	Có README.md trên GitHub.
* [ ]	Có đường dẫn repository để nộp Portal.

HẾT BÀI 5
