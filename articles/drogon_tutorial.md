--- 
title: "ãDrogonãå¥é" 
emoji: "ð" 
type: "tech" 
topics: ["Web", "framework","http", "cpp", "html"] 
published: true
--- 
# ãDrogonãå¥é

ã¿ãªãããããã«ã¡ã¯ã
corkï¼ã³ã«ã¯ï¼ã§ãã
ä»æ¥ã¯Web ãã¬ã¼ã ã¯ã¼ã¯**Drogon**ãä½¿ãæ©ä¼ããã£ãã®ã§ããã¥ã¼ããªã¢ã«ã¨ãã¦èªåãã©ã®ãããªãã¨ãè¡ã£ãããæ¸ãæ®ãããã¨æãã¾ãã

-------

# 1. Drogonã¨ã¯
![](https://storage.googleapis.com/zenn-user-upload/11bf5cd4b3fc-20211223.jpg)
[å¬å¼HP](https://drogon.docsforge.com/)ã«ããã¨
> Drogonã¯ãC++14/17ãã¼ã¹ã®HTTPã¢ããªã±ã¼ã·ã§ã³ãã¬ã¼ã ã¯ã¼ã¯ã§ãã

ã¨æ¸ããã¦ãã¾ãã
**Drogon**ã¯C++ãç¨ãã¦ãã¾ãã¾ãªWebã¢ããªã±ã¼ã·ã§ã³ãµã¼ãã¼ãã­ã°ã©ã ãæ¸ãããã¨ãç¹å¾´ã§ãããLinuxã»macOSã»FreeBSDã»OpenBSDã»HaikuOSã»Windowsãªã©å¹åºãOSã«å¯¾å¿ãã¦ããã¯ã­ã¹ãã©ãããã©ã¼ã ã®ãã¬ã¼ã ã¯ã¼ã¯ã§ãã

ã¡ãªã¿ã«ã**Drogon**ã®ç±æ¥ã¯ã¢ã¡ãªã«ã®ãã¬ãã¢ãã¡"Game of Thrones"ã«åºã¦ãããã©ã´ã³ã®ååã ããã§ãã
â»ãã©ã´ã³ã®ç¶´ãã¯"Dragon"ã§ããã**Drogon**ã¯ããè¨ã£ãç±æ¥ããtypoã§ã¯ããã¾ããã

è©³ããã¯**Drogon**ã®[Getting Started](https://drogon.docsforge.com/master/)ãè¦ã¦ãã ããã

# 2. æ¦è¦
**Drogon**ãã¤ã³ã¹ãã¼ã«ãã¦ä½¿ã£ã¦ã¿ã¾ããã**Drogon**ã¯2018å¹´4æã«çºè¡¨ããããæ¯è¼çæ°ãããã¬ã¼ã ã¯ã¼ã¯ã®ãããæ¥æ¬èªã®æç®ãããªãå°ãªãã§ãããã®ããããããã**Drogon**ãä½¿ã£ã¦ã¿ããã¨ããäººåãã«ãã®è¨äºãå·ç­ãã¾ãããç§ã¯ããã¾ã§ç¥è­ã®ããæè¡èã§ã¯ãªãã®ã§ãè§£éãééã£ã¦ããé¨åããããã¨æãã¾ããè¨æ­£ãªã©ã¯ã³ã¡ã³ãã§éæåãä»ãã¦ãã¾ãã
ã¾ããMacã§éçºããããªã£ãããMacã®ä½¿ç¨ãåæã«è¨äºãæ¸ãã¦ãã¾ããï¼Linuxã»Windowsã®äººããããªããï¼


# 3. éçºç°å¢
- macOS Monterey 12.0.1
- intel Core i5
- dorogon 1.7.4

# 4. ç°å¢æ§ç¯
## 4.1 å¿è¦ãã¼ã«
MacOSãä½¿ç¨ããå ´åã¯ä»¥ä¸ã®ç°å¢ãå¿è¦ã§ãã
- git
- gcc/g++
- cmake
- jsoncpp
- uuid
- OpenSSL
- zlib

MacOSãä½¿ç¨ãã¦ããã®ã§ããã°ããã¹ã¦Homebrewã§ã¤ã³ã¹ãã¼ã«ãå¯è½ã§ããã¾ã ãHomebrewãã¤ã³ã¹ãã¼ã«ãããã¨ããªãã¨ããäººã¯[ãã¡ã](https://qiita.com/zaburo/items/29fe23c1ceb6056109fd)ãåèã«ã¤ã³ã¹ãã¼ã«ãã¦ã¿ã¦ãã ããã

```shellsession
$ brew update
$ brew install git
$ brew install gcc
$ brew install cmake
$ brew install jsoncpp
$ brew install ossp-uuid
$ brew install openssl
$ brew install zlib
```

## 4.2 ã¤ã³ã¹ãã¼ã«
ã¯ã¼ã¯ã¹ãã¼ã¹ãä½ã£ã¦ãGithubããã½ã¼ã¹ãã¯ã­ã¼ã³ãããã«ããã¾ãã
ãã®è¨äºã§ã¯ã¯ã¼ã¯ã¹ãã¼ã¹ã®ååããdrogon-testãããã¾ãã

```shellsession
$ mkdir drogon-test
$ cd drogon-test
$ git clone https://github.com/an-tao/drogon
$ cd drogon
$ git submodule update --init
$ mkdir build
$ cd build
$ cmake ..
$ make && sudo make install
```
ä¸è¨ã®ã³ãã³ããå©ãã¨ã¤ã³ã¹ãã¼ã«å®äºã§ãã
æ­£å¸¸ã«ã¤ã³ã¹ãã¼ã«ãåºæ¥ã¦ããã`$ drogon_ctl -v`ã¨ã³ãã³ããå©ãã¨ä»¥ä¸ã®åçã®ãããªè¡¨ç¤ºããããã¨æãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/14aa1271b5b1-20211221.png)*dorogonã®ãã¼ã¸ã§ã³ã¨ã­ã´*

ããã§ç°å¢æ§ç¯ã¯çµäºã§ãã
æ¬¡ããã¯å®éã«drogonãä½¿ã£ã¦ããã¾ãã

# 5. ãµã¼ãã¼ãç«ã¡ä¸ãã

## 5.1 ãã­ã¸ã§ã¯ããä½æãã

ã¾ãã`drogon-test`ã®ãã£ã¬ã¯ããªã¾ã§æ»ãã¾ãã
ä»¥ä¸ã®ã³ãã³ããæã¤ãã¨ã§ããã­ã¸ã§ã¯ããä½æã§ãã¾ãã
```shellsession
$ drogon_ctl create project [YOUR_PROJECT_NAME]
$ cd [YOUR_PROJECT_NAME]
```
ãã®è¨äºã§ã¯ãã­ã¸ã§ã¯ãåããsampleãã¨ãã¾ãã
ãã­ã¸ã§ã¯ããä½æããã¨ã ãããä»¥ä¸ã®ãããªãã£ã¬ã¯ããªæ§æã§ãã¡ã¤ã«ãçæãããã¨æãã¾ãã

```markdown
.sample
âââ build               # ãã«ãç¨ãã£ã¬ã¯ããª
âââ CMakeLists.txt      # cmakeç¨ (Makefileçæç¨)
âââ config.json         # Drogonã¢ããªã®è¨­å®ãã¡ã¤ã«
âââ controllers         # ã³ã³ãã­ã¼ã©ç®¡çç¨
âââ filters             # ãã£ã«ã¿ç®¡çç¨
âââ main.cc             # ã¢ããª ã¡ã¤ã³ãã¡ã¤ã«
âââ models              # ã¢ãã«ç®¡çç¨
â   âââ model.json
âââ views               # ãã¥ã¼ç®¡çç¨
```

`main.cc`ã¯ãããªæãã«ãªã£ã¦ããã¨æãã¾ãã

```cpp:main.cc
#include <drogon/drogon.h>
int main() {
    //Set HTTP listener address and port
    drogon::app().addListener("0.0.0.0",80);
    //Load config file
    //drogon::app().loadConfigFile("../config.json");
    //Run HTTP framework,the method will block in the internal event loop
    drogon::app().run();
    return 0;
}
```

ããã§ã¯`drogon`ã¨ããååç©ºéãä½¿ããã¦ãã¾ããã`using namespace drogon`ã§çç¥å¯è½ã§ããååç©ºéã«ã¤ãã¦ããããªãæ¹ã¯èª¿ã¹ã¦ã¿ã¦ãã ããã

## 5.2 ã­ã¼ã«ã«ãµã¼ãã¼ãç«ã¡ä¸ãã
ä»¥ä¸ã®ã³ãã³ããå©ãã¦ã­ã¼ã«ã«ãµã¼ãã¼ãç«ã¡ä¸ãã¦ã¿ã¾ãããã
```shellsession
$ cd build      # ãã«ãç¨ãã£ã¬ã¯ããªã¸ç§»å
$ cmake ..      # Makefileçæ
$ make          # ãã«ãã¨ã³ã³ãã¤ã«
$ ./sample      # å®è¡
```

[http://localhost](http://localhost)ã«ã¢ã¯ã»ã¹ããã¨ãä»¥ä¸ã®ããã«è¡¨ç¤ºããã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/afee4b04f6cc-20211222.png)

htmlãã¡ã¤ã«ãä½ãä½ã£ã¦ãªãã®ã§`404 Not Found`ã¨è¡¨ç¤ºãããããã¿ã¼ã«ã¯**Drogon**ã®ãã¼ã¸ã§ã³ãè¡¨ç¤ºããã¾ãã

## 5.3 ä¸­èº«ãè¡¨ç¤ºããã
ã³ã³ãã­ã¼ã©ãä¸ã¤ä½æããURLã«ã¢ã¯ã»ã¹ããã¨ãã«ãªã«ããè¿ã£ã¦ããããã«ãã¾ãã
ä»¥ä¸ã®ã³ãã³ããå©ãããtestctrlãã¨ããååã®ã³ã³ãã­ã¼ã©ãä½æãã¾ãã

```shellsession
$ cd ..
$ cd controllers
$ drogon_ctl create controller testctrl
```
ããã§ã`testctrl.h`ã¨`testctrl.cc`ãä½æãããã¨æãã¾ãã

**Drogon**ã§ã¯ã**ããããã¡ã¤ã«ã«ã«ã¼ãã£ã³ã°ããã½ã¼ã¹ãã¡ã¤ã«ã«å¦çãæ¸ã**ããä¸¡æ¹ã®ãã¡ã¤ã«ãä¿®æ­£ãã¦ããã¾ãã
URLã«ã¢ã¯ã»ã¹ãããã¨ãã«ã«ã¼ãã£ã³ã°ãããããã«ããããã¡ã¤ã«ã«`ã/ã`ã¨`ã/testã`ã¨ãã2ã¤ã®ãã¹ãè¿½å ãã¾ãã

```diff cpp: testctrl.h
    #pragma once //ã¤ã³ã¯ã«ã¼ãã«ã¼ã
    #include <drogon/HttpSimpleController.h>
    using namespace drogon;
    class testctrl:public drogon::HttpSimpleController<testctrl>
    {
    public:
        virtual void asyncHandleHttpRequest(const HttpRequestPtr& req, std::function<void (const HttpResponsePtr &)> &&callback) override;
        PATH_LIST_BEGIN
        //list path definitions here;
        //PATH_ADD("/path","filter1","filter2",HttpMethod1,HttpMethod2...);

+       PATH_ADD("/", Get, Post);
+       PATH_ADD("/test", Get);

        PATH_LIST_END
    };
```

ç¶ãã¦ã`testctrl.cc`ãä¿®æ­£ãã¦ããã¾ãã

```diff cpp:testctrl.cc
    #include "testctrl.h"
    void testctrl::asyncHandleHttpRequest(const HttpRequestPtr& req, std::function<void (const HttpResponsePtr &)> &&callback)
    {
        //write your application logic here
+       auto resp = HttpResponse::newHttpResponse();  // æ°ããã¬ã¹ãã³ã¹ã¤ã³ã¹ã¿ã³ã¹ãçæ
+       resp->setStatusCode(k200OK);  // HTTPã¹ãã¼ã¿ã¹ã³ã¼ã 200ã«è¨­å®
+       resp->setContentTypeCode(CT_TEXT_HTML);  // Header: Content typeãHTMLã«ãã
+       resp->setBody("<h1>Hello World!</h1>");  // Body:
+       callback(resp);
    }
```

ã§ã¯ãä»¥ä¸ã®ã³ãã³ããå©ãã¦å®è¡ãã¦ã¿ã¾ãããã

```shellsession
$ cd ..
$ cd build
$ cmake ..
$ make
$ ./sample
```
[http://localhost](http://localhost)ã¨[http://localhost/test](http://localhost/test)ã®ã©ã¡ãã«ã¢ã¯ã»ã¹ãã¦ã"Hello World!"ã¨è¡¨ç¤ºããã¦ããã¨æãã¾ãã

ãã®ããã«ãã£ãæ°è¡ã³ã¼ããå¤æ´ããã ãã§ãã³ã³ãã­ã¼ã©ã®è¨­å®ãå®äºãã¾ãã

# 6. Controllerå¥é
## 6.1 Controllerã¨ã¯
åã»ã©ãtestctrlãã¨ããã³ã³ãã­ã¼ã©ãä½æãã¦ãURLã«ã¢ã¯ã»ã¹ããæã«ã¬ã¹ãã³ã¹ãè¿ã£ã¦ããããã«ãã¾ããããããããControllerã¨ã¯ã©ã®ãããªå½¹å²ãæã£ã¦ããã®ã§ããããã

[å¬å¼HP](https://drogon.docsforge.com/master/controller-introduction/)ã«ããã¨ã
>ã³ã³ãã­ã¼ã©ã¯ãã©ã¦ã¶ããéããããªã¯ã¨ã¹ããå¦çãããã©ã¦ã¶ã¸ã®ã¬ã¹ãã³ã¹ãçæãã¾ã

ã¨æ¸ããã¦ãã¾ããè¦ããã«**éããã¦ããHTTPãªã¯ã¨ã¹ãã«ãã£ã¦ã©ããã£ãå¦çãè¡ãããæ±ºå®ãã**éè¦ãªé¨åã§ããã¨ããã¾ãã
åã»ã©ã¯**Drogon**ããµãã¼ããã¦ããã³ã³ãã­ã¼ã©ã®ä¸­ã§ãæãã·ã³ãã«ãª`HttpSimpleController`ãä½¿ç¨ãã¾ãããä»åã¯ããå®ç¨çãªã³ã³ãã­ã¼ã©ã§ãã`HttpController`ãä½¿ç¨ãããã¨æãã¾ãã

ä»åã¯[å¬å¼ãã­ã¥ã¡ã³ã](https://drogon.docsforge.com/master/controller-introduction/controller-httpcontroller/)ãåèã«èª¬æãã¦ããã®ã§ãç´°ããé¨åã§æ°ã«ãªãã¨ãããããã°ãã¡ããåç§ãã¦ãã ããã

## 6.2 HttpControllerã®çæ
`HttpSimpleController`ãçæããæã¨åãããã«`drogon_ctl`ã³ãã³ããç¨ãã¦çæãã¾ãã
éå¸¸ã®ã³ã³ãã­ã¼ã©çæã³ãã³ãã¯`-h`ãªãã·ã§ã³ãã¤ãããä»¥ä¸ã®ãããªã³ãã³ãã§çæãã¾ãã

```shellsession
$ drogon_ctl create controller -h <[namespace::]class_name>
```
ååç©ºéã¯çç¥å¯è½ã§ãããååç©ºéã®è¡çªãé¿ããããã«è¨­å®ãããã¨ããããããã¾ãã

ã¾ãã**Drogon**ã§ã¯ååç©ºéããã®ã¾ã¾URLã«åæ ããã¾ããä»åã¯[å¬å¼ãã­ã¥ã¡ã³ã](https://drogon.docsforge.com/master/controller-introduction/controller-httpcontroller/)ã«å¾ã£ã¦ä»¥ä¸ã®ã³ãã³ããå©ãã¦ã³ã³ãã­ã¼ã©ãä½æãã¾ããã

```shellsession
$ cd controllers
$ drogon_ctl create controller -h demo::v1::User
```
ããã§ãä»ããç·¨éããã³ã³ãã­ã¼ã©ã¯`http://localhost/demo/v1/user/{ã«ã¼ãã£ã³ã°ãããã¹}`ã«ã¢ã¯ã»ã¹ããã¨ãã®å¦çãè¡ãã¾ãã

`controllers`ã®ãã£ã¬ã¯ããªãè¦ã¦ã¿ãã¨`demo_v1_User.cc`ã¨`demo_v1_User.h`ã¨ãã2ã¤ã®ãã¡ã¤ã«ãæ°ãã«åºæ¥ã¦ããã¨æãã¾ãã

```cpp:demo_v1_User.cc
#include "demo_v1_User.h"
using namespace demo::v1;
// add definition of your processing function here
```

```cpp:demo_v1_User.h
#pragma once
#include <drogon/HttpController.h>
using namespace drogon;
namespace demo {
namespace v1 {
class User : public drogon::HttpController<User> {
   public:
    METHOD_LIST_BEGIN
    // use METHOD_ADD to add your custom processing function here;
    // METHOD_ADD(User::get,"/{2}/{1}",Get);//path is
    // /demo/v1/User/{arg2}/{arg1}
    // METHOD_ADD(User::your_method_name,"/{1}/{2}/list",Get);//path is
    // /demo/v1/User/{arg1}/{arg2}/list
    // ADD_METHOD_TO(User::your_method_name,"/absolute/path/{1}/{2}/list",Get);//path
    // is /absolute/path/{arg1}/{arg2}/list

    METHOD_LIST_END
    // your declaration of processing function maybe like this:
    // void get(const HttpRequestPtr& req,std::function<void (const
    // HttpResponsePtr &)> &&callback,int p1,std::string p2); void
    // your_method_name(const HttpRequestPtr& req,std::function<void (const
    // HttpResponsePtr &)> &&callback,double p1,int p2) const;
};
}  // namespace v1
}  // namespace demo
```

## 6.3 ãã¡ã¤ã«ã®ç·¨é
å¬å¼ãã­ã¥ã¡ã³ãã§ã¯`ã/info/{userId}ã`ã§ã¦ã¼ã¶ ID ã¨ååã JSON ã§è¿ãã¨ããå¦çãè¡ããã­ã°ã©ã ãæ¸ãã¦ããã®ã§ãå®è£ãã¦ã¿ããã¨æãã¾ãã
ï¼å¬å¼ãã­ã¥ã¡ã³ãã§ã¯`login`ãè¡ã£ã¦ãã¾ãããèª¬æãç°¡ç¥åããããã«çãã¦ãã¾ãï¼

ã¾ããããããã¡ã¤ã«ãç·¨éãã¾ãã

```diff cpp:demo_v1_User.h
    #pragma once
    #include <drogon/HttpController.h>
    using namespace drogon;
    namespace demo {
    namespace v1 {
    class User : public drogon::HttpController<User> {
    public:
        METHOD_LIST_BEGIN
        // use METHOD_ADD to add your custom processing function here;
        // METHOD_ADD(User::get,"/{2}/{1}",Get);//path is
        // /demo/v1/User/{arg2}/{arg1}
        // METHOD_ADD(User::your_method_name,"/{1}/{2}/list",Get);//path is
        // /demo/v1/User/{arg1}/{arg2}/list
        // ADD_METHOD_TO(User::your_method_name,"/absolute/path/{1}/{2}/list",Get);//path
        // is /absolute/path/{arg1}/{arg2}/list

+       METHOD_ADD(User::getInfo, "/info/{1}", Get);

        METHOD_LIST_END
        // your declaration of processing function maybe like this:
        // void get(const HttpRequestPtr& req,std::function<void (const
        // HttpResponsePtr &)> &&callback,int p1,std::string p2); void
        // your_method_name(const HttpRequestPtr& req,std::function<void (const
        // HttpResponsePtr &)> &&callback,double p1,int p2) const;

+       void getInfo(const HttpRequestPtr &req,
+                  std::function<void(const HttpResponsePtr &)> &&callback,
+                  std::string userId) const;
    };
    }  // namespace v1
    }  // namespace demo
```

ããã§GETã§ã¢ã¯ã»ã¹ãããå ´åã`User::getInfo()`ã«å¦çãæããããã«ãªãã¾ãã
æ¬¡ã«ã½ã¼ã¹ãã¡ã¤ã«ãç·¨éãã¦ããã¾ãã

```diff cpp:demo_v1_User.cc
    #include "demo_v1_User.h"
    using namespace demo::v1;
    // add definition of your processing function here

+  void User::getInfo(
+       const HttpRequestPtr &req,
+       std::function<void(const HttpResponsePtr &)> &&callback,
+       std::string userId
+   ) const {
+       // LOG_DEBUGã§ã³ã³ã½ã¼ã«ä¸ã«ãã­ã°ãè¡¨ç¤ºããã
+       LOG_DEBUG << "User " << userId << " get his information";
+
+       // ããã§ãã¼ã¯ã³ãåç§ãããããã¼ã¿ãåå¾ããå¦çãå¥ã£ãããã
+
+       Json::Value ret;
+
+       // JSONã«ãã¼ã¿ãæ ¼ç´
+       ret["result"] = "ok";
+       ret["user_name"] = "Jack";
+       ret["user_id"] = userId;
+       ret["gender"] = 1;
+
+       auto resp = HttpResponse::newHttpJsonResponse(ret);
+       callback(resp);
+   }
```

ããã§ç·¨éã¯å®äºã§ããå®éã«åä½ç¢ºèªããã¦è¦ã¾ãããã

## 6.4 åä½ç¢ºèª
ä»¥ä¸ã®ã³ãã³ããå©ãã¦ãã«ããã¦ãã ããã
```shellsession
$ cd ..
$ cd build
$ cmake ..
$ make
$ ./sample
```
[http://localhost/demo/v1/user/info/123](http://localhost/demo/v1/user/info/123)ã«ã¢ã¯ã»ã¹ããã¨ä»¥ä¸ã®ããã«ãªãã¨æãã¾ãã

![](https://storage.googleapis.com/zenn-user-upload/080fe9b34117-20211222.png)*/demo/v1/user/info/123*

ãã®ããã«ãJSONå½¢å¼ã®ãã¼ã¿ã¨ãã¦`{"gender":1,"result":"ok","user_id":"123","user_name":"Jack"}`ãè¿ã£ã¦ãã¾ãã
ã¾ããã·ã§ã«ã«ã¯ã­ã°ã¨ãã¦
```
20211222 06:55:26.984065 UTC 2622569 DEBUG [getInfo] User 123 get his information - demo_v1_User.cc:11
```
ãåºåããã¦ããã¨æãã¾ããï¼æéã¯èª­èã®ã¿ãªããã«ä¾å­ãã¾ããï¼

## 6.5 URLãã©ã¡ã¼ã¿ã®ãã¾ãã¾ãªè¨æ³

UserIDãURLã§è¡¨ç¾ããæã«ããä½¿ããã`/info?userId={xxx}`ã®ãããªURLã`demo_v1_User.h`ã«ä»¥ä¸ã®å¦çãè¿½å ãããã¨ã§`/info/{xxx}`ã¨åæ§ã«å¦çã§ãã¾ãã

```cpp
METHOD_ADD(User::getInfo,"/info?userId={1}",Get);
```

ããã§å¬å¼ãã­ã¥ã¡ã³ãã«æ¸ãã¦ããURLãã©ã¡ã¼ã¿ã®è¨æ³ãç´¹ä»ãã¾ãã

1. `{}` : éå¸¸ã®ãã©ã¡ã¼ã¿ãããã³ã°
2. `{1}, {2}`  : æ°å­ãå«ã¾ãããã©ã¡ã¼ã¿
3. `{anything}` : `{}` ã¨åãã§å¯èª­æ§åä¸ã®ããã«ä½ãããæå­åãå¥ãããã¨ãã§ãã
4. `{1:anything}, {2:xxx}` : `{1}, {2}` ã¨åãã§å¯èª­æ§åä¸ã®ããã®ãã®

å¬å¼ãã­ã¥ã¡ã³ãã§ã¯3çªç®ã®è¨æ³ãæ¨å¥¨ããã¦ãã¾ãã

ãããè¸ã¾ããã¨ä»¥ä¸ã®4ã¤ã¯ãã¹ã¦åãã«ã¼ãã£ã³ã°ãè¡ããã¾ãã

- "/users/{}/books/{}"
- "/users/{}/books/{2}"
- "/users/{user_id}/books/{book_id}"
- "/users/{1:user_id}/books/{2}"

ãããã¿ã¦ãããããã«ã3çªç®ãããªãå¯èª­æ§ãé«ããã¨ããããã¾ããéçºèç®ç·ã§ã3çªç®ãä½¿ç¨ããã»ããããã§ãããã

## 6.6 multiple path mapping
ä»¥ä¸ã®ã«ã¼ãã£ã³ã°ãè¡ãã°ãè¤æ°ã®URLãªã¯ã¨ã¹ãã1ã¤ã®ã³ã³ãã­ã¼ã©ã§å¦çã§ãã¾ãã
```cpp
ADD_METHOD_TO(UserController::handler1,"/users/.*",Post);
ADD_METHOD_TO(UserController::handler2,"/{name}/[0-9]+",Post); 
```
ã¾ããä¸ã®ã«ã¼ãã£ã³ã°ã§ã¯`/users/`ãåé ­ã«ãããã¹ã¦ã®URLã®å¦çãè¡ããä¸ã®ã«ã¼ãã£ã³ã°ã§ã¯`/{æå­å}/{æ°å­}`ã§è¡¨ç¾ããããã¹ã¦ã®URLã®å¦çãè¡ãã¾ãã

ãã ãããã ãã§ãªããã£ã¨è¤éãªè¨­å®ãè¡ãããå ´é¢ãåºã¦ããã¨æãã¾ãããããªæã¯æ­£è¦è¡¨ç¾ãç¨ãã¦è¨è¿°ãããã¨ãã§ãã¾ãã

## 6.7 Regular expressionï¼æ­£è¦è¡¨ç¾ï¼
å¬å¼ãã­ã¥ã¡ã³ãã«ã¯ä»¥ä¸ã®ãããªä¾ãè¼ã£ã¦ãã¾ãã
```cpp
ADD_METHOD_VIA_REGEX(UserController::handler1,"/users/(.*)",Post);
ADD_METHOD_VIA_REGEX(UserController::handler2,"/.*([0-9]*)",Post);
ADD_METHOD_VIA_REGEX(UserController::handler3,"/(?!data).*",Post);
```
1çªç®ã®ã«ã¼ãã£ã³ã°ã§ã¯ã`/users/`ãåé ­ã¨ãããã¹ã¦ã®URLã®å¦çãè¡ãã2çªç®ã®ã«ã¼ãã£ã³ã°ã§ã¯æ«å°¾ãæ°å­ã¨ãªããã¹ã¦ã®URLã®å¦çãè¡ãã3çªç®ã®ã«ã¼ãã£ã³ã°ã§ã¯`/data`ã§å§ã¾ããªããã¹ã¦ã®URLã®å¦çãè¡ãã¾ãã
ããããã¾ãä½¿ãã°ä»»æã®URLã«å¯¾ãã¦ãããªãå¦çãè¡ããã¨ãã§ãã¾ããã ãããç«¶åããªãããã«æ³¨æãã¾ãããã

æ­£è¦è¡¨ç¾ã«ã¤ãã¦ã¯è§£èª¬ãã¦ããæ¬ããµã¤ããç¡æ°ã«ããã®ã§èªåã«ãã£ãæç®ãåèã«èª¿ã¹ã¦è¦ã¦ãã ããã

# 7. Viewå¥é

## 7.1 Viewã¨ã¯
[å¬å¼ãã­ã¥ã¡ã³ã](https://drogon.docsforge.com/master/view/)ã«ããã¨ã
> ããã¯ã¨ã³ãã®ã¬ã³ããªã³ã°æè¡ãæä¾ãããµã¼ãã¼ãã­ã°ã©ã ãHTMLãã¼ã¸ãåçã«çæã§ããããã«ããé¨å

ã¨æ¸ããã¦ãã¾ããè¦ããã«**è¦ãç®(View)ã®é¨åãåçã«çæãããã¨ã®ã§ãã**ã®ã§ãã
**Drogon**ã¯JSPã¨åãããã«ãã­ã°ã©ã ã³ã¼ãã«HTMLãåãè¾¼ããã¨ã§ç´æçã«ã³ã¼ãã£ã³ã°ãããã¨ãã§ãã¾ãã

ä»åã[å¬å¼ãã­ã¥ã¡ã³ã](https://drogon.docsforge.com/master/view/)ã«æ²¿ã£ã¦è©±ãã¦ããã®ã§ããããªããã¨ãããã°ãã¡ããåèã«ãã¦ãã ããã

## 7.2 Viewã®ã³ã³ãã­ã¼ã©ã®çæ
ä»åã¯åãåã£ãGETãã©ã¡ã¼ã¿ãå±éããããã«ãããã¨æãã¾ãã
ã¾ãã¯ãã³ã³ãã­ã¼ã©ãå¿è¦ä¸å¯æ¬ ãªã®ã§ãListParametersãã¨ããååã®ã³ã³ãã­ã¼ã©ãä½æãã¾ãã
ä»¥ä¸ã®ã³ãã³ããå©ãã¦ãã ããã

```shellsession
$ cd controllers
$ drogon_ctl create controller ListParameters
```

ã¾ãã¯ãããããã¡ã¤ã«ãç·¨éãã¾ãã
ã/list_paraãã¨ããURLãã«ã¼ãã£ã³ã°ãã¾ãã

```diff cpp:ListParameters.h
    #pragma once
    #include <drogon/HttpSimpleController.h>
    using namespace drogon;
    class ListParameters : public drogon::HttpSimpleController<ListParameters> {
    public:
        virtual void asyncHandleHttpRequest(
            const HttpRequestPtr &req,
            std::function<void(const HttpResponsePtr &)> &&callback) override;
        PATH_LIST_BEGIN
        // list path definitions here;
        // PATH_ADD("/path","filter1","filter2",HttpMethod1,HttpMethod2...);
+       PATH_ADD("/list_para", Get);

        PATH_LIST_END
    };
```
æ¬¡ã«ã½ã¼ã¹ãã¡ã¤ã«ãå®è£ãã¾ãã
ããã§ã¯CSPï¼å¾è¿°ï¼ã«ã©ã®ãããªãã¼ã¿ãã©ã®ããã«æ¸¡ãããè¨è¿°ãã¦ãã¾ãã

```diff cpp:ListParameters.cc
    #include "ListParameters.h"
    void ListParameters::asyncHandleHttpRequest(
        const HttpRequestPtr &req,
        std::function<void(const HttpResponsePtr &)> &&callback) {
        // write your application logic here
        
+       // CSPã«æ¸¡ããã¼ã¿ãæ ¼ç´
+       auto para = req->getParameters();
+       HttpViewData data;
+       data.insert("title", "list parameters");
+       data.insert("parameters", para);
+
+       // ListParaCsp.cspã«ãã¼ã¿ãæ¸¡ã
+       auto res =
+           drogon::HttpResponse::newHttpViewResponse("ListParaCsp.csp", data);
+       callback(res);
    }
```
â»`ListParameters.cc`ã¯åèè¨äºã¨ã¯å°ãç°ãªãã¾ãã

## 7.3 CSPã¨ã¯
CSPã¨ã¯ããC++ Server Pagesãã®ç¥ã§ã**ãµã¼ããµã¤ãã§C++ã©ã¤ã¯ãªæ§æãå¦çããHTMLãçæãããã®**ã§ãã
Javaã«ãããJSPã®C++çã¨èããã¨ããããããã¨æãã¾ãã

CSPã¯**HTMLåã®ããã¹ã³ã¼ãã«ããã¦ã¯C++ãè¨è¿°ã§ãã**ãã¨ãç¹å¾´ã§ãã
ä»¥ä¸ã«CSPã«è¨æ³ãç´¹ä»ãããã¨æãã¾ãã

### I. `<%inc %>`
`<%inc %>`åã§ã¯ã `#include`ãããã¨ãå¯è½ã§ãã
ä¾ï¼`<%inc#include "xx.h" %>`

### II. `<%c++ %>`
`<%c++ %>`åã§ã¯ã**`#include`ãé¤ãC++ã®ã³ã¼ã**ãè¨è¿°å¯è½ã§ãã
ä¾ï¼`<c++ std:string name="drogon"; %>`

### â¢. `@@`
`@@`ã¯**ã³ã³ãã­ã¼ã©ããæ¸¡ããããã¼ã¿å¤æ°**ãè¡¨ãã¾ãã
åã»ã©ã®`ListParameters.cc`ã®`date`ãããã«ãããã¾ãã
éã«ãCSPãã`data`ã¨ããååã§ã¯å¼ã³åºãã¾ããã

### â£. `$$`
`$$`ã¯`<<`ã¨çµã¿åããããã¨ã§ãã¼ã¸ã«åºåãããã¨ãã§ãã¾ãã
C++ã§ãã`std::cout`ã¿ãããªãã®ã§ãã

### â¤. `[[ ]]`
`[[ ]]`åã®æå­åãã­ã¼ã¨ãã¦ã**ã³ã³ãã­ã¼ã©ããæ¸¡ããããã¼ã¿ããå¯¾å¿ãããã®ãè¦ã¤ãåºããè¡¨ç¤ºããã¾ãã**
ãã ããå¯¾å¿ãã¦ããæå­åãã¼ã¿åã¯`const char *`ã`std::string`ã`const std::string`ã®3ã¤ã§ãããã¨ã«æ³¨æãã¦ãã ãããã¾ããåãè¡ã®ä¸­ã§å²ã¾ãªããã°ããã¾ããã

### â¥. `{% %}`
`{% %}`åã§ã¯ãããããã`<%c++ %>`ãªã©ã§å®£è¨ãããå¤æ°ãè¡¨ç¤ºã§ãã¾ãã
ããªãã¡ã`{%val.xx%}`ã¨`<%c++ $$<<val.xx; %>`ã¯åç¾©ã§ãã
ãã ããåãè¡ã®ä¸­ã§å²ã¾ãªããã°ããã¾ããã

### â¦. `<%view %>`
`<%view %>`åã§ã¯**ãµããã¥ã¼ã¨ãã¦ãä»ã®CSPãã¡ã¤ã«ãå±éã§ãã¾ãã**
`header.csp`ãå­å¨ããã°ã`<%view header %>`ã¨è¨è¿°ãããã¨ã§ãã®å ´ã«`header.csp`ãå±éãããã¨ãã§ãã¾ãã
ããã«ãããåãã¼ã¸ã®å±éé¨åã1ã¤ã®ãã¼ã¸ã«ã¾ã¨ãããã¨ãå¯è½ã§ãã

## 7.4 CSPã®çæ
ã§ã¯ãå®éã«CSPãå®è£ãã¦ã¿ã¾ãããã
ãListParaCsp.cspãã¨ããååã®CSPãã¡ã¤ã«ãçæãã¦ç·¨éãã¾ãã

```shellsession
$ cd views
$ touch ListParaCsp.csp
```

```html:ListParaCsp.csp
<!DOCTYPE html>
<html>
<%c++
// dataããunorder_mapã¨ãã¦ãã©ã¡ã¼ã¿ãåå¾
auto para = @@.get<std::unordered_map<std::string, std::string>>("parameters");

// é©å½ã«å¤æ°å®£è¨ãã
auto name = "Drogon Inc.";
auto date = "2021.12.25";
%>
<head>
    <meta charset="UTF-8">
    <title>[[ title ]]</title>
</head>
<body>

<!-- å¤æ°å±éã¯ã©ã¡ãã§ãè¯ã -->
<p>Hello, {% name %}</p>
<p>Date: <%c++ $$ << date; %></p>

<%c++ if(para.size()>0){%>
<H1>Parameters</H1>
<table border="1">
    <tr>
        <th>name</th>
        <th>value</th>
    </tr>
    <!-- ã¤ãã¬ã¼ã·ã§ã³ã«ã¼ãã§ãã©ã¡ã¼ã¿ãå±é -->
    <%c++ for(auto iter:para){ %>
    <tr>
        <td>{% iter.first %}</td> 
        <td><%c++ $$<<iter.second;%></td>
    </tr>
    <%c++ } // endfor%>
</table>
<%c++ }else{ %>
<H1>no parameter</H1>
<%c++ } // endif %>
</body>
</html>
```

ã³ã¼ãã£ã³ã°ãçµãã£ãããã«ããã¦å®è¡ãã¦ã¿ã¾ãããã
```shellsession
$ cd ..
$ cd build
$ cmake ..
$ make
$ ./sample
```

åä½ç¢ºèªã®ããã«ã[http://localhost/list_para?p1=a&p2=b&p3=c](http://localhost/list_para?p1=a&p2=b&p3=c)ã«ã¢ã¯ã»ã¹ãã¦ã¿ãã¨ãä»¥ä¸ã®ãããªç»é¢ãè¡¨ç¤ºãããã¨æãã¾ããï¼æ¥ä»ãã¯ãªã¹ãã¹ã«ãªã£ã¦ããã®ã¯å·ç­æã®æ¥ä»ãã¯ãªã¹ãã¹ã ã£ãããã§ããããä»¥ä¸ã¯ãªã«ãèããªãã§ãã ãããï¼

![](https://storage.googleapis.com/zenn-user-upload/8bf8d3646f20-20211224.png =300x)

ã¾ããä»¥ä¸ã®ã³ãã³ããå©ããã¨ã§C++ã½ã¼ã¹ãã¡ã¤ã«ãçæããã³ã³ãã­ã¼ã©ï¼`ListParaCsp.h`ã¨`ListParaCsp.cc`ï¼ããview ãã£ã¬ã¯ããªä¸ã«èªåçæãã¦ãããæ©è½ãããã¾ãã

```shellsession
$ drogon_ctl create view ListParaCsp.csp
```

### ä½è«
CSPãã¡ã¤ã«ã`ListParameters.csp`ã¨ããã`ListParaCsp.csp`ã«ãã¦ãã¾ããåèã®ãã¡ã¤ã«åã§ã¯ãã«ããå¤±æãããããå¾èã®ãã¡ã¤ã«åã«å¤æ´ãã¾ãããï¼ãªã³ã«ã®ã¨ã©ã¼ãåºã¦ãã®ã§ããèª¿ã¹ã¦ãè§£æ±ºç­ãããããªãã£ãã®ã§ãæ¸ãååãå¤æ´ãã¾ããããã®å¤æ´ã¯ç¾æ®µéã§ã¯åé¡ãªãã§ããããã¾ãè¯ããªãå¤æ´ã ã¨æãã¾ããï¼

# 8. æå¾ã«
ã¿ãªããããã£ã¦è¦ã¦ãããã§ããã§ãããããC++ã«æ£ãã¦ããªãäººã«ã¨ã£ã¦ã¯å°ãé£ããã£ãããããã¾ããããä½¿ã£ã¦è¦ã¦ãããã®ã§ã¯ãªãã§ããããã
ã¾ããåèªèº«ãèª¿ã¹ãªããå·ç­ãã¦ããã®ã§è¨èãééã£ã¦ããããçè§£ãééã£ãããã¦ããé¨åããããã¨æãã¾ãããã®ç¹ã«ã¤ãã¦ã¯éæææãã¦ããã ããã¨ãããããã§ãã

ã¾ãããã®è¨äºã®å·ç­ã«ãããä¸è¨ã®è¨äºã«ã¯å¤§å¤ãããã«ãªãã¾ããããã®å ´ããåããã¦æè¬ç³ãä¸ãã¾ãããã ããã®è¨äºã®ã³ã¼ããåèã«ã¯ãã¦ãããã®ã®å¤æ´ãã¦ããé¨åã®å¤ãããã®ã§ãä¸¡æ¹ãåèã«ããªããä½æ¥­ãããã¨ã¯ãããããã¾ããã
https://rightcode.co.jp/blog/information-technology/fastest-c-web-framework-drogon-quick-start
https://rightcode.co.jp/blog/information-technology/fastest-c-web-framework-drogon-controller
https://rightcode.co.jp/blog/information-technology/fastest-c-web-framework-drogon-view
