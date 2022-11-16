# Các kỹ thuật trong ETL 
ETL viết tắt của Extract, Transform và Load. ETL đề cập tới quá trình quán lý dữ diệu từ nhiều nguồn, điều chỉnh dữ liệu theo định dạng hoặc cấu trúc thống nhất và load dữ liệu đã được transform vào môi trường mới (có thể là Database, Data Warehose hoặc Data Lake).
![ELT_techniques_1](https://user-images.githubusercontent.com/103992475/202216380-35fa6f1a-e0b3-4213-a45d-d2ad51bb96b5.png)

**Hình 1.** Quy trình ETL, dữ liệu được extract từ nhiều nguồn khác nhau đến khu vực tổ chức trung gian (intermediate staging area) nơi mà dữ liệu được tích hợp và chuẩn bị cho việc load vào một đích (destination) chẳng hạn như data warehouse. 

## Extract 
Trích xuất dữ liệu là giai đoạn đầu tiên của quy trình ETL, nơi mà dữ liệu được lấy từ các hệ thống nguồn khác nhau. Data có thể hoàn toàn thô, chẳng hạn như dữ liệu cảm biến từ các thiết bị IoT, hoặc có thể dữ liệu phi cấu trúc từ các tài liệu y tế được scan hoặc từ email của công ty. Dữ liệu có thể là steaming data đến từ một mạng truyền thông xã hội hoặc các giao dịch mua bán trên thị trường chứng khoán theo thời gian thực (real-time) hoặc dữ liệu cũng có thể đến từ các database và data warehouse hiện có của doanh nghiệp. 

## Transform 
Giai đoạn transform là nơi mà các quy tắc (rules) và các quy trình (processes) được áp dụng cho dữ liệu để chuẩn bị dữ liệu cho việc load dữ liệu sau khi biến đổi vào các hệ thống đích (target system). Điều này thường được thực hiện trong một môi trường trung gian được gọi là "khu vực tổ chức" (staging area). Tại đây, dữ liệu được làm sạch để đảm bảo độ tin cậy (reliability) và được điều chỉnh để đảm bảo khả năng tương thích với hệ thống đích (target system).

Nhiều cách biến đổi khác nhau được áp dụng như:
* Cleaning: sửa đổi giá trị lỗi bất kỳ hoặc missing values.
* Filtering: chỉ chọn những gì cần thiết.
* Joining: hợp nhất dữ liệu từ nhiều nguồn khác nhau.
* Normalizing: chuyển đổi dữ liệu sang các đơn vị phổ biến.
* Data Structuring: chuyển đổi một định dạng dữ liệu sang định dạng dữ liệu khác, chẳng hạn JSON, XML or CSV về cơ sở dữ liệu dạng bảng.
* Feature Engineering: sử dụng như trong machine learning.
* Anonymizing and Encrypting: đảm bảo riêng tư và bảo mật.
* Sorting: sắp xếp thứ tự dữ liệu để cải thiện hiệu năng tìm kiếm.
* Aggregating: tổng hợp dữ liệu.

## Load 
Giai đoạn load là ghi dữ liệu đã được biến đổi vào một hệ thống đích. Hệ thống đích (target system) có thể là database hoặc data warehouse, data mart, data lake hoặc một số kho dữ liệu tập trung để phân tích, mô hình hóa và được sử dụng để đưa ra các quyết định bởi người phân tích kinh doanh, quản lý, giám đóc điều hành, data scientists và tất cả người dùng ở mọi cấp bậc trong doanh nghiệp. 

Trong hầu hết các trường hợp, dữ liệu được load vào trong database, các ràng buộc được xác định bởi lược đồ (schema) phải được thỏa mãn workflow để chạy thành công. Lược đồ (schema) là tập các quy tắc được gọi là ràng buộc toàn vẹn, bao gồm các quy tắc như tính duy nhất và các trường bắt buộc. Do đó, các yêu cầu như vậy được áp dụng cho giai đoạn load giúp đảm bảo chất lượng dữ liệu tổng thể.

## ETL Workflows dưới dạng Data Pipelines 
Nói chung, ETL workflow là một quy trình được cân nhắc kỹ lưỡng, được thiết kế cẩn thận để đáp ứng các yêu cầu kỹ thuật và yêu cầu của người dùng cuối.

Theo truyền thống, độ chính xác tổng thể của ETL workflow là một yêu cầu quan trọng hơn tốc độ, mặc dù hiệu quả thường là một yếu tố quan trọng trong việc giảng hiểu chi phí tài nguyên. Để tăng hiệu quả, dữ liệu được cung cấp thông qua một data pipeline trong các gói dữ liệu nhỏ hơn (như hình 2). Trong khi một packet đang được extract, một packet trước đó đang được transform và một packet khác đang được load. Bằng cách này, dữ liệu có thể tiếp tục di chuyển trong workflow mà không bị gián đoạn. Mọi bottleneck còn lại được giải trong data pipeline thường có thể được xử lý bằng cách thực hiện song song các task chậm hơn.

![ETL_Workflow_as_Data_Pipelines](https://user-images.githubusercontent.com/103992475/202229381-ed2713a7-4502-4944-befb-294a12c48246.png)

**Hình 2.** Các data packets được cung cấp theo trình tự hoặc "được dẫn" (piped) thông qua ETL data pipeline. Lý tưởng nhất, vào thời điểm packet thứ 3 được ingested, cả 3 quy trình ETL đều chạy đồng thời trên các packet khác nhau. 

Với các quy trình ETL thông thường, dữ liệu được xử lý theo batches, thường theo lịch trình lặp lại cách nhau từ vài giờ đến vài ngày.

## Staging Areas (Khu vực tập trung)

![staging_](https://user-images.githubusercontent.com/103992475/202250185-235a13d9-8c23-41a1-b311-a819f2245745.png)

## ETL Workflows dưới dạng DAGs
## Các tool ETL phổ biến 
