# 创建vue项目

1. 检查nodejs环境 `node -v`,nodejs要求的版本至少要求18.0
2. `npm create vue@latest`创建项目,初始化名字,和基本配置
3. `npm run dev`运行vue3项目


# 目录结构
>![[Pasted image 20231226120949.png]]

# 使用element-plus

1. 使用npm下载
```npm
npm install element-plus --save
```

2. 起步配置
先参考官网起步

3. 添加自动导入插件
```cmd
npm install -D unplugin-vue-components unplugin-auto-import
```

4. 添加'unplugin-element-plus'这个包

```cmd
npm install unplugin-element-plus
```

```html
<-- App.vue -->
<template>
  <el-button>我是 ElButton</el-button>
</template>
<script>
  import { ElButton } from 'element-plus'
  export default {
    components: { ElButton },
  }
</script>
```


```js
vite.config.js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import AutoImport from 'unplugin-auto-import/vite';
import Components from 'unplugin-vue-components/vite';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';
import ElementPlus from 'unplugin-element-plus/vite';

export default defineConfig({
  plugins: [
    ElementPlus(),
    vue(),
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
  resolve: {
    alias: {
      '@': '/src' // 你的源代码路径
    }
  },
  css: {
    modules: {
      localsConvention: 'camelCase' // 如果你使用了CSS模块，可以添加这个配置
    }
  }
});
```

```json
jsconfig.json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "types": ["element-plus/global"],
  "exclude": ["node_modules", "dist"]
}
```


```js
main.js
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'
const app = createApp(App)
app.use(ElementPlus)
app.mount('#app')
```

# 使用Axios
1. 安装
`npm install axios`

2. 在当前vue组件导入
`import axios from 'axios';`

# 使用Vue Router4

### 引入依赖

```c
npm install vue-router@4
```


### 创建路由文件
在src下创建文件夹router,在文件夹下创建index.js文件
```js
import { createRouter,createWebHashHistory } from "vue-router";
//引入组件
import login from '../components/Login.vue';
import index from '../components/Index.vue';
//创建路由表
const routes = [
    {
        path: '/',
        component:login
    },
    {
        path: '/index',
        component:index
    }
]
//创建路由对象
const router = createRouter({
    history:createWebHashHistory(),
    //使用路由表
    routes
})
//向外暴露路由表
export default router;
```

### 配置使用路由

在mian.js文件中使用vue-router

```js
//引入vue_router
import router from './router';
//使用
app.use(router);
```


### 修改原来的app.vue文件
```html
<template>
<router-view></router-view>
</template>
<script>
export default {
  return() {},
  components:{
  }
};
</script>
```




# 打包vue项目

```c
npm run build
```


# 查看某端口

```c
netstat -ano | findstr :端口号
```



# MD5二次加密

## 前端安装MD5加密
```c
npm install md5
```

```c
let md5_passwd = md5(password);
```

## 后端调用spring核心包

#### 引入密钥
```c
@Value("${md5.secretKey}")  
private String salt;
```

```c
//后端加盐操作
String salt_pwd=user.getPassword()+salt;
// 最终的 MD5 密码
String final_md5pwd= DigestUtils.md5DigestAsHex(salt_pwd.getBytes());
```



# AXIOS配置基本路由以及携带令牌

```c
import { createApp } from 'vue';
import axios from 'axios';
import ElementPlus from 'element-plus';
import 'element-plus/dist/index.css';
import App from './App.vue';
import router from './router';

const app = createApp(App);
axios.defaults.baseURL = 'http://127.0.0.1:9999';
// 在请求发送前设置token
axios.interceptors.request.use(
  (config) => {
    const token = localStorage.getItem('token'); // 从localStorage中获取token
    if (token) {
      config.headers.Authorization = `Bearer ${token}`; // 将token放入请求头中
    }
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);
app.config.globalProperties.$axios = axios;
app.use(router);
app.use(ElementPlus);
app.mount('#app');
```






