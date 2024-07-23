# 使用InternStudio创建开发机环境并完成测试

##  完成SSH连接与端口映射并运行`hello_world.py`

### SSH连接

- 首先进入InternStudio网站：https://studio.intern-ai.org.cn/console/instance，创建开发机：

![image-20240723160302606](D:\桌面\InternStudioNotes\使用InternStudio创建开发机环境并完成测试.assets\image-20240723160302606.png)

- 开发机相关配置：

![image-20240723160335331](D:\桌面\InternStudioNotes\使用InternStudio创建开发机环境并完成测试.assets\image-20240723160335331.png)

- 点击SSH连接复制登录命令在本地Powershell上登陆：

![image-20240723162806837](D:\桌面\InternStudioNotes\使用InternStudio创建开发机环境并完成测试.assets\image-20240723162806837.png)

- 配置SSH密钥进行SSH远程连接，Windows机器上`C:\Users\username\.ssh\id_rsa.pub`中存储着**SSH公钥**，如果没有输入`ssh-keygen -t rsa`一路回车生成。回到开发机平台，在首页点击配置**SSH Key**，接着点击**添加SSH公钥**。完成SSH Key创建以后，重启**终端**进行远程连接，就会跳过密码输入这一步了。

### 端口映射

- **端口映射**是一种网络技术，它可以将外网中的任意端口映射到内网中的相应端口，实现内网与外网之间的通信。通过端口映射，可以在外网访问内网中的服务或应用，实现跨越网络的便捷通信。

- **为什么需要端口代理**：当我们直接从外部网络访问开发机时，可能会遇到代理服务器的阻碍，导致某些UI资源无法加载完全。这种情况在Web应用中比较常见，因为现代Web应用通常依赖于大量的静态资源（如JavaScript文件、CSS文件、图片等），这些资源可能托管在不同的CDN（内容分发网络）上。如果代理服务器阻止了这些资源的加载，Web应用的UI可能会显示不完整。通过端口映射，将外部网络的访问请求转发到本地主机，我们可以避开这些代理服务器的限制，从而确保所有资源都能正确加载。这是因为在本地访问时，所有的网络请求都是直接在本地网络中完成的，不会经过外部的代理服务器。

- 点击自定义服务后复制第一条命令**在本地机器终端中执行**：

  ![image-20240723165416999](D:\桌面\InternStudioNotes\使用InternStudio创建开发机环境并完成测试.assets\image-20240723165416999.png)

![image-20240723165817146](D:\桌面\InternStudioNotes\使用InternStudio创建开发机环境并完成测试.assets\image-20240723165817146.png)

### 运行`hello_world.py`

在开发机创建源文件`hello_world.py`并运行，需要`pip install gradio==4.29.0`命令安装以下依赖包

```python
import socket
import re
import gradio as gr
 
# 获取主机名
def get_hostname():
    hostname = socket.gethostname()
    match = re.search(r'-(\d+)$', hostname)
    name = match.group(1)
    
    return name
 
# 创建 Gradio 界面
with gr.Blocks(gr.themes.Soft()) as demo:
    html_code = f"""
            <p align="center">
            <a href="https://intern-ai.org.cn/home">
                <img src="https://intern-ai.org.cn/assets/headerLogo-4ea34f23.svg" alt="Logo" width="20%" style="border-radius: 5px;">
            </a>
            </p>
            <h1 style="text-align: center;">☁️ Welcome {get_hostname()} user, welcome to the ShuSheng LLM Practical Camp Course!</h1>
            <h2 style="text-align: center;">😀 Let’s go on a journey through ShuSheng Island together.</h2>
            <p align="center">
                <a href="https://github.com/InternLM/Tutorial/blob/camp3">
                    <img src="https://oss.lingkongstudy.com.cn/blog/202406301604074.jpg" alt="Logo" width="20%" style="border-radius: 5px;">
                </a>
            </p>

            """
    gr.Markdown(html_code)

demo.launch()
```

![image-20240723171500643](D:\桌面\InternStudioNotes\使用InternStudio创建开发机环境并完成测试.assets\image-20240723171500643.png)

