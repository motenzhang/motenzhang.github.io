<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [git 免密](#git-%E5%85%8D%E5%AF%86)
- [配置信息](#%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF)
- [添加已有文件夹到git仓库](#%E6%B7%BB%E5%8A%A0%E5%B7%B2%E6%9C%89%E6%96%87%E4%BB%B6%E5%A4%B9%E5%88%B0git%E4%BB%93%E5%BA%93)
- [更新github上fork别人的代码](#%E6%9B%B4%E6%96%B0github%E4%B8%8Afork%E5%88%AB%E4%BA%BA%E7%9A%84%E4%BB%A3%E7%A0%81)
- [git完整迁移\(包含代码 提交 分支等所有文件\)](#git%E5%AE%8C%E6%95%B4%E8%BF%81%E7%A7%BB%E5%8C%85%E5%90%AB%E4%BB%A3%E7%A0%81-%E6%8F%90%E4%BA%A4-%E5%88%86%E6%94%AF%E7%AD%89%E6%89%80%E6%9C%89%E6%96%87%E4%BB%B6)

<!-- /MarkdownTOC -->
<a id="git-%E5%85%8D%E5%AF%86"></a>
## git 免密
`cd ~ `  
`cat ~/.ssh/id_rsa.pub `  
`cat ~/.ssh/id_rsa.pub`  
<a id="%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF"></a>
## 配置信息
```bash
# 不加global选项意味仅当前项目使用如下配置
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global user.password 1234 #慎用
```
<a id="%E6%B7%BB%E5%8A%A0%E5%B7%B2%E6%9C%89%E6%96%87%E4%BB%B6%E5%A4%B9%E5%88%B0git%E4%BB%93%E5%BA%93"></a>
## 添加已有文件夹到git仓库
```bash
cd ucd
git init
git remote add origin git@10.1.7.15:ucd/ucd.git
git add .
git commit -m "first commit"
git push -u origin master

git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/motenzhang/condenast.git
git push -u origin master
```
<a id="%E6%9B%B4%E6%96%B0github%E4%B8%8Afork%E5%88%AB%E4%BA%BA%E7%9A%84%E4%BB%A3%E7%A0%81"></a>
## 更新github上fork别人的代码
```bash
# 1.克隆自己的到本地
git clone https://github.com/motenzhang/moodle.git
# 2.添加源/上游地址 upstream即别人代码的git地址
git remote add upstream https://github.com/moodle/moodle.git
# 3.拉取源地址到本地
git fetch upstream
# 4.获取master代码并与源代码合并
git checkout master
git merge upstream/master
# 5.推送master代码到自己github仓库
git push origin master
# 11.第二种方法 删除之前fork的代码 重新fork
```
<a id="git%E5%AE%8C%E6%95%B4%E8%BF%81%E7%A7%BB%E5%8C%85%E5%90%AB%E4%BB%A3%E7%A0%81-%E6%8F%90%E4%BA%A4-%E5%88%86%E6%94%AF%E7%AD%89%E6%89%80%E6%9C%89%E6%96%87%E4%BB%B6"></a>
## git完整迁移(包含代码 提交 分支等所有文件)
```bash
mkdir temp_dir
cd temp_dir
git clone --bare git@10.1.7.15:old/old.git
cd old.git
git remote set-url --push origin https://github.com/motenzhang/new.git
git push --mirror
cd ..
# 删除本地
rm -rf project_name.git 
```