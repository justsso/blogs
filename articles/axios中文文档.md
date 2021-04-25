---
2020.3.18
---

axios中文文档
什么是axios?
Axios是一个基于promise的HTTP库，可以用在浏览器和node.js中。

特性
从浏览器中创建XMLHttpRequests
从node.js创建http请求
支持Promise API
拦截请求和响应
转换请求数据和响应数据
取消请求
自动转换JSON 数据
客户端支持防御XSRF
axios API
axios(config)
axios(url[,config])
请求方法的别名
axios.request(config)
axios.get(url[,config])
axios.delete(url[, config])
axios.head(url[, config])
axios.options(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.patch(url[, data[, config]])
注意
在使用别名方法时， url、method、data 这些属性都不必在配置中指定。

并发
处理并发请求的助手函数

axios.all(iterable)
axios.spread(callback)
创建实例
可以使用自定义配置新建一个axios实例。

使用 axios.create([config]) 方法创建

Javascript
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
实例方法

以下是可用的实例方法。指定的配置将与实例的配置合并。

axios#request(config)
axios#get(url[, config])
axios#delete(url[, config])
axios#head(url[, config])
axios#options(url[, config])
axios#post(url[, data[, config]])
axios#put(url[, data[, config]])
axios#patch(url[, data[, config]])
请求配置
这些是创建请求时可以用的配置选项。只有url是必须的。如果没有指定method,请求将默认使用get方法。

Javascript
{
    // 'url'是用于请求的服务器URL
    url: '/user',
    //method 是创建请求时的使用的方法
    method: 'get',
    // baseURL 将自动加在url前面，除非url是一个绝对URL
    baseURL: 'https://some-domain.com/api/',
    // transformRequest 允许向服务器发送前，修改请求数据
    //只能用在PUT POST 和PATCH 这几个请求方法
    // 后面数组中的函数必须返回一个字符串，或ArrayBuffer或Stream
    transformRequest: [function (data, headers) {
        //对data 进行任意转换处理
        return data;
    }],
    transformResponse: [function(data) {
        //对data 进行任意转换处理
        return data;
    }],
    //headers 是即将被发送的自定义请求头
    headers: {'X-Requested-With': 'XMLHttpRequest'},
    //params 是即将与请求一起发送的URL参数
    //必须是一个无格式对象(plain object)或 URLSearchParams 对象
    params: {
     ID : 213
    },
// `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: 'Fred'
  },
// `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

   // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

 // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // **这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头**
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

   // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default

  // `responseEncoding` indicates encoding to use for decoding responses
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // default

   // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default

   // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

   // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // default

  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
插曲：
我们在做jwt验证时，通常会在request的header中添加一个token，是这样写的:

Javascript
const token = window.sessionStorage.getItem("token");
if (token) {
    config.headers.Authorization = `Bearer ${token}`;
}
那么这个token的认证和上文配置中的auth有什么关联呢？

原来auth 是进行的http用户验证，token是进行的我们自己系统的认证，是两码事。

auth 认证后的header信息一般是这样的：
Authorization: Basic dWVub3NlbjpwYXNzd29yZA==
首部字段 Authorization 是用来告知服务器，用户代理的认证信息（证 书值）。通常，想要通过服务器认证的用户代理会在接收到返回的 401 状态码响应后，
把首部字段 Authorization 加入请求中。共用缓存 在接收到含有 Authorization 首部字段的请求时的操作处理会略有差 异
认证方案是Basic,auth用的比较少。

配置默认值
你可以指定将被用在各个请求的配置默认值

全局的axios默认值
Javascript
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = Auth_TOKEN;
axios.defaults.head.post['Content-Type'] 'application/x-wwww-form-url';
自定义实例默认值
有两种方式

Javascript

//1.当你创建实例的时候，就在配置config中写明
const instance = axios.create({
    baseURL: 'https://api.example.com'
})

//2. 在创建实例之后，再去修改
instance.defaults.headers.common['Authrization'] = AUTH_TOKEN;
配置的优先顺序
请求配置 > 实例配置 > 默认配置

拦截器
在请求或响应被then或catch处理前拦截它们。

Javascript
// 添加请求拦截器

axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
}, function (error){
    //对请求错误做些什么
    return Promise.reeject(error)
})



// 添加响应拦截器
axios.interceptors.response.use(function (response){
    // 对响应数据做点什么
    return response;
}, function (error){
    //对响应错误做点什么
    return Promise.reject(error)
})
如果你想在稍后移除拦截器，可以这样：

Javascript

const myInterceptor = axios.interceptors.request.use(function () {/**/})
axios.interceptors.request.eject(myInterceptor);
可以为自定义axios实例添加拦截器

Javascript
const instance = axios.create();
instance.interceptors.request.use(function(){/**/})
错误处理
Javascript
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // The request was made and the server responded with a status code
      // that falls out of the range of 2xx
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // The request was made but no response was received
      // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
      // http.ClientRequest in node.js
      console.log(error.request);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
可以使用validateStatus配置选项定义一个自定义HTTP状态码的错误范围。

Javascript
axios.get('/user/12345', {
    validateStatus: function (status) {
        return status < 500   
    }
})
取消
使用cancel token取消请求

Axios的cancel token API基于cancelable promises proposal,它还
处于第一阶段。

可以使用CancelToken.source工厂方法创建cancel token，像这样：

Javascript
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('/user/12345', {
    cancelToken: source.token
}).catch(function(){
    if(axios.isCancel(thrown)) {
        console.log('Request cancled', thrown.message);
    }else{
    //处理错误
    }
})

axios.post('/user/12345', {
  name: 'new name'
}, {
  cancelToken: source.token
})

// 取消请求（message 参数是可选的）
source.cancel('Operation canceled by the user.');
还可以通过传递一个 executor 函数到 CancelToken 的构造函数来创建 cancel token：

Javascript

const CancelToken = axios.CancelToken;
let cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
});

// cancel the request
cancel();
注意: 可以使用同一个 cancel token 取消多个请求

使用 application/x-www-form-urlencoded format
默认情况下，axios将JavaScript对象序列化为JSON。 要以application / x-www-form-urlencoded格式发送数据，您可以使用以下选项之一。
在浏览器和Node.js中要有不同的处理方法

浏览器
在浏览器中，您可以使用URLSearchParams API，如下所示：

Javascript
const params = new URLSearchParams();

params.append('param1','value1');
params.append('param2','value2');

axios.post('/foo', params);
请注意，所有浏览器都不支持URLSearchParams（请参阅 caniuse.com）
polyfill(确保填充全局环境)

或者，您可以使用qs库编码数据：

Javascript
const qs = require('qs');
axios.post('/foo', qs.stringify({'bar': 123}));
或者以另一种方式（ES6），

Javascript

import qs from 'qs';
const data = { 'bar': 123 };
const options = {
  method: 'POST',
  headers: { 'content-type': 'application/x-www-form-urlencoded' },
  data: qs.stringify(data),
  url,
};
axios(options);
Node.js
在node.js中，您可以使用querystring模块，如下所示：

Javascript
const querystring = require('querystring');
axios.post('http://something.com/', querystring.stringify({ foo: 'bar' }));
您也可以使用qs库。

Pomises
axios依赖原生的ES6 Promise 实现而被支持，如果你的环境不支持ES6 Promise
可以使用polyfill

TypeScript
axios包括TypeScript定义。

Javascript
import axios from 'axios';
axios.get('/user?ID=12345')
赞扬
axios 深受Angular提供的 $http服务的启发。最终，axios是为了在Angular之外使用而提供独立的类似$http服务的。

协议
MIT