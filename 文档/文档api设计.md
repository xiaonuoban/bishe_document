## 1-全局注意事项

- 1-json格式的统一格式，统一最外层放状态码，0为错误，1为正常


```
{
    "status": "xxx",
    "data":{
        "xxx":"xxx"
    }
}
```

- 为了方便表示，在这里表示的数据类型都是字符串的形式，实际接口json字符串的有些数据并不全是字符串
- 所有接口都以/api开头

## 2-首页的api接口和格式

### 2-1-轮播图

- 轮播图接口为`/api/index/sliders` **-----get**

- 返回的json格式

```
{
    "status": "xxx",
    "data":[
        {
            "r_pd_id": "xxx",
            "r_pd_type": "xxx",
            "r_pd_img": "xxx"
        },
        {
            ...一共有五个轮播图的数据
        }
    ]
}
```



### 2-2-菜单格式

- 菜单接口为`/api/index/menus`**-----get**

- 返回的json格式

```
{
    "status": "xxx",
    "data":[
        {
            "r_pd_id": "xxx",
            "r_pd_type": "xxx",
            "r_pd_title": "xxx",
            "r_pd_content": "xxx",
            "r_pd_user_name": "xxx"，
        },
        {
            ...一共有18个菜单的数据
        }
    ]
}
```



###  2-3-首页分类里的新秀菜谱和一周热门

- 新秀菜谱接口为`/api/index/xxcp?page=xxx`**-----get**

- 返回的json格式（每页返回20条数据）

```
{
    "status": "xxx",
    "data":{
    	"page": "xxx",
    	"type": "xxx",
        "recipes":[
            {
            "r_i_id": "xxx",
            "r_i_type": "xxx",
            "r_i_show_title": "xxx",
            "r_i_u_id": "xxx",
            "r_i_shoe_user_name": "xxx",
            "r_i_avatar": "xxx",
            "r_i_show_img": "xxx"
        	},
        	...
        ]
}
```

- 一周热门接口为`/api/index/yzrm?page=xxx`**-----get**

- 返回的json格式（每页返回20条数据）

```
{
    "status": "xxx",
    "data":{
        "page": "xxx",
        "type": "xxx",
        "recipes":{
            {
            "r_i_id": "xxx",
            "r_i_type": "xxx",
            "r_i_show_title": "xxx",
            "r_i_u_id": "xxx",
            "r_i_shoe_user_name": "xxx",
            "r_i_avatar": "xxx",
            "r_i_show_img": "xxx"
        	},
        	...
        }
    }
    }
}
```

采用分页的形式可以让前端加入上拉加载更多的功能



## 3- 轮播图的api

- 接口`/api/sliders?r_pd_id=xxx`**-----get**

- 通过r_pd_id去取菜单页面中的数据
- json数据如下

```
{
    "status": "xxx",
    "data": {
        "r_pd_id": "xxx",
        "r_pd_type": "xxx",
        "r_pd_img": "xxx",
        "r_pd_desc": "xxx",
        "list": [
            #  放分标题,比如五个，每个标题下还有详细的食谱
            {"title": "xxx",   
             "content": "xxx", 
             "recipes": [
                    # 可能二十几个
                    {"r_i_id": "xxx",
                     "r_i_type": "xxx",
                     "r_i_r_id": "xxx",
                     "r_i_show_title": "xxx",
                     "r_i_u_id": "xxx",
                     "r_i_show_username": "xxx",
                     "r_i_avatar": "xxx",
                     "r_i_show_img": "xxx"
                     }
                     ...
             ]}
             ...
        ]
    }
}
```



## 4-菜单的api

- 接口`/api/menus?r_pd_id=xxx`**-----get**
- 通过r_pd_id去取轮播图页面中的数据
- json数据如下

