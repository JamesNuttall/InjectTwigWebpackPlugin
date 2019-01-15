inject-twig-webpack-plugin
===

[![NPM](https://nodei.co/npm/inject-twig-webpack-plugin.png)](https://nodei.co/npm/inject-twig-webpack-plugin/)

based off [inject-html-webpack-plugin](https://github.com/ali322/inject-html-webpack-plugin). Takes js/css files and using the twig view.register syntax injects the files.

Install
===

```javascript
npm install inject-twig-webpack-plugin --save--dev
```

Usage
===

add plugin in your webpack.config.js

```javascript
var InjectTwigPlugin = require('inject-twig-webpack-plugin');

module.exports = {
    entry:{
        index:"./index.js"
    },
    module:{
        loaders:[
            ...
        ]
    },
    output:{
        path:'./dist',
        filename:'[name].min.js'
    },
    plugins:[
        new InjectTwigPlugin({
            transducer: function (filename) {
                return "/assets/js/vue/dist/"+filename;
            },
            filename: '../../../../templates/_layout/_footer.html',
            chunks:['filters']
        })
    ]
}
```

then add below placeholders into html file

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <!-- start:css -->
  <!-- end:css -->
</head>
<body>
  <!-- start:js -->
  <!-- end:js -->
</body>
</html>
```

Output
===

```
<!-- start:js --> 
{% do view.registerJsFile(siteUrl ~ "/assets/js/vue/dist/filters.c38144da9d3ebd917778.js") %}
<!-- end:js -->
```

## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)