## 发送文本邮件

```bash
/usr/sbin/sendmail -t -F SenderDisplayerName <<EOF
SUBJECT: sendmail test subject
TO: to_mail_address
CC: cc_mail_addres
MIME-VERSION: 1.0
Content-type: text/plain

mail content

EOF 
```

## 发送HTML邮件

```bash
/usr/sbin/sendmail -t -F SenderDisplayerName <<EOF
SUBJECT: sendmail test subject
TO: to_mail_address
CC: cc_mail_addres
MIME-VERSION: 1.0
Content-type: text/html

<html>
<body>
<table border="0" cellpadding="0" cellspacing="1" bgcolor="black">
<tr><td bgcolor="white">1</td><td bgcolor="white">content line 1</td></tr>
<tr><td bgcolor="white">2</td><td bgcolor="white">content line 2</td></tr>
</table>
</body>
</html>

EOF
```

## 发送组合消息（附件、图片等）

```bash
/usr/sbin/sendmail -t -F SenderDisplayerName <<EOF
SUBJECT: sendmail test subject
TO: to_mail_address
CC: cc_mail_addres
MIME-VERSION: 1.0
Content-Type: multipart/mixed; boundary="GvXjxJ+pjyke8COw"

--GvXjxJ+pjyke8COw
Content-type: text/html; charset=ISO-8859-15
Content-Transfer-Encoding: 7bit

<html>
<body>
<img src="cid:cid1">
<table border="0" cellpadding="0" cellspacing="1" bgcolor="black">
<tr><td bgcolor="white">1</td><td bgcolor="white">line 1</td></tr>
<tr><td bgcolor="white">2</td><td bgcolor="white">line 2</td></tr>
</table>
<img src="cid:cid2">
</body>
</html>

--GvXjxJ+pjyke8COw
Content-type: image/jpeg;name="a.jpg"
Content-Transfer-Encoding: base64
Content-ID: <cid1>
Content-Disposition: inline; filename="a.jpg"

$(base64 path/a.jpg)

--GvXjxJ+pjyke8COw
Content-type: image/jpeg; name="b.jpg"
Content-Transfer-Encoding: base64
Content-ID: <cid2>
Content-Disposition: inline; filename="b.jpg"

$(base64 path/b.jpg)

--GvXjxJ+pjyke8COw
Content-type: application/zip
Content-Transfer-Encoding: base64
Content-Disposition: attachement; filename=c.zip

$(base64 path/c.zip)

EOF
```

## 注意事项

多个邮件地址用,而不是;分隔。