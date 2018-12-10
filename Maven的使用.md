# IDEA配置Maven
## 更改配置文件

更改配置文件
```
将安装的maven路径下拷贝一份settings.xml文件，到一下路径
C:\Users\ICEMARK\.m2 
```

进行一下修改

- 配置本地仓库
```
<localRepository>F:\Soft\Maven\apache-maven-3.5.3\repository</localRepository>
```
- 配置远程仓库

```
<mirror>
<id>nexus</id>
<mirrorOf>*</mirrorOf>
<name>Nexus aliyun</name>
<url>http://maven.aliyun.com/nexus/content/groups/public/</url>
</mirror>
```
## 新疆Maven项目
1. 选择新建项目的类型
![image](https://note.youdao.com/yws/public/resource/a2dbde6b45bafd71a42fa605091f5de9/xmlnote/2E6BFDBD724340A6A6409AC07208367B/7773)
2. 项目的信息
![image](https://note.youdao.com/yws/public/resource/a2dbde6b45bafd71a42fa605091f5de9/xmlnote/47E1AACADF504ACA8B66D96756BE9F67/7782)
3. Maven信息
![image](https://note.youdao.com/yws/public/resource/a2dbde6b45bafd71a42fa605091f5de9/xmlnote/7B24E1F2193D45BDBE0179D91450321E/7789)

4. 项目的路径信息
![image](https://note.youdao.com/yws/public/resource/a2dbde6b45bafd71a42fa605091f5de9/xmlnote/9B4598C2A440400D877B0AF99650BBAE/7795)
