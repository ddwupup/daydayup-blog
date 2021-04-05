# 使用hexo+github pages+travis ci搭建个人博客

一直以来，很想搭建一个自己的博客。作为一个SE出身的菜鸡，很想自己用spring boot + vue.js自己写一个，奈何自己觉得太麻烦了，就一直没有去做，属实惭愧。昨天心血来潮，有用hexo搭建博客的想法。网上搜索了一些教程，以下就是自己搭建博客时遇到的一些问题。

参考：[【Hexo】使用Hexo+github pages+travis ci搭建好看的个人博客（一）](https://mfrank2016.github.io/breeze-blog/2020/05/02/hexo/hexo-start/#toc-heading-12)

## 遇到的坑

上面这个教程写的很好，清晰易懂，方便上手操作。

但是在，步骤 [五、使用 hexo 搭建博客](https://mfrank2016.github.io/breeze-blog/2020/05/02/hexo/hexo-start/#toc-heading-10)，出现了如下问题：

![image-20210405115502498](C:\Users\DDW\AppData\Roaming\Typora\typora-user-images\image-20210405115502498.png)

问题出现的原因是，在本地博客文件夹下执行hexo init时，该命令会去github上clone hexo-start这个项目，而在国内从github clone项目时，网速会很慢，有时甚至端开连接。

而在我们学校，最近校园网不知道怎么回事儿了，访问github都需要科学上网了。

一开始想到的解决方案（有坑）就是，自己手动去github上下载hexo-starter的zip包，并解压到博客目录，然后再执行hexo init，结果又出现了以下问题：

![image-20210405120735925](C:\Users\DDW\AppData\Roaming\Typora\typora-user-images\image-20210405120735925.png)

问题的原因是，将hexo-starter放到博客文件夹下面后，博客文件夹不是空的，而hexo init命令默认在空文件夹下执行该操作。

最终还是决定去修改执行hexo init命令的代码。hexo init命令执行后会去giihub上clone hexo-starter，而出现问题的原因是，在国内从github上clone项目网速慢，甚至端开连接。

我们可以使用国内的gihub镜像来clone项目。

打开文件：C:\Users\用户名\AppData\Roaming\npm\node_modules\hexo-cli\lib\console\init.js

![image-20210405121441136](C:\Users\DDW\AppData\Roaming\Typora\typora-user-images\image-20210405121441136.png)

把其中的 GIT_REPO_URL变量中的 github.com 替换成 github.com.cnpmjs.org ,将原来博客文件夹清空，然后直接执行hexo init ，就可以解决了。

后面按照参考连接中的步骤做，没有遇到什么坑，一个简单的博客就这样搭好了。