# cli
Cmmand Line Interface


```
npm install bluebird --save // 实现 Promise 的库
npm install fs-extra --save // 文件操作
npm install commander --save // 处理命令行工具的包，可处命令参数等
```


lib/generateStructure.js
```
var Promise = require("bluebird"),
    fs = Promise.promisifyAll(require('fs-extra'));

function generateStructure(project){
  return fs.copyAsync('structure', project,{clobber: true})
    .then(function(err){
      if (err) return console.error(err)
    })
}

module.exports = generateStructure;
```

bin/index.js
```
#!/usr/bin/env node
var gs = require('../lib/generateStructure');

gs("demo");
```
```
#!/usr/bin/env node

var program = require('commander'),
    gs = require('../lib/generateStructure');

program
  .version(require('../package.json').version)
  .usage('[options] [project name]')
  .parse(process.argv);

var pname = program.args[0]

gs(pname);
```
