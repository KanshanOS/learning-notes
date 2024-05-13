# Charles 抓包重写

## 前言

- 确保设备不要开启代理软件
- 确保设备连接相同网络

## Mac 安装证书

- 点击 `Charles` >  `Help` > `SSL Proxying` > `Install Charles Root Certificate`

- 在系统`钥匙串访问`中找到 `Charles Proxy CA`证书，并设置为 `始终信任`

  ![image-20231124105123123](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124105123123.png)

  ![image-20231124105255791](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124105255791.png)

- `Proxy` > `Proxy Setting`

  ![image-20231124132858006](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124132858006.png)

- `Proxy` > `SSL Proxy Settings`

  ![image-20231124133038922](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124133038922.png)

## iPhone 安装证书

- 点击 `Charles` >  `Help` > `SSL Proxy` > `Install Charles Root Certificate on a Mobile Device or Remote Browser`

  ![image-20231124111356550](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124111356550.png)

- 确保 iPhone 与 Mac 连接同一网络，在所连接详情页`配置代理` > `手动` > `服务器&端口`填写上图配置，**点击「存储」后，Mac 端会弹出询问窗口，点击 「Allow」按钮进行**

  ![image-20231128112224306](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231128112224306.png)

- 手机端使用 Safari 浏览器打开：[chls.pro/ssl](chls.pro/ssl)，点击「允许」进行下载，**若下载失败，需检查手机、电脑是否开启代理软件**

  ![IMG_A6EFADE5A53F-1](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/IMG_A6EFADE5A53F-1.jpeg)

- `iPhone` >`设置` > `通用` > `VPN与设备管理`找到 `Charles Proxy CA`  描述文件根据引导进行安装

- `iPhone` >`设置` > `通用` > `关于本机`>`证书信任设置` 找到 `Charles Proxy CA`开启完全信任

> 至此，已经可以通过 Charles 抓取手机的请求包了



## 重写请求

1. 找到需要重写的请求，然后右键点击：`Breakpoints` ，以：百度首页获取搜索历史记录接口为例

   ![image-20231124134031517](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124134031517.png)

2. 直接点击请求创建断点的方式适用于 URL 不会变的情况，但类似上面这种 URL 会携带可变参数的请求，需要点击：`Proxy` > `Breakpoints Settings`找到需要的请求，将**变化的参数（Query）全部删除**

   ![image-20231124135747583](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124135747583.png)

3. 点击 「`Edit Request`」按钮编辑请求信息，编辑完成后点击「`Execute`」按钮发送请求

   ![image-20231124134756764](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124134756764.png)

4. 点击 「`Edit Response`」按钮编辑响应信息，编辑完成后点击「`Execute`」按钮返回响应数据

   ![image-20231124135057180](./images/Charles%20%E6%8A%93%E5%8C%85%E9%87%8D%E5%86%99%20/image-20231124135057180.png)

























