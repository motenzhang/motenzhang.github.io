<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [轮询加水印](#%E8%BD%AE%E8%AF%A2%E5%8A%A0%E6%B0%B4%E5%8D%B0)
- [图片转换到BASE64](#%E5%9B%BE%E7%89%87%E8%BD%AC%E6%8D%A2%E5%88%B0base64)

<!-- /MarkdownTOC -->
# Editor's Choice: Intervention/Image
<a id="%E8%BD%AE%E8%AF%A2%E5%8A%A0%E6%B0%B4%E5%8D%B0"></a>
## 轮询加水印
```php
// 把原图强制转换成800px(resize)
// 并使其宽高按原图比例适用(aspectRatio)
// 同时不转换图片的横竖比例(orientate)(特指长图【宽窄 竖长】时保持生成图片的样式不变)
$img = Image::make($pureImg)->orientate()->resize(800, null, function ($constraint) {
    $constraint->aspectRatio();
    $constraint->upsize();
});
$watermark = Image::make($watermark);
$x = 0;
while ($x < $img->width()) {
    $y = 0;
    while($y < $img->height()) {
        $img->insert($watermark, 'top-left', $x, $y)->save(storage_path('app/public/cert/' . $filename));
        $y += $watermark->height() + 30;
    }
    $x += $watermark->width() + 30;
}
```
<a id="%E5%9B%BE%E7%89%87%E8%BD%AC%E6%8D%A2%E5%88%B0base64"></a>
## 图片转换到BASE64
```php
$data = (string) Image::make('public/bar.png')->encode('data-url');
```