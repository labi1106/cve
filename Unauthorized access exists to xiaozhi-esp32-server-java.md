# Vulnerability Description
The `/api/user/queryUsers` interface in Xiaozhi ESP32 Server Java v3.0.0 has an unauthorized access vulnerability. An attacker could access this interface without logging in, allowing it to return the phone numbers and email addresses of all registered accounts.

# Vulnerability Analysis

Vulnerable class file: src/main/java/com/xiaozhi/common/config/WebMvcConfig.java

![](https://github.com/labi1106/picx-images-hosting/raw/master/xiaozhi-esp32-server-java/image.migtm8th.webp)

The configuration only excludes /api/user/login and /api/user/register, but the interceptor's internal logic marks the entire /api/user/ path as a public path.

In src/main/java/com/xiaozhi/common/interceptor/AuthenticationInterceptor.java, accessing /api/user without logging in results in unauthorized access.

![](https://github.com/labi1106/picx-images-hosting/raw/master/xiaozhi-esp32-server-java/image.2dp4y11ndb.webp)

The implemented interface is src/main/java/com/xiaozhi/controller/UserController.java

![](https://github.com/labi1106/picx-images-hosting/raw/master/xiaozhi-esp32-server-java/image.7snnggh9g1.webp)

Directly accessing the route /api/user/queryUsers enables unauthorized access.

# Vulnerability Reproduction

Directly access the vulnerable address[http://110.40.176.82:8084/api/user/queryUsers](http://110.40.176.82:8084/api/user/queryUsers)or[http://connectai.chat/api/user/queryUsers](http://connectai.chat/api/user/queryUsers)

![](https://github.com/labi1106/picx-images-hosting/raw/master/xiaozhi-esp32-server-java/image.8ok4vwr3sg.webp)

![](https://github.com/labi1106/picx-images-hosting/raw/master/xiaozhi-esp32-server-java/image.1lc9galug3.webp)

Successful unauthorized access


