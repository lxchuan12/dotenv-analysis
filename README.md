# dotenv-analysis

## 前言

## dotenv 的作用

[dotenv](https://github.com/motdotla/dotenv)

[dotenv-expand](https://github.com/motdotla/dotenv-expand)

.env

[vue-cli .env](https://cli.vuejs.org/zh/guide/mode-and-env.html#%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)

[create-react-app .env](https://create-react-app.dev/docs/adding-custom-environment-variables/#what-other-env-files-can-be-used)


## 


## 

```.env
NAME=若川
AGE=18
BLOG=https://lxchuan12.gitee.io
MP_WEIXIN='若川视野'
```

### 简单实现

```js
const fs = require('fs')
const path = require('path')

const parse = function parse(src){
    const obj = {};
    src.toString().split('\n').forEach(function(line, index){
        const keyValueArr = line.split('=');
        key = keyValueArr[0];
        val = keyValueArr[1] || '';
        obj[key] = val;
    });
    return obj;
}

const config = function(){
    let dotenvPath = path.resolve(process.cwd(), '.env');
    const parsed = parse(fs.readFileSync(dotenvPath, 'utf-8'));

    Object.keys(parsed).forEach(function(key){
        if(!Object.prototype.hasOwnProperty.call(process.env, key)){
            process.env[key] = parsed[key];
        }
    });

    return parsed;
};

console.log(config());
console.log(process.env);

module.exports.config = config;
module.exports.config = parse;
```