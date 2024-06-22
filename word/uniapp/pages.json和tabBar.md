## pages.json

用于配置页面的路由、导航栏、tabBar页面信息

## 导航栏

``` json
import {memberStore} from '@/stores/member.js'
// 添加拦截器
const baseURL = "http://pcapi-xiaotuxian-front-devtest.itheima.net"
const httpInterceptors = {
	 invoke(option) {
		// 非 http开头请求需要拼接地址,排除个例请求其他接口的情况
	  if (!option.url.startsWith('http')) {  
		option.url = baseURL + option.url;  
	  }  
		// 请求超时
		option.timeout = 10000
		// 添加请求头标识
		option.header = {
			// 展开原本的请求头标识，在请求的时候如果赋值会覆盖原本的请求头
			...option.header,
			'source-client': 'miniapp'
		}
		// 添加token
		const  member = memberStore()
		// 从pinia中获取token
		const token = member.member.token
		// 如果有token
		if(token) {
			// 请求头中添加token
			option.header.Authorization = token
		}
		console.log(option)
	}
}
// 添加请求拦截器
uni.addInterceptor('request', httpInterceptors)
// 添加上传文件拦截器
uni.addInterceptor('uploadFile', httpInterceptors)
// 请求函数
export const http = (options)=>{
	// resolve获取成功，reject获取失败
	return new Promise((resolve, reject)=>{
		uni.request({
			...options,
			success(res){
				// 状态码200请求成功返回数据
				if(res.statusCode >= 200 && res.statusCode < 300){
					resolve(res.data)
				} else if (res.statusCode == 401){ // 401登录超时
					const  member = memberStore()
					member.RemoveMember() // 清除本地数据
					uni.navigateTo({ // 跳转页面，必须未非tabBar页面
						url:'/pages/login/login'
					})
					reject(res.data)
				}else{ // 其他错误
					uni.showToast({ // 轻提示
						icon:'none',
						title:res.data.msg || "error"
					})
				}
			},
			// 响应失败
			fail(err) {
				uni.showToast({ // 轻提示
					icon:'error',
					title:res.data.msg || "网络错误"
				})
				reject(err)
			}
		})
	})
}
```

