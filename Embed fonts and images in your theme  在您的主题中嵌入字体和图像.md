

Learn how to include assets, such as fonts and images, in your theme.  
学习如何在您的主题中包含资产，例如字体和图像。

Loading remote content 加载远程内容

For Obsidian to work offline and to preserve user privacy, themes [aren't allowed](https://docs.obsidian.md/Developer+policies) to load remote content over the network. For more information, refer to [Theme guidelines > Keep resources local](https://docs.obsidian.md/Themes/App+themes/Theme+guidelines#Keep%20resources%20local)  
为了使 Obsidian 离线工作并保护用户隐私，主题 [不允许](https://docs.obsidian.md/Developer+policies) 通过网络加载远程内容。有关更多信息，请参阅 [主题指南 > 保持资源本地](https://docs.obsidian.md/Themes/App+themes/Theme+guidelines#Keep%20resources%20local)

## 0.1 Use data URLs 使用数据 URL

To include assets such as fonts, icons, and images in your theme, you need to _embed_ them in the CSS file by passing a [data URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs) to the [url()](https://developer.mozilla.org/en-US/docs/Web/CSS/url) function.  
要在您的主题中包含资产，例如字体、图标和图像，您需要通过将 [数据 URL](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs) 传递给 [url()](https://developer.mozilla.org/en-US/docs/Web/CSS/url) 函数来 _嵌入_ 它们到 CSS 文件中。

To create a data URL for your assets, create a URL using the following format:  
要为您的资产创建数据 URL，请使用以下格式创建 URL：

```css
url("data:<MIME_TYPE>;base64,<BASE64_DATA>")
```

- Replace `<MIME_TYPE>` with the MIME type for your asset. If you don't know it, refer to [Common MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types).  
    将`<MIME_TYPE>`替换为您的资产的 MIME 类型。如果您不知道，请参考[常见 MIME 类型](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)。
- Replace `<BASE64_DATA>` with the [Base64](https://en.wikipedia.org/wiki/Base64) encoded representation of your asset.  
    将`<BASE64_DATA>`替换为您的资产的[Base64](https://en.wikipedia.org/wiki/Base64)编码表示。

The following example embeds a GIF file as a background image:  
以下示例将 GIF 文件嵌入为背景图像：

```css
h1 {
  background-image: url("data:image/gif;base64,R0lGODdhAQADAPABAP////8AACwAAAAAAQADAAACAgxQADs=")
}
```

## 0.2 Encode your assets 编码您的资产

For instructions on how to encode an asset into base64, refer to [Encoding data into base64 format](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs#encoding_data_into_base64_format).  
有关如何将资产编码为 base64 的说明，请参阅[将数据编码为 base64 格式](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs#encoding_data_into_base64_format)。

You can also use one of the many free online tools for encoding.  
您还可以使用许多免费的在线工具进行编码。

For fonts: 字体：

- [Woff2Base](https://hellogreg.github.io/woff2base/) for WOFF2 font files  
    [Woff2Base](https://hellogreg.github.io/woff2base/) 用于 WOFF2 字体文件
- [Aspose](https://products.aspose.app/font/base64) supports a wide variety of font formats  
    [Aspose](https://products.aspose.app/font/base64) 支持多种字体格式

For images: 对于图像：

- [WebSemantics](https://websemantics.uk/tools/image-to-data-uri-converter/) converts JPEG, JPG, GIF, PNG, SVG  
    [WebSemantics](https://websemantics.uk/tools/image-to-data-uri-converter/) 转换 JPEG、JPG、GIF、PNG、SVG
- [Base64 Guru](https://base64.guru/converter/encode/image) supports a wide variety of image formats  
    [Base64 Guru](https://base64.guru/converter/encode/image) 支持多种图像格式
- [Yoksel URL-encoder for SVG](https://yoksel.github.io/url-encoder/) optimized for SVG files  
    [Yoksel URL-encoder for SVG](https://yoksel.github.io/url-encoder/) 针对 SVG 文件进行了优化

## 0.3 Consider file size 考虑文件大小

Embedding assets increases the file size of your theme, which may lead to poor performance in the following situations:  
嵌入资产会增加主题的文件大小，这可能会导致在以下情况下性能不佳：

- Downloading and updating your theme from the community theme directory.  
    从社区主题目录下载和更新您的主题。
- Loading and using your theme in the Obsidian app.  
    在 Obsidian 应用中加载和使用您的主题。
- Editing your theme in a code editor. Consider breaking up your theme into multiple files using a CSS preprocessor, such as [Sass](https://sass-lang.com/) or [Less](https://lesscss.org/).  
    在代码编辑器中编辑您的主题。考虑使用 CSS 预处理器（如[Sass](https://sass-lang.com/)或[Less](https://lesscss.org/)）将主题拆分为多个文件。