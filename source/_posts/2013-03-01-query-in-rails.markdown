---
layout: post
title: "rails 查询"
date: 2013-03-01 15:01
comments: true
categories: rails ruby 
---

资料
--

[guide](http://guides.rubyonrails.org/active_record_querying.html)

[rails casts](http://cn.asciicasts.com/episodes/202-active-record-queries-in-rails-3)

[高级查询](http://cn.asciicasts.com/episodes/215-advanced-queries-in-rails-3)
<!-- more -->
常用的查询
-----

* 查询一组数据

``` ruby 
    User.where("id in (?)", [1, 2, 3])
    User.where("id in (?) and status = ?", [1, 2, 3], 0)
    # range 的写法
    Client.where(:created_at => (Time.now.midnight - 1.day)..Time.now.midnight)
```

* 查询特定的列

``` ruby
    User.select("gender, location")
    User.select(:gender)
```
 
* 排序

``` ruby
    User.oder("created_at ASC")
    User.oder("created_at DESC")
    # 模糊查询, 比如 北京 昌平，而当只有北京时也希望满足，就用下面的方法
    ->(location) where("location like ?", "%#{location}%")
```

* 连表查询 joins

``` ruby

    # 下面是各个model的关系(来源:官方guides)
    class Category < ActiveRecord::Base
      has_many :posts
    end
     
    class Post < ActiveRecord::Base
      belongs_to :category
      has_many :comments
      has_many :tags
    end
     
    class Comment < ActiveRecord::Base
      belongs_to :post
      has_one :guest
    end
     
    class Guest < ActiveRecord::Base
      belongs_to :comment
    end
     
    class Tag < ActiveRecord::Base
      belongs_to :post
    end
    
    # 用法(多级联查)
    Category.joins(:posts => [{:comments => :guest}, :tags])

    # 解释
    SELECT categories.* FROM categories
    INNER JOIN posts ON posts.category_id = categories.id
    INNER JOIN comments ON comments.post_id = posts.id
    INNER JOIN guests ON guests.comment_id = comments.id
    INNER JOIN tags ON tags.post_id = posts.id
    
```

`inner join` 同时要求两个表都满足， 即左边和右边同时有数据才行

`left join`  只要左边的表有数据就满足

`right join` 只要右边的表有数据就满足

`full join`  只要有一个表有数据就满足

* 贪婪加载 includes

``` ruby
    # 这个加载的过程，会将10条有关address的数据同时加载，而不是只加载clients
    clients = Client.includes(:address).limit(10)

    # 要清楚一点是，includes 的加载方式是 left join 
    Post.includes(:category, :comments)
    
```

* joins 和 includes 的选择

joins 使用的是`inner join`, includes 使用的是`left join`

joins只会把主表的数据查询出来放在内存，如果需要查询连接表的数据，还必须再次查询数据库， includes会把一起连接表的所有字段都查询出来，放到内存里面.

* scope

``` ruby
    # 不带参数的写法scope
    scope :published, where(:published => true)
    
    # -> 是lambda的简写，这种写法是带参数的写法
    scope :get_status, ->(status) { where("status in(?)", status) }

    # scope 可以联合使用
    Article.published.get_status([0, 1])
```

* 取数据库中的一列

``` ruby
    # pluck    
    User.where("gender = ?", 0).pluck(:name)

    # collect
    User.where("gender = ?", 0).collect(&:name)
```
二者取出的结果是一样的，都是取`gender = 0` 的用户的名字

