#Tìm hiểu về giao thức HTTP và dịch vụ Web

##Mục lục

[I. Giao thức HTTP](#http)

[1. Tổng quan giao thức http](#tong-quan)

[2. Nguyên tác hoạt động](#nguyen-tac)

[3. HTTP Request và HTTP Respond](#http-rq-rp)

[II. Dịch vụ Web](#web)

[1. Tổng quan về dịch vụ Web](#tq-web)

[2. Các bước hoạt động](#hoat-dong)

----

### <a name="http"></a>I. Giao thức HTTP
#### <a name="tong-quan"></a>1. Tổng quan về giao thức http

- HTTP là chữ viết tắt của HyperText Transfer Protocol (giao thức truyền tải siêu văn bản). Dùng để trao đổi ngôn ngữ văn bản,hình ảnh,
 đồ họa, âm thanh và được sử dụng rất phổ biến trên các máy chủ web-server.
Đây là một giao thức thuộc tầng ứng dụng trong bộ các giao thức TCP/IP (gồm một nhóm các giao thức nền tảng cho internet). 
HTTP hoạt động dựa trên mô hình Client – Server(máy khách và máy chủ) thực hiện trên các hệ thống đầu cuối khác nhau,
nói chuyện với nhau khác bằng cách trao đổi các thông điệp HTTP. 

#### <a name="nguyen-tac"></a>2. Nguyên tác hoạt động.

- HTTP hoạt động dựa trên mô hình Client – Server.  HTTP sử cổng port 80 để giao tiếp với các client, và sử dụng bản tin respond để đáp ứng các bản tin request của client.
- Các bước hoạt động của web-client và web-server:
<ul>
<li>Đầu tiên máy client khởi tạo quá trình kết nối tới máy chủ server thông qua quá trình bắt tay 3 bước
- **Quá trình bắt tay 3 bước**
(xét quá trình truy cập Webserver)
- Bước 1: Dữ liệu yêu cầu đi từ tầng Application xuống sẽ được tầng Transport khởi tạo cổng nguồn là 45994, 
đánh số thứ tự của gói tinh này là 200 (trường Sequence đánh số 200). Giao thức TCP sẽ đóng thêm cổng đích là 80 vào gói tin. 
Đồng thời cờ SYN được bật. Cờ SYN bật lên để yêu cầu thiết lập phiên truyền.
- Bước 2: Sau khi Server Web sẽ nhận dữ liệu và xử lý thì tầng Transport sẽ đóng cổng nguồn là 80 và cổng đích là 45994, 
số thứ tự gói tin Web Server gửi đi là 1540 ( trường Sequence đánh số 1540). 
ACK sẽ bằng số Sequence của Client gửi sang và tăng lên một để báo nhận thành công (ACK=201). 
Cờ SYN và ACK cùng bật để thông báo đây là phiên truyền thứ 2.
- Bước 3: Client nhận được dữ liệu truyền về từ Server nó sẽ báo lại là nhận thành công. 
Lúc này cổng nguồn của phiên thiếp lập vẫn là 45994, cổng đích là 80. 
Số thứ tự gói tin được được trường Sequence đánh là 201 chính bằng số ACK của Server gửi về. 
Số ACK gửi đi là 1541, bằng số Sequence của Server gửi sang và tăng lên một để báo nhận thành công. 
</li>
<li>Sau khi đã khởi tạo kết nối, máy client sẽ gửi một bản tin request tới server để yêu cầu được lấy dữ liệu</li>
<li>Khi nhận được bản tin resquest từ client. 
Server gửi lại bản tin ACK cho client xác nhận đã nhận được bản tin request của client và ngay sau đó sẽ gửi cho client gói tin có chưa dữ liệu mà client yêu cầu(bản tin respond).</li>
</ul>

#### <a name="http-rq-rp"></a>3. Bản tin Request và Respond
##### a. Bản tin Request
- Để bắt đầu trao đổi dữ liệu, phía client khởi tạo một HTTP session bằng cách mở một kết nối TCP đến HTTP server sau đó gửi request đến server này. 
Request có thể được tạo bằng nhiều cách, trực tiếp khi người dùng nhấp vào một liên kết trên trình duyệt hoặc gián tiếp, 
ví dụ như một video được đính kèm trong một website và việc request đến website này sẽ dẫn đến một request tới video ấy.
- Bắt đầu 1 bản tin Request sẽ là dòng Request Line với 3 thông tin đó là 
<ul>
<li>Method: là phương thức mà HTTP Request này sử dụng, thường là GET, POST, ngoài ra còn một số phương thức khác như HEAD, PUT, DELETE, OPTION, CONNECT.
- GET: lấy một nguồn tài nguyên hiện có. URL chứa tất cả các thông tin cần thiết các máy chủ cần phải xác định vị trí và trả lại tài nguyên.
- POST: tạo ra một nguồn tài nguyên mới. POST yêu cầu thường mang một tải trọng mà xác định các dữ liệu về tài nguyên mới.
- PUT: cập nhật một nguồn tài nguyên hiện có. Tải trọng có thể chứa dữ liệu cập nhật của nguồn tài liệu. 
- DELETE: xóa một nguồn tài nguyên hiện có.
- HEAD: đây là tương tự như GET, nhưng không có nội dung thư. Nó được sử dụng để lấy các tiêu đề máy chủ cho một tài nguyên cụ thể, thường để kiểm tra xem tài nguyên đã thay đổi, qua thời gian. 
- TRACE: sử dụng để lấy các bước nhảy là một yêu cầu cần thiết để làm tròn chuyến đi từ máy chủ. Mỗi proxy trung gian hoặc gateway sẽ bơm IP hoặc tên DNS vào trường “Via”. Điều này có thể được sử dụng cho mục đích chẩn đoán.
- OPTIONS: sử dụng để lấy các khả năng máy chủ. Về phía khách hàng, nó có thể được sử dụng để chỉnh sửa theo yêu cầu dựa trên những gì các máy chủ có thể được hỗ trợ 
</li>
<li>URI: là địa chỉ định danh của tài nguyên. Nếu URI là / - tức request cho tài nguyên gốc, nếu request không yêu cầu một tài nguyên cụ thể, URI có thể là dấu *.</li>
<li>HTTP version: là phiên bản HTTP đang sử dụng. vd: HTTP 1.1.</li>
</ul>

- Tiếp theo là các trường request-header, cho phép client gửi thêm các thông tin bổ sung về thông điệp HTTP request và về chính client. 
Một số trường thông dụng như:
<ul>
<li>Accept: loại nội dung có thể nhận được từ thông điệp response. Ví dụ: text/plain, text/html…</li>
<li>Accept-Encoding: các kiểu nén được chấp nhận. Ví dụ: gzip, deflate, xz, exi…</li>
<li>Connection: tùy chọn điều khiển cho kết nối hiện thời. Ví dụ: keep-alive, Upgrade…</li>
<li>Cookie: thông tin HTTP Cookie từ server.</li>
<li>User-Agent: thông tin về user agent của người dùng.</li>
</ul>

##### b. Bản tin Respond
- Cấu trúc HTTP response gần giống với HTTP request, chỉ khác nhau là thay vì Request-Line, thì HTTP có response có Status-Line. 
Và giống như Request-Line, Status-Line cũng có ba phần như sau:
<ul>
<li>HTTP-version: phiên bản HTTP cao nhất mà server hỗ trợ.</li>
<li>Status-Code: mã kết quả trả về.</li>
<li>Reason-Phrase: mô tả về Status-Code.</li>
</ul>


- Một số loại Status-Code thông dụng mà server trả về cho client như sau:

**1xx: information Message:** các status code này chỉ có tính chất tạm thời, client có thể không quan tâm.

**2xx Successful**: khi đã xử lý thành công request của client, server trả về status dạng này:

- 
<ul>
<li>200 OK: request thành công.</li>
<li>202 Accepted: request đã được nhận, nhưng không có kết quả nào trả về, thông báo cho client tiếp tục chờ đợi.</li>
<li>04 No Content: request đã được xử lý nhưng không có thành phần nào được trả về.</li>
<li>205 Reset: giống như 204 nhưng mã này còn yêu câu client reset lại document view.</li>
<li>206 Partial Content: server chỉ gửi về một phần dữ liệu, phụ thuộc vào giá trị range header của client đã gửi.</li>
</ul>

**3xx Redirection**: server thông báo cho client phải thực hiện thêm thao tác để hoàn tất request:

-
<ul>
<li>301 Moved Permanently: tài nguyên đã được chuyển hoàn toàn tới địa chỉ Location trong HTTP response.</li>
<li>303 See other: tài nguyên đã được chuyển tạm thời tới địa chỉ Location trong HTTP response.</li>
<li>304 Not Modified: tài nguyên không thay đổi từ lần cuối client request, nên client có thể sử dụng đã lưu trong cache.</li>
</ul>

**4xx Client error**: lỗi của client:

- 
<ul>
<li>400 Bad Request: request không đúng dạng, cú pháp.</li>
<li>401 Unauthorized: client chưa xác thực.</li>
<li>403 Forbidden: client không có quyền truy cập.</li>
<li>404 Not Found: không tìm thấy tài nguyên.</li>
<li>405 Method Not Allowed: phương thức không được server hỗ trợ.</li>
</ul>

**5xx Server Error**: lỗi của server:

-
<ul>
<li>500 Internal Server Error: có lỗi trong quá trình xử lý của server.</li>
<li>501 Not Implemented: server không hỗ trợ chức năng client yêu cầu.</li>
<li>503: Service Unavailable: Server bị quá tải, hoặc bị lỗi xử lý.</li>
</ul>

- Ngoài ra HTTP Respond còn có một số trường khác:
<ul>
<li>Date: ngày dữ liệu được lưu trên server</li>
<li>Server: chỉ ra thông tin server sử dụng phiên bản của chương trình máy chủ</li>
<li>Connection: thông báo web-server sẽ giữ phiên kết nối sau khi gửi xong dữ liệu web-client yêu cầu</li>
<li>Keep-Alive: thông báo phiên kết nối sẽ được giữ trong vòng 1s và max=100s</li>
</ul>

### <a name="web"></a>II. Dịch vụ Web
#### <a name="tq-web"></a>1. Tổng quan về dịch vụ web

- Là dịch vụ liên kết trang siêu văn bản. Dùng để truyền thông tin tới người dùng một cách đa dạng và phong phú.
- Dịch vụ Web dùng 2 cách để gửi dữ liệu tới người dùng đó là HTTP (không bảo mật) và HTTPS (có bảo mật).
- Để dịch vụ Web hoạt động được nó phải có 2 thành phần: Web Server và Web Client
<ul>
<li>Web Server là nơi cung cấp dữ liệu Web. Người ta xây dựng lên một Website để người dùng truy cập vào. Web Server sẽ chạy ở Port 80 hoặc 443.</li>
<li>Web Client là phía người dùng. Người dùng mở IE hoặc Firefox truy cập vào tên miền của trang Web.</li>
</ul>

#### <a name="hoat-dong"></a>2. Các bước hoạt động của dịch vụ Web

- Bước 1: người dùng truy cập tên miền Website bằng IE hoặc Firefox.
- Bước 2: IE hoặc Firefox sẽ sinh ra một Port cao đồng thời dữ liệu sẽ chuyển xuống tầng Transport. 
Đồng thời IE hoặc Firefox sẽ nhờ DNS Client phân giải hộ tên miền ra địa chỉ IP Web Server. 
- Bước 3: Transport thấy dữ liệu là Web nó sẽ nhận bằng Port 80 hoặc 443 sau đó đóng giao thức TCP rồi truyền xuống dưới.
- Bước 4: Dữ liệu sẽ được tầng Network đóng IP máy mình và IP máy Web Server (IP Web Server được DNS Client nhờ DNS Server phân giải hộ).
- Bước 5: Sau khi dữ liệu tới được Web Server nó sẽ được chuyển lên theo Port 80 hoặc 443. Sau đó dữ liệu được đóng lại và gửi xuống đường truyền. 
- Khi Client nhận được nó sẽ được Transport chuyển lên IE đúng vào Port cao khi khởi tạo (do có Port cao này nên ta có thể mở nhiều cửa sổ trên một trình duyệt với nhiều Website khác nhau mà không sợ bị trùng. 