```
{
    "status": "xxx",
    "data": {
        "r_pd_id": "xxx",
        "r_pd_type": "xxx",
        "r_pd_menu_data": {},
        "recipes": [
                # 可能二十几个
                {"r_i_id": "xxx",
                "r_i_type": "xxx",
                "r_i_r_id": "xxx",
                "r_i_show_title": "xxx",
                "r_i_u_id": "xxx",
                "r_i_show_username": "xxx",
                "r_i_avatar": "xxx",
                "r_i_show_img": "xxx",
                "r_i_materials": "xxx"
                }
                ...
        ]
    }
}
```



## 5-全部分类的api

### 5-1-获取分类的标题

- 接口`/api/type/getType`**-----get**
- json数据如下

```
{
    "status": "xxx",
    "data":{
    	"type": [
            {"name": "最新推荐"，"code": "1"},
        	{"name": "最新发布"，"code": "2"},
        	...
    	]
    }
}
```



### 5-2-获取分类标题下第n页的数据

- 接口`/api/type/getData?code=xxx&page=xxx`**----get**

- json数据如下（每页返回20条数据）

```
{
    "status": "xxx",
    "data":{
    	"type": "xxx",
    	"page": "xxx",
    	"recipes": [
            {    	
                "r_a_id": "xxx",
                "r_a_type": "xxx",
                "r_a_r_id": "xxx",
                "r_a_show_title": "xxx",
                "r_a_u_id": "xxx",
                "r_a_show_user_name": "xxx",
                "r_a_avatar": "xxx",
                "r_a_show_img": "xxx",
            },
        	...
    	]
    }
}
```



## 6-详细食谱

- 接口`/api/recipes?r_id=xxx`

- json数据如下

```
{
    "status": "xxx",
    "data":{
    	"r_id": "xxx",
    	"r_title": "xxx",
    	"r_u_id": "xxx",
    	"r_user_name": "xxx",
    	"r_avatar": "xxx",
    	"r_show_photo": ["xxx"],  //可能有多张
    	"r_desc": "xxx",
    	"r_materials": {
            "main": [
            	{"name": "xxx", "gram": "xxx"},
            	{"name": "xxx", "gram": "xxx"},
            	...
        	],
        	"subsidiary": [
        		{"name": "xxx", "gram": "xxx"},
        		...
        	],
        	"category": [
            	{"name": "xxx", "desc": "xxx"},
            	{"name": "xxx", "desc": "xxx"},
            	...
        	],
    	},
    	"r_step": [
           	{"content": "xxx", "step_img": "xxx"}, 
           	{"content": "xxx", "step_img": "xxx"},
        	...
    	]
    }
}
```



## 7-登录

- 待定



## 8-注册

-  待定



## 9-获取个人信息

- 接口`/api/user/getUserInfo?u_id=xxx`

- json数据

```
{
    "status": "xxx",
    "data":{
    	"u_id": "xxx",
    	"u_user_name": "xxx",
    	"u_avatar": "xxx",
    	"u_gender": "xxx",
    	"u_individual_desc": "xxx",
    	"u_area": "xxx",
    	"recipes": [
    		##发过的菜谱
            {    	
                "r_id": "xxx",
                "r_title": "xxx",
                "r_user_name": "xxx",
                "r_show_photo": "xxx"
            },
        	...
    	]
    }
}
```





## 10-发帖子

- 待定



## 11-评论

- 获取评论信息接口`/api/comments/getCommentsData?r_id=xxx`
- json数据如下

```
{
    "status": "xxx",
    "data":{
    	"comments": [
            {   
            	"c_id": "xxx",
    			"c_r_id": "xxx",
                "c_u_id": "xxx",
                "c_u_user_name": "xxx",
                "c_content": "xxx",
                "comments":[
                    #二级评论信息，可能有，可能无
                    {
                        "rp_id": "xxx",
                        "rp_c_id": "xxx",
                        "rp_type": "xxx",
                        "rp_content": "xxx",
                        "rp_u_id": "xxx",
                        "rp_u_user_name": "xxx",
                    	"rp_u_id_ed": "xxx",
                    	"rp_u_user_name_ed": "xxx",
                    }
                    ...
                ]
            },
        	...
    	]
    }
}
```

