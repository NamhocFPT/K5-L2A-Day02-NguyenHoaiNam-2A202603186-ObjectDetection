# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp     | Định nghĩa của bạn                                                                                   | Ví dụ/điểm phân biệt                                                                                                                      |
| ------- | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `car`   | Có mũi xe (capo) nhô ra phía trước rõ, mui thấp hoặc vừa, có cốp hoặc cửa hậu nhỏ.                   | Sedan, hatchback, SUV, crossover, coupe. Mui thấp, kính chắn gió nghiêng, thường có cốp sau riêng.                                        |
| `truck` | Có thùng hàng phía sau tách khỏi cabin (thùng hở, thùng bạt, thùng kín, thùng ben), hoặc là đầu kéo. | Xe tải nhỏ, xe tải thùng, xe ben, xe đầu kéo, xe bán tải. Điểm nhận biết là phần cabin và phần thùng hàng rõ ràng, thân sau cao hoặc dài. |
| `bus`   | Thân rất dài, hàng cửa sổ liên tục hai bên, mui cao phẳng                                            | Xe buýt thành phố, xe khách đường dài, xe giường nằm. Thân dài, mui cao phẳng, hàng cửa sổ liên tục                                       |
| `van`   | Thân liền một khối hình hộp, đầu xe ngắn hoặc gần như không có capo                                  | xe van giao hàng, minivan 7 chỗ kiểu hộp. Mui cao hơn car, thân liền khối, thường không có cửa sổ hai bên khoang sau                      |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: vẽ hộp vừa khít quanh xe, các cạnh chạm sát đầu xe, đuôi xe, nóc và bánh.
- Vật thể bị che khuất: 
+ Che ít (dưới 1/3): vẽ bình thường.
+ Che khoảng 1/3 đến 2/3: vẫn vẽ nếu còn nhìn ra là xe gì. Chỉ vẽ box quanh phần thấy được, không tự đoán phần bị che.
+ Che hơn 2/3 hoặc không còn nhìn ra loại xe: Đọc lại guildeline hoặc bỏ qua, hỏi lại labCoach.
- Vật thể bị cắt bởi rìa ảnh: còn thấy từ khoảng 1/3 thân xe trở lên và nhìn ra loại xe (không tự phỏng đoán) thì vẽ, kéo box sát mép ảnh. Chỉ lộ một góc nhỏ (một bánh, một mảng thân) thì bỏ qua.
- Vật thể rất nhỏ/mơ hồ: 
+ Xe nhỏ đến mức box có cạnh ngắn dưới khoảng 20 px: bỏ qua.
+ Xe đủ lớn nhưng nhìn không ra là car, van hay truck: không tự ý đoán và đánh box, đọc kĩ guideline nếu chưa rõ tiếp tục hỏi labcoach
+ Đã chọn ngưỡng nào thì dùng đúng ngưỡng đó cho cả bộ ảnh.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh         | Tình huống                                                                                                                                                        | Quyết định cuối                                                                                            | Lý do theo schema                                                                                                                                                                                      |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `drive_003` | Các box chồng lấn, khó biết ranh giới từng xe.                                                                                                                    | Mỗi xe một box riêng, chỉ bao phần nhìn thấy của xe đó, cho phép các box chồng nhau. Không vẽ phần bị che. | Quy tắc vẽ hai box riêng trên phần nhìn thấy của từng xe                                                                                                                                               |
| `drive_005` | Camera nhìn từ trên xuống phía đầu xe nên mui xe che mất phần đuôi. Chỉ thấy đầu, nóc và hai bên thân. Dáng xe hơi cao và vuông nên dễ băn khoăn giữa car và van. | Giữ truck, box bao phần thấy được                                                                          | truck do thấy thùng hàng tách khỏi cabin. Ở đây không thấy trực tiếp, nhưng phần thân phía sau cabin kéo dài ra và hơi thấp hơn cabin, khác với van là mui liền một khối. Vì vậy vẫn nghiêng về truck. |
| `drive_010` | Ảnh tối, thấy thân bên nhưng nhòe                                                                                                                                 | Gán car                                                                                                    | Còn nhìn ra dáng xe con (capo, cốp, kính), chỉ tối chứ không bị che                                                                                                                                    |
