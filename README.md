# novelDoc
小说文档

### 一、图书详情
![](imgs/book_detial1.png)


```lua

接口1：
{
	详情{
	  	书名，
	   	作者，
	  	封面图，
	   	字数，
	  	二级分类名，
		三级分类名，
		出版状态(如：已完结),
		评论数，
		章节数，
		简介,
		点赞星级(所有玩家评价取均值，1-10的整数，10就是5颗星，9就是4颗半)，
	}，
	

}

接口2:
评论列表
(
	{
		用户名，
		用户头像，
		评论时间，
		评论内容，
		点赞星级(该玩家的评价，1-10的整数,10就是5颗星，不需要平均值)，
	}
	...
)，



接口3：
相关图书推荐(因为有换一换功能，所以需要可以随机返回，每次调用,
推荐的书籍都不一样，一次推荐四本)
推荐图书是可以跳转推荐的图书详情的，可能得要返回bookid
（
	{
		封面，
		书名,
		作者,
	},
	...
）

接口4：
加入书架
参数:{
	uid,
	bookid/音频专辑id,
}
返回值{
	code（状态码）
}



接口5：
从书架删除
参数:{
	uid,
	bookid/音频专辑id,
}
返回值{
	code（状态码）
}


```

### 二、评论
![](imgs/comment_publish1.png)

```lua
接口1：评论
参数:{
	点赞星级(int 类型，1-5，5颗星),
	评论内容(字符串),
	bookid,
}
返回值{
	code（状态码）
}
```

### 三、音频专辑详情
![](imgs/audio_detial1.png)

```lua

接口1：专辑详情
{
 	专辑名称，
	主播，
	三级分类名称，
	更新时间，
	详情（类似介绍的字符串），
	节目总数,(考虑从首页推荐等其它入口，拿不到节目数，所以在这个接口加)

}


接口2:节目
(
	{
	节目名称，
	时长，
	评论数，
	发布时间，
	简介,
	文件大小，
	},
	…
)


接口3:相似(音频详情的相关推荐也用这一个接口，是否已收藏的字段不要了)
(
	{
	节目名称，
	节目描述，
	总共集数，

	},
	…
)

```

### 四、音频节目详情
![](imgs/auido_item1.png)

```lua


接口1：音频下载接口

接口2：评论列表

(
	{
		用户名，
		用户头像，
		评论用户uid
		评论时间，
		评论内容，
		回复数，点赞数（回复和点赞丁总说先不做）
	}
	...
)，

接口3：评论
参数:{
	评论内容(字符串),

}
返回值{
	code（状态码）
}

```

### 五、登录
![](imgs/login1.png)

```lua
接口1：登录接口
参数{
	手机号，
	密码
}
返回值{
	code,(状态码,0成功，1还未注册,2密码错误,3其它原因导致失败)

	头像，
	手机，
	昵称，
	性别，
	省份，
	uid,
}

接口2：注册
参数{
	手机号，
	密码，
}
返回值{
	code(状态码,0成功，1已注册，2其它原因导致失败)
}

接口3：找回密码
参数{
	手机号，
	新密码，
	验证码，
}
返回值{
	code(状态码,0成功，1验证码错误,2还未注册，3其它原因导致失败)
}

接口4：获取验证码（验证码通过短信发送至手机）
参数{
	手机号，
	type,(int型，1注册，2找回密码)
}
返回值{
	code,(状态码,0成功，1已注册(type为1的情况才会出现),2还未注册(type为2的情况才会出现),3其它原因导致失败)
	验证码，
}

```

### 六、书架
![](imgs/shelf1.png)

```lua
接口1：书架列表
参数{
	uid
}
返回值{
	书架列表：（
		书籍：{
			封面，
			书名，
			是audio还是书本（需要根据某个字段进行区分），
			bookid（跳转书籍详情和音频专辑的必要字段）
		}
	…
	）
}
```

### 七、我的评论
![](imgs/my_comment.jpeg)

```lua
接口1：我的评论列表
参数{
	uid
}
返回值{
	评论列表：（
		{
			bookId，（跳详情),
			书籍名称(专辑名称),
			专辑简介(音频简介),
			用户名，
			用户头像，
			用户uid
			评论时间，
			评论内容，
		}
	…
	）
}
```

