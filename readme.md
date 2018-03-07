# 导入文件组件

## [在线demo](https://codepen.io/rubyisapm/pen/WjYVPp)

## 使用

从npm安装`ct-adc-importer`
```
npm install ct-adc-importer
```
在代码中引用
```
import Importer from 'ct-adc-importer';
//全局注册
Vue.component(Importer.name,Importer);

//局部注册

new Vue({
    ...
    components:{
        Importer
    },
    ...
})
```
## 参数说明

参数|描述|类型|默认值
--- | --- | --- | --- |
buttonText | 按钮文字 | String | '导入文件'
server | 上传接口地址 | String | ''
method | 上传方式 | String | 'POST'
accept | 和webuploader中accept配置项一致，包含extensions和mimeTypes两项。详见下方说明 | Object | null
fileSizeLimit | 可以接受的文件大小(单位为B) | Number | undefined
formData | 随文件上传的参数 | Object | {}
chunked | 是否分片上传文件 | Boolean | false
disabled | 按钮是否可用 | Boolean | false
tip | disabled为false时生效。当tip为''时不显示tip框 | String | ''
direction | tip的方向 | String | 'left'/'right'/'top'/'bottom'
hasInput | 是否需要input框 | Boolean | false
inputPlaceholder | input框的placeholder | String | '请上传一个文件'
headers | 自己需要配置的请求头 | Object | {}
auto | 自动或者是手动上传文件 | Boolean | false
sendAsBinary | 是否以二进制流方式上传 | Boolean | false
multiple | 是否支持文件多选 | Boolean | false
compress | 是否需要压缩 | false(Boolean) 或 Object(详细见下) | false

### accept

accept参数为一个对象，包含两项：
* extensions

以‘,’隔开 如 jpg,png,gif

* mimeTypes

文件类型,如'image/jpeg'. 请具体列出文件类型，避免类似'image/*'这样的写法。

### compress

```
{
    width: 1600,
    height: 1600,

    // 图片质量，只有type为`image/jpeg`的时候才有效。
    quality: 90,

    // 是否允许放大，如果想要生成小图的时候不失真，此选项应该设置为false.
    allowMagnify: false,

    // 是否允许裁剪。
    crop: false,

    // 是否保留头部meta信息。
    preserveHeaders: true,

    // 如果发现压缩后文件大小比原来还大，则使用原来图片
    // 此属性可能会影响图片自动纠正功能
    noCompressIfLarger: false,

    // 单位字节，如果图片大小小于此值，不会采用压缩。
    compressSize: 0
}
```

## 事件说明

### success

成功后的回调，参数为服务端响应内容

### error

失败后的回调，参数为错误信息。
错误信息为字符串，内容不固定。
如果是http且状态码需要客户端解析(状态码除去[200,300)和[500,600)后其他的状态码)，会返回如"http-401"这种错误。
如需解析，请先解析状态码，如果无状态码信息，则提示默认的提示如“上传失败，请重试”

ps: 上传后的逻辑层面的失败需要在外部处理。


### 依赖列表

此处的依赖列表是指需要用户手动引入到全局的js资源

1. [webuploader](http://fexteam.gz01.bdysite.com/webuploader/)

内部引用地址
http://static.uc108.com/cdn/webuploader/0.1.6/webuploader.html5only.min.js

