<!-- MarkdownTOC levels="2,3" autolink="true" autoanchor="true" style="unordered" markdown_preview="gitlab" -->

- [生成Word文档](#%E7%94%9F%E6%88%90word%E6%96%87%E6%A1%A3)

<!-- /MarkdownTOC -->
<a id="%E7%94%9F%E6%88%90word%E6%96%87%E6%A1%A3"></a>
## 生成Word文档
```php
// 使用 PhpWord
use PhpOffice\PhpWord\PhpWord;
// 创建对象
$phpWord = new PhpWord();
// 添加页面
$section = $phpWord->addSection();
// 添加标题
$phpWord->addTitleStyle(1, ['name' => '宋体', 'size' => 20]);
$section->addTitle('标题', 1);
// 添加文本
$section->addText('文本', ['name' => '宋体', 'size' => 10]);
// 添加超链接
$section->addLink('baidu.com', null, ['name' => '宋体', 'size' => 10, 'color' => '0000FF', 'underline' => 'single']);
// 添加线条
$lineStyle = array('weight' => 1, 'width' => 100, 'height' => 0, 'color' => 635552);
$section->addLine($lineStyle);
// 设置文档背景颜色（setColor 为自定义函数，详见新后台代码）
$phpWord->getSettings()->setColor('CAEACA');
// 添加目录
$section->addTOC(['name' => '宋体', 'size' => 10]);
// 设置格式
$writer = IOFactory::createWriter($phpWord, 'Word2007');
// 保存
$writer->save('new.docx');
```