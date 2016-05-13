#Tìm hiểu giao thức và dịch vụ DNS
##Mục lục
[I. Tổng quan về DNS](#tong-quan)

[II. Cấu trúc hệ thống DNS](#cau-truc)

[1. DNS name space](#name-space)

[2. Các DNS server](#server-dns)

[3. DNS zone](#zone-dns)

[4. Các bản ghi của DNS Server](#ban-ghi)

[5. Cơ chế phân giải tên miền](#co-che)


----

### <a name="tong-quan"></a>I. Tổng quan về DNS

- Mỗi máy tính, thiết bị mạng tham gia vào mạng Internet đều giao tiếp với nhau bằng địa chỉ IP (Internet Protocol. 
Để thuận tiện cho việc sử dụng và dễ nhớ ta dùng tên (domain name) để xác định thiết bị đó. 
Hệ thống tên miền DNS (Domain Name System) được sử dụng để ánh xạ tên miền thành địa chỉ IP. 
Vì vậy, khi muốn liên hệ tới các máy, chúng chỉ cần sử dụng chuỗi ký tự dễ nhớ (domain name) như: 
http://hanu.vn, http://www.fit.hanu.vn …, thay vì sử dụng địa chỉ IP là một dãy số dài khó nhớ.

- Ban đầu, khi DNS chưa ra đời, người ta sử dụng một file tên Host.txt, file này sẽ lưu thông tin về tên host và địa chỉ của host của tất cả các máy trong mạng, 
file này được lưu ở tất cả các máy để chúng có thể truy xuất đến máy khác trong mạng. Khi đó, nếu có bất kỳ sự thay đổi về tên host, 
địa chỉ IP của host thì ta phải cập nhật lại toàn bộ các file Host.txt trên tất cả các máy. 
Do vậy đến năm 1984 Paul Mockpetris thuộc viện USC’s Information Sciences Institute phát triển một hệ thống quản lý tên miền mới lấy tên là Hệ thống tên miền – Domain Name .

- Hệ thống tên miền này cũng sữ dụng một file tên host.txt, lưu thông tịn của tất cả các máy trong mạng, nhưng chỉ được đặt trên máy làm máy chủ tên miền (DNS). 
Khi đó, các Client trong mạng muốn truy xuất đến các Client khác, thì nó chỉ việc hỏi DNS.

- Như vậy, mục đích của DNS là :
<ul>
<li>Phân giải địa tên máy thành địa chỉ IP và ngược lại.</li>
<li>Phân giải tên domain.</li>
</ul>

### <a name="cau-truc"></a>II. Cấu trúc hệ thống DNS

####<a name="name-space"></a> 1. DNS name space

- Hệ thống tên trong DNS được sắp xếp theo mô hình phân cấp và cấu trúc cây logic được gọi là DNS namespace.

<img src="https://cloud.githubusercontent.com/assets/18635054/15224759/5a5a0c76-18a5-11e6-82e1-cd14d4fce76a.png">

- Hệ thống tên miền được phân thành nhiêu cấp :
<ul>
<li>Gốc (Domain root): Nó là đỉnh của nhánh cây của tên miền. Nó có thể biểu diễn đơn giản chỉ là dấu chấm “.”</li>
<li>Tên miền cấp một (Top-level-domain) : gồm vài kí tự xác định một nước, khu vưc hoặc tổ chức. Nó đươc thể hiện là “.com” , “.edu” ….</li>
<li>Tên miền cấp hai (Second-level-domain): Nó rất đa dạng rất đa dạng có thể là tên một công ty, một tổ chức hay một cá nhân.</li>
<li>Tên miền cấp nhỏ hơn (Subdomain): Chia thêm ra của tên miền cấp hai trở xuống thường được sử dụng như chi nhánh, phòng ban của một cơ quan hay chủ đề nào đó.</li>
</ul>

- Tổ chức quản lý hệ thống tên miền trên thế giới là The Internet Coroperation for Assigned Names and Numbers (ICANN).
Tổ chức này quản lý mức cao nhất của hệ thống tên miền (mức root) do đó nó có quyền cấp phát các tên miền ở mức cao nhất gọi là Top-Level-Domain.

- Khi một máy khách (client) truy vấn một tên miền nó sẽ đi lần lượt từ root phân cấp xuống dưới để đến DNS quản lý domain cần truy vấn.

- Các loại tên miền:
<ul>
<li>Com     :    Tên miền này được dùng cho các tổ chức thương mại.</li>
<li>Edu     :    Tên miền này được dùng cho các cơ quan giáo dục, trường học.</li>
<li>Net     :    Tên miền này được dùng cho các tổ chức mạng lớn.</li>
<li>Gov     :    Tên miền này được dùng cho các tổ chức chính phủ.</li>
<li>Org     :    Tên miền này được dùng cho các tổ chức khác.</li>
<li>Int     :    Tên miền này dùng cho các tổ chức quốc tế.</li>
<li>Info    :    Tên miền này dùng cho việc phục vụ thông tin.</li>
<li>Arpa    :     Tên miền ngược.</li>
<li>Mil     :    Tên miền dành cho các tổ chức quân sự, quốc phòng.</li>
<li>Mã các nước trên thế giới tham gia vào mạng internet, các quốc gia này được qui định bằng hai chữ cái theo tiêu chuẩn ISO-3166 .Ví dụ : Việt Nam là .vn, Singapo là sg….</li>
</ul>

####<a name="server-dns"></a> 2. Các DNS server

- Là một máy tính chạy chương trình DNS Server, như là DNS service.

- Lưu thông tin của Zone, truy vấn và trả kết quả cho DNS Client, chạy DNS service.

- DNS Server là một cơ sở dữ liệu chứa các thông tin về vị trí của các DNS domain và phân giải các truy vấn xuất phát từ các Client.

- DNS Server có thể cung cấp các thông tin do Client yêu cầu, 
và chuyển đến một DNS Server khác để nhờ phân giải hộ trong trường hợp nó không thể trả lời được các truy vấn về những tên miền không thuộc quyền quản lý và cũng luôn sẵn sàng trả lời các máy chủ khác về các tên miền mà nó quản lý.

- Máy chủ cấp cao nhất là Root Server do tổ chức ICANN quản lý:
<ul>
<li>Là Server quản lý toàn bộ cấu trúc của hệ thống tên miền</li>
<li>Root Server không chứa dữ liệu thông tin về cấu trúc hệ thống DNS mà nó chỉ chuyển quyền (delegate) quản lý xuống cho các Server cấp thấp hơn và do đó Root Server có khả năng định đường đến của một domain tại bất kì đâu trên mạng</li>
</ul>

##### 2.1 Primary Server

- Mỗi Domain phải có 1 Primary Name Server. Server này được register trên Internet để quản lý Domain. Mọi người trên Internet đều biết tên máy tính và IP của Server này.

- Người quản trị DNS sẽ tổ chức các cơ sở dữ liệu DNS trên Primary Name Server. 
Server này đảm nhận vai trò chính trong việc phân giải tất cả các máy tính trong Domain hay Zone

##### 2.2 Secondary Server

- Mỗi Domain có 1 Primary Name Server để quản lý cơ sở dữ liệu DNS. 
Nếu như Server này tạm ngưng hoạt động vì 1 lý do nào đó thì việc phân giải DNS bị gián đoạn. 
Để tránh trường hợp này ngườ ta đã thiết kế ra 1 máy chủ dự phòng gọi là Secondary Name Server (hay còn gọi là Slave).

- Khi Secondary Name Server được khởi động nó sẽ tìm Primary Name Server nào mà nó được phép lấy dữ liệu về máy. 
Nó sẽ copy lại toàn bộ CSDL DNS của Primary Name Server mà nó được phép transfer (quá trình này gọi là quá trình Zone Transfer). 
Theo 1 chu kỳ nào đó do người quản trị quy định thì Secondary Name Server sẽ sao chép và cập nhật CSDL từ Primary Name Server.

##### 2.3 Caching-only Server

- Loại này chỉ sử dụng cho việc truy vấn, lưu giữ câu trả lờ dựa trên thông tin có trên cache của máy và cho kết quả truy vấn. 
Chúng không hề quản lý một domain nào và thông tin mà nó chỉ giới hạn những gì được lưu trên cache của Server.

- Lúc ban đầu khi Server bắt đầu chạy thì nó không lưu thông tin nào trong cache. 
Thông tin sẽ được cập nhật theo thời gian khi các Client Server truy vấn dịch vụ DNS. 
Nếu sử dụng kết nối mạng WAN tốc độ thấp thì việc sử dụng caching-only DNS Server là giải pháp hữu hiệu cho phép giảm lưu lượng thông tin truy vấn trên đường truyền.

- Caching-only có khả năng trả lời các câu truy vấn đến Client. Nhưng không chứa Zone nào và cũng không có quyền quản lý bất kì domain nào. 
Nó sử dụng bộ cache của mình để lưu các truy vấn của DNS của Client. Thông tin sẽ được lưu trong cache để trả lời các truy vấn đến Client.

##### 2.4 Stub Server

- Là DNS Server chỉ chứa các bản copy của Zone, nó chỉ chứa danh sách các DNS Server được authoritative từ master Zone.
- Sử dụng stub có thể tăng tốc độ phân giải tên. Dễ quản lý.

####<a name="zone-dns"></a> 3. Các DNS zone

- Tập hợp các ánh xạ từ host đến địa chỉ IP và từ IP đến host của một phần liên tục trong một nhánh của domain.
- Thông tin của DNS Zones là những record gồm tên Host và địa chỉ IP được lưu trong DNS Server, DNS Server quản lý và trả lời những yêu cầu từ Client liên quan đến DNS Zones này.
- Hệ thống tên miền (DNS) cho phép phân chia tên miền để quản lý và nó chia hệ thống tên miền thành Zone và trong Zone quản lý tên miền được phân chia đó.
Các Zone chứa thông tin vê miền cấp thấp hơn, có khả năng chia thành các Zone cấp thấp hơn và phân quyền cho các DNS Server khác quản lý.
- **Forward Lookup Zone**: Dùng để phân giải host name thành địa chỉ IP
- **Reverse Lookup Zone** : Dùng để phân giải ngược giống như In-addr.arpa Zone. Cho phép phân giải địa chỉ IP thành host name

####<a name="ban-ghi"></a> 4. Các bản ghi của DNS Server

##### 4.1 Bản ghi A (Address) và CNAME (Canonical Name):
- Record A  (Address) ánh xạ  tên máy  (hostname) vào địa chỉ  IP. 
- Record CNAME  (canonical name) tạo tên bí danh alias trỏ vào một tên canonical. Tên canonical là tên host trong record A hoặc lại trỏ vào 1 tên canonical khác
- Cú pháp record A:  
[tên-máy-tính]   IN  A  [địa-chỉ-IP]

##### 4.2 MX (Mail Exchange)
- Dùng để xác định Mail Server cho một domain. Ví dụ khi bạn gởi email tới thaonv@hanu.vn, 
mail server sẽ xem xét MX Record hanu.vn xem nó được điểu khiển chính xác bởi mail server nào (mail.hanu.vn chẳng hạn) rồi tiếp đến sẽ xem A Record để chuyển tới IP đích.
- Cú pháp: [tên miền] IN MX [giá trị ưu tiên] [máy chủ thư điện tử]
Ví dụ hanu.vn IN MX 1 mail.hanu.vn

##### 4.3 PTR (Pointer)

- Record PTR (pointer) dùng để ánh xạ địa chỉ IP thành Hostname.
- Cú pháp:
[Host-ID.{Reverse_Lookup_Zone}] IN PTR [tên-miền]
Ví dụ:

10.0.0.100.in-addr.arpa. IN PTR hanu.vn.

##### 4.4 NS (Name Server)
- Chứa địa chỉ IP của DNS Server cùng với các thông tin về domain đó.
- Cú pháp : [tên miền] IN NS [tên của máy chủ tên miền]
Ví dụ mail.hanu.vn IN NS hanu.vn

####<a name="co-che"></a> 5. Cơ chế phân giải tên miền

- Giả sử người sử dụng muốn truy cập vào trang web có địa chỉ là http://www.google.com
- Trước hết chương trình trên máy người sử dụng gửi yêu cầu tìm kiếm địa chỉ IP ứng với tên miền http://www.google.com tới máy chủ quản lý tên miền (name Server) cục bộ thuộc mạng của nó (ISP DNS Server).
- Máy chủ tên miền cục bộ này kiểm tra trong cơ sở dữ liệu của nó có chứa cơ sở dữ liệu chuyển đổi từ tên miền sang địa chỉ IP của tên miền mà người sử dụng yêu cầu không. 
Trong trường hợp máy chủ tên miền cục bộ có cơ sở dữ liệu này, nó sẽ gửi trả lại địa chỉ IP của máy có tên miền nói trên (www.google.com)
- Trong trường hợp máy chủ tên miền cục bộ không có cơ sở dữ liệu về tên miền này nó thường hỏi lên các máy chủ tên miền ở cấp cao nhất (máy chủ tên miền làm việc ở mức Root). 
Máy chủ tên miền ở mức Root này sẽ trả về cho máy chủ tên miền cục bộ địa chỉ của máy chủ tên miền quản lý các tên miền có đuôi .com.
- Máy chủ tên miền cục bộ gửi yêu cầu đến máy chủ quản lý tên miền có đuôi (.com) tìm tên miền http://www.google.com. 
Máy chủ tên miền quản lý các tên miền .com sẽ gửi lại địa chỉ của máy chủ quản lý tên miền google.com.
- Máy chủ tên miền cục bộ sẽ hỏi máy chủ quản lý tên miền google.com này địa chỉ IP của tên miền http://www.google.com. 
Do máy chủ quản lý tên miền google.com có cơ sở dữ liệu về tên miền http://www.google.com nên địa chỉ IP của tên miền này sẽ được gửi trả lại cho máy chủ tên miền cục bộ.
- Máy chủ tên miền cục bộ chuyển thông tin tìm được đến máy của người sử dụng.
- PC của người dùng sẽ sử dụng địa chỉ IP này để mở một phiên kết nối TCP/IP đến Server chứa trang web có địa chỉ http://www.google.com
