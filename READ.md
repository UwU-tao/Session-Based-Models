## Data raw là 1 file csv với header lần lượt là ‘sessionId’, ‘timestamp’, ‘itemId’, ‘category’.
+ ‘sessionId’, ‘itemId’, ‘category’: 'int'
+ ‘Timestamp’: %Y-%m-%dT%H:%M:%SZ. Ví dụ: 2023-11-14T10:20:00Z.\
Lưu ý: tên từng cột lần lượt là như trên nhưng sẽ không ghi tên của từng cột vào file data.\
Một dòng data sẽ có dạng: 123,2023-11-14T10:20:00Z,456,1. Với\
+ 123 là sessionId.
+ 2023-11-14T10:20:00Z là timestamp
+ 456 là itemId
+ 1 là category

## Cách xử lý data của mô hình (code có sẵn ở mô hình, đây chỉ là mô tả cách mà code hoạt động):
1. Lọc hết các session mà có tương tác với item < 2
2. Lọc hết các item mà có tương tác < 5 trong từng session
3. Data được chia ra 2 tập train, test. Train lấy các session phía trước của thời gian item đầu tiên trong session cuối cùng được tương tác - 1 ngày. Test lấy các session sau thời gian đó.

## Cách chạy model
1. Clone repo
```bash
!git clone -b trans4rec https://github.com/UwU-tao/Session-Based-Models.git
```
2. Cài đặt requirements.
```bash
%cd Session-Based-Models
!pip install -r requirements.txt
```
3. Chuyển data vào project
```bash
!mkdir datasets
!mkdir datasets/yoochoose
```
Sau đó, ta sẽ chuyển file data dạng .csv hoặc .dat vào folder yoochoose, lưu ý rename file data thành yoochoose.csv hoặc yoochoose.dat.\
4. Tiền xử lý dữ liệu
```bash
!python src/preprocessing.py --dataset 'yoochoose'
```
5. Chạy mô hình\
+ Mô hình TRON
```bash
!python -m src --config-filename tron/yoochoose_x
```
Thay x từ 1 đến 5 để đi qua 5 configs khác nhau.\
+ Mô hình SASREC
```bash
!python -m src --config-filename sasrec/sasrec_yoochoose_x
```
Thay x từ 1 đến 5 để đi qua 5 configs khác nhau.\
+ Mô hình GRU4REC
```bash
!python -m src --config-filename gru4rec/gru4rec_yoochoose_x
```
Thay x từ 1 đến 5 để đi qua 5 configs khác nhau.\
