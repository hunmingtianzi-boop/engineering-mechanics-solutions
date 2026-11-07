# 编译和预览检查

## 编译

在源稿目录保留 figures/ 相对路径。优先使用已安装的 XeLaTeX，在临时目录编译，等 PDF 核验通过后再写入交付目录。更新带书签的文件时按编译器日志完成必要的第二轮编译。用户需要可编辑稿时一并交付 .tex 和其引用的题图。

模板默认用 Windows 的 SimSun 和 SimHei。其他环境可将模板中的字体名换成实际安装的中文字体。用 Windows 便携版 Tectonic 时，如果引擎找不到系统字体，在临时目录写入下列 fonts.conf，将进程的 FONTCONFIG_FILE 指向该文件的绝对路径，再从 .tex 所在目录编译。

    <?xml version="1.0"?>
    <!DOCTYPE fontconfig SYSTEM "urn:fontconfig:fonts.dtd">
    <fontconfig>
      <dir>C:/Windows/Fonts</dir>
      <cachedir prefix="relative">font-cache</cachedir>
    </fontconfig>

    & $tectonic -X compile --keep-logs --outdir $buildDir homework.tex

遇到中文缺失时，检查成品中的中文字体是否真正嵌入并具有 Unicode 映射。更换字体后重新验证显示和文本提取。

## 验收

- 用 pdftoppm -png -r 120 或同类工具渲染全部页，查看题号、公式、题图和页眉。放大检查标注箭头的起点与方向，以及标签是否遮住尺寸和题目数据。
- 用浏览器 PDF 渲染器再打开成品，至少确认一页有公式和图的中文题干、解答实际可见。条件允许时，用 PDF.js 获取每一页的文本并核对中文题号与标题。仅有 Poppler 图像正常不足以排除浏览器漏显中文。
- 核对每道题的题号、题图、解答和答案在同一页。若模板报告题块超高或日志报告内容超出版心，先裁掉题图留白、调整并排方式或缩减间距，再重新编译检查。
- 核对题目清单、页数、页眉署名和导出文件。交付目录使用经过检查的编译版本。
