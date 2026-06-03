# Investigating-Windows
câu 1
em vào system information

<img width="1919" height="960" alt="image" src="https://github.com/user-attachments/assets/13eb04c4-07e2-4979-a25a-7a5603af31b8" />

thấy dòng OS name 

<img width="1919" height="968" alt="image" src="https://github.com/user-attachments/assets/bd8ccbf3-bb35-4770-a965-07d373d9272f" />

 os name: microsoft windows server 2016 datacenter, nên em điền trước windows server 2016 nếu ko được sẽ điền windows server 2016  datacenter

<img width="952" height="1046" alt="image" src="https://github.com/user-attachments/assets/83dca06e-bffb-4c8b-8833-e5a4ef20f695" />
 em điền  windows server 2016 thì pass luôn

 câu 2 

 Which user logged in last?

em vào 
<img width="1872" height="1014" alt="image" src="https://github.com/user-attachments/assets/5bf45db7-ab1f-4ce8-bf92-f3e92faeec27" />

thấy được các user 
<img width="1919" height="941" alt="image" src="https://github.com/user-attachments/assets/47ef3372-196e-46b1-ae6a-001ae1206936" />
và có 3 cái đáng nghi nhất là jenny
john
ssm-user

Nên em dùng net user jenny
net user john
net user ssm-user để kiểm tra thời giang login của từng user

<img width="1788" height="765" alt="image" src="https://github.com/user-attachments/assets/958e6377-e2b6-438d-87b7-b9e41614db55" />


<img width="1551" height="858" alt="image" src="https://github.com/user-attachments/assets/7beb9121-16f9-485e-915f-465a938fb2d1" />

<img width="1913" height="982" alt="image" src="https://github.com/user-attachments/assets/d71522d2-498e-42e0-ba97-203dedf7592f" />

<img width="1918" height="921" alt="image" src="https://github.com/user-attachments/assets/8cf08a11-ee67-45d5-8787-95974e21e7b6" />

<img width="1919" height="1022" alt="image" src="https://github.com/user-attachments/assets/24268e05-a708-47a2-90f5-60620e4bb67b" />


với administrator

kết quả:

last logon: 6/2/2026 3:26:23 pm

với john
kết quả:

last logon: 3/2/2019 5:48:32 pm

các user còn lại khi kiểm tra last logon thì hiện never

so sánh các mốc thời gian, administrator có thời gian đăng nhập mới nhất

=> user logged in last là administrator nên đáp án là 

administrator

câu 3

when did john log onto the system last?

câu này hỏi john đăng nhập vào hệ thống lần cuối lúc nào

ở câu trước, em đã dùng net user để so sánh last logon của các tài khoản

trong lúc kiểm tra user nào đăng nhập cuối, em cũng đã chạy:

net user john

kết quả của john có dòng:

last logon: ```3/2/2019 5:48:32 pm```

vì câu này hỏi riêng thời gian đăng nhập cuối của john, nên em lấy trực tiếp giá trị ở dòng last logon đó

đáp án
```
03/02/2019 5:48:32 PM
```
---
câu 4
đầu tiên em vào regedit

sau đó em tìm đến đường dẫn ```hkey_local_machine\software\microsoft\windows\currentversion\run```để xem các chương trình tự động chạy cùng hệ thống

tại đây em thấy một key tên là updatesvc rất đáng nghi

nhìn sang cột data của nó em thấy chuỗi lệnh c:\tmp\p.exe -s \\10.34.2.3 'net user' > c:\tmp\o...

<img width="1919" height="988" alt="image" src="https://github.com/user-attachments/assets/151819f3-b674-474c-bef0-19765c0bf7f8" />

kẻ tấn công đã giấu lệnh ở đây để máy tính tự động kết nối đến ip 10.34.2.3 mỗi khi vừa khởi động

từ chuỗi này em lấy được ip cần tìm

đáp án
```10.34.2.3```

câu 5

em vào computer management

mở local users and groups chọn groups

nhấp đúp vào administrators

trong bảng members thấy có administrator, guest và jenny

đề yêu cầu 2 tài khoản ngoài administrator và xếp abc nên em chọn guest và jenny


<img width="1023" height="520" alt="image" src="https://github.com/user-attachments/assets/a3078fd2-bb06-4dd0-9324-7b61db3e6cff" />


đáp án
```
Guest, Jenny
```
câu 6

em mở task scheduler và kiểm tra danh sách active tasks

em chú ý đến task clean file system được lên lịch chạy hàng ngày vào 4:55 pm

lý do em chốt task này là vì cách đặt tên của nó, kẻ tấn công cố tình dùng cái tên nghe có vẻ giống chức năng dọn dẹp để ngụy trang đánh lừa mắt người quản trị, nhưng thực tế windows không có tác vụ mặc định nào ghi tên chung chung như vậy

<img width="1024" height="535" alt="image" src="https://github.com/user-attachments/assets/06d72a89-6ba6-400a-a9e4-6fd352df8823" />

<img width="1024" height="525" alt="image" src="https://github.com/user-attachments/assets/7a409608-1462-4815-abce-1197980e3422" />

đáp án

```
clean file system

```
