# Các kỹ thuật trong ETL 
ETL viết tắt của Extract, Transform và Load. ETL đề cập tới quá trình quán lý dữ diệu từ nhiều nguồn, điều chỉnh dữ liệu theo định dạng hoặc cấu trúc thống nhất và load dữ liệu đã được transform vào môi trường mới (có thể là Database, Data Warehose hoặc Data Lake).
![ELT_techniques_1](https://user-images.githubusercontent.com/103992475/202216380-35fa6f1a-e0b3-4213-a45d-d2ad51bb96b5.png)

**Hình 1.** Quy trình ETL, dữ liệu được extract từ nhiều nguồn khác nhau đến khu vực tổ chức trung gian (intermediate staging area) nơi mà dữ liệu được tích hợp và chuẩn bị cho việc load vào một đích (destination) chẳng hạn như data warehouse. 

## Extract 
Trích xuất dữ liệu là giai đoạn đầu tiên của quy trình ETL, nơi mà dữ liệu được lấy từ các hệ thống nguồn khác nhau. Data có thể hoàn toàn thô, chẳng hạn như dữ liệu cảm biến từ các thiết bị IoT, hoặc có thể dữ liệu phi cấu trúc từ các tài liệu y tế được scan hoặc từ email của công ty. Dữ liệu có thể là steaming data đến từ một mạng truyền thông xã hội hoặc các giao dịch mua bán trên thị trường chứng khoán theo thời gian thực (real-time) hoặc dữ liệu cũng có thể đến từ các database và data warehouse hiện có của doanh nghiệp. 

## Transform 
## Load 
## ETL Workflows dưới dạng Data Pipelines 
## Staging Areas (Khu vực tập trung)
## ETL Workflows dưới dạng DAGs
## Các tool ETL phổ biến 
