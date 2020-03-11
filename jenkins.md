```bash
# 服务器构建脚本
if [ $version -gt 10 ];then
  echo "你回滚的版本过旧，禁止回滚"
else if [ $version == 0 ];then
  ssh apache@10.38.15.203 "cd /var/www/newsys_backend/newsys && git pull"
    ssh apache@10.38.15.214 "cd /var/www/newsys_backend/newsys && git pull"
else
  echo "version: $version"
    ssh apache@10.38.15.203 "cd /var/www/newsys_backend/newsys &&git reset --hard  HEAD~$version&& git pull"
    ssh apache@10.38.15.214 "cd /var/www/newsys_backend/newsys &&git reset --hard  HEAD~$version&& git pull"
fi
fi
```