# Mục đích
Mục đích của chương trình này là tự động hóa chuyển hàng loạt file .pdf sang file định dạng .txt

Parse tất cả file .pdf trong thư mục `input/` và xuất kết quả ra thư mục `<tên file>/output` trong thư mục này

Trong thư mục output này, file final.md là ghép tất cả các trang

# Hướng dẫn chạy
* **Do máy chủ ban đầu đang sập, nên tạm thời mấy hướng dẫn sau đều vô ích, bạn hãy kéo xuống cuối cùng để xem cách dùng mới**

* *Để tự động hóa, chúng tôi đã tạo file `run_py.bat` cho phiên bản python(chính) và `run_ipynb` cho phiên bản jupyter notebook(mục đích nghiên cứu) để tự động chạy chương trình. Nếu bạn muốn chạy thủ công thì hãy đọc tiếp phần dưới đây.*

Đầu tiên bạn cần chắc chắn mình đã cài đầy đủ các thư viện cần thiết, do đó hãy chạy lệnh này:
```
python -m pip install -r requirements.txt
```

Chúng tôi ở đây dùng [Gemini CLI](https://github.com/google-gemini/gemini-cli) làm API để chuyển đổi dữ liệu raw sang format text2qti, hãy chắc chắn bạn đã cài đặt gemini cli theo hướng dẫn [này](https://github.com/google-gemini/gemini-cli)

## Chạy bằng Python

File chính ở đây là `main.py`

Trước hết bạn hãy đổi đường dẫn hoạt động:
```
cd src/python
```
Sau đó bạn hãy chạy lệnh này để auto-parse file .pdf thành file .md tổng quát:
```
python main.py
```
Output của mỗi file pdf sẽ được lưu tại `<đường dẫn file>/<tên file>/output/`

Nếu bạn muốn convert sang qti file thì bạn có thể chạy lệnh sau:
```
python QTIconvert.py
```

## Chạy bằng Jupyter Notebook (Dành cho mục đích phát triển)

File chính ở đây là `main.ipynb`

Sau đó bạn hãy chạy lệnh này để auto-parse file .pdf thành file .md tổng quát:
```
jupyter nbconvert --to notebook --execute src/main.ipynb --output executed_notebook.ipynb
```
Output của mỗi file pdf sẽ được lưu tại `<đường dẫn file>/<tên file>/output/`

Nếu bạn muốn convert sang qti file thì bạn có thể chạy lệnh sau:
```
jupyter nbconvert --to notebook --execute src/QTIconvert.ipynb --output executed_notebook2.ipynb
```

# Cách hoạt động của chương trình
Upload lần lượt các file .pdf trong thư mục `input/` lên máy chủ [OCR](https://dotsocr.xiaohongshu.com) online

Download file zip kết quả của mỗi file xuống lần lượt các thư mục cùng tên với file

Giải nén file zip

Ghép lại file các trang thành một file mang tên final.md

Chương trình dựa theo các bước cơ bản này mà bắt đầu thực hiện tự động hóa, xử lý hàng loạt file pdf một cách tự động.

# Cách chạy tạm thời đối mặt với máy chủ gốc bị sập

Trước tiên các bước ban đầu vẫn khá giống cách cũ:

Đầu tiên bạn cần chắc chắn mình đã cài đầy đủ các thư viện cần thiết, do đó trong command prompt hãy chạy lệnh này:
```
python -m pip install -r requirements.txt
```

Sau đó bạn hãy vào thư mục chứa file code:
```
cd src/python
```

Ở đây có một file mới để xử lý cho việc đổi máy chủ đó là `newocr.ipynb`

Bạn chỉ cần vào vscode, mở file này lên, ipynb đơn giản là notebook cho phép chia code python thành các cell nhỏ, từ đấy có thể chạy từng cell một tùy ý. 

Bạn hãy bấm chạy cell đầu tiên, nếu bạn chưa cài jupyter notebook thì vscode sẽ thông báo, bạn chỉ cần đồng ý cho cài đặt các thư viện cần thiết rồi ngồi đợi.

Khi cell code chạy rồi sẽ có một cửa sổ chrome bật lên, yêu cầu đăng nhập vào server, bạn chỉ cần điền email, nhận mã xác nhận,... khi đăng nhập xong thì để yên windows ấy vào lại vscode.

Sau đó bạn hãy chạy thủ công lần lượt cell thứ 2, cell thứ 3, cell thứ 4... và cứ thế cho đến khi chạy hết notebook.

Sau khi xong rồi bạn chỉ cần chạy trong terminal lệnh `python QTIconvert.py` là xong.
