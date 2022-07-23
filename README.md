# TrongNhan_Docker
Họ tên: Tô Trọng Nhân
MSSV: 110119035
Lớp: DA19TTA
Email: 110119035@st.tvu.edu.vn
SĐT: 0359695554
Hướng dẫn sử dụng 
- Sử dụng hệ điều hành Ubuntu Server 16.04 đã cài đặt sẵn Docker
- Khởi tạo container my-php và my-mysql 
-	Đầu tiên, tạo docker network có tên “my-network-joomla” để kết nối các conatiner
$ docker network create my-network-joomla

-	Đối với Php thì sử dụng image my-php vừa push lên docker hub 
$ docker pull trongnhan35/image:version1
-	Khởi tạo container php từ image trongnhan35/image:vesion1, kết nối với network có tên “ my-network-joomla,”  tên container là “ container-myphp ”, mount thư vừa git clone source về, cổng 9000.
$ docker run  --net my-network-joomla --name php-container -v /SourceCode:/var/www/html -p 9000:80 -d trongnhan35/image:version1
-	Đối với Mysql, thì mình sử dụng trực tiếp image từ Dockerhub
$ docker pull mysql:5.7
-	Khởi tạo container mysql từ image mysql:5.7, hostname là sql (trùng tên với host trong file config của joomla), kết nối với network có tên “ my-network-joomla,”  tên container là “ container-mysql ”, mount thư vừa git clone database về.
$ docker run --restart always --hostname sql --name mysql-container --net my-network-joomla -v /database:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:5.7

- Giải nén 2 file SourceCode và database 
- Mount 2 thư mục đó đến thư mục làm việc của container
- Truy cập trình trình duyệt http://localhost:9000 để xem kết quả

