# 远程调用接口返回结果的通用设计 #

## 接口返回结果 ##

- successful：操作是否成功，boolean类型，true表示成功，false表示失败
- errorCode：错误码，字符串类型。当successful=false的时候才有值
- errorMessage：错误信息，字符串类型。当successful=false的时候才有值
- retryable：是否可以重试，boolean类型。true表示可以重试，如系统发生未知异常；false表示重试也没有效果，如输入参数不合法

retryable不一定需要，主要是给那些后台任务形式（如消息处理、定时任务等）的调用方使用，用户的直接请求如一次web访问，一般不需要系统自动重试或者最多重试一俩次，用户自己可以重试。


## 客户端调用方式 ##

```java
if (result.isSuccessful()) {
	// 处理操作成功的情况
} else {
	if (result.isRetryable()) {
		// 重试或者间隔一段时间重试，一般不能无限次重试，有一定的重试规则，如最多重试多少次，每次重试的间隔是上次重试间隔的2倍等
	} else {
		// 处理操作失败的情况，如打印出errorCode和errorMessage。或者根据errorCode做不同的处理
	}
}
```

## 错误码的设计 ##

请参考[错误码的设计](error_code)