# 每日一句
Ideal is the beacon. Without ideal, there is no secure direction; without direction, there is no life. 
理想是指路明灯。没有理想，就没有坚定的方向;没有方向，就没有生活。

# 概述

对集合进行分片时,你需要选择一个 片键（Shard Key） , shard key 是每条记录都必须包含的,且建立了索引的单个字段或复合字段,MongoDB按照片键将数据划分到不同的 数据块 中,并将 数据块 均衡地分布到所有分片中.

为了按照片键划分数据块,MongoDB使用如下方式分配：

-  基于哈希的分片方式（随机平均分配）
- 基于范围的分片方式（数值大小分配）

用什么字段当片键都可以，如：nickname作为片键，但一定是必填字段。



# 哈希策略

对于 基于哈希的分片 ,MongoDB计算一个字段的哈希值,并用这个哈希值来创建数据块.

在使用基于哈希分片的系统中,拥有”相近”片键的文档 很可能不会 存储在同一个数据块中,因此数据的分离性更好一些.

使用nickname作为片键，根据其值的哈希值进行数据分片



```
sh.shardCollection("articledb.comment",{"nickname":"hashed"})
```



# 范围策略

对于 基于范围的分片 ,MongoDB按照片键的范围把数据分成不同部分.

假设有一个数字的片键:想象一个从负无穷到正无穷的直线,每一个片键的值都在直线上画了一个点.MongoDB把这条直线划分为更短的不重叠的片段,并称之为 数据块 ,每个数据块包含了片键在一定范围内的数据.

在使用片键做范围划分的系统中,拥有”相近”片键的文档很可能存储在同一个数据块中,因此也会存储在同一个分片中.

如使用作者年龄字段作为片键，按照点赞数的值进行分片：

```
sh.shardCollection("articledb.author",{"age":1})
```

**注意**

1）一个集合只能指定一个片键，否则报错。

2）一旦对一个集合分片，分片键和分片值就不可改变。 如：不能给集合选择不同的分片键、不能更新分片键的值。

3）根据age索引进行分配数据。



# 两种策略对比

基于范围的分片方式提供了更高效的范围查询,给定一个片键的范围,分发路由可以很简单地确定哪个数据块存储了请求需要的数据,并将请求转发到相应的分片中.不过,基于范围的分片会导致数据在不同分片上的不均衡,有时候,带来的消极作用会大于查询性能的积极作用.比如,如果片键所在的字段是线性增长的,一定时间内的所有请求都会落到某个固定的数据块中,最终导致分布在同一个分片中.在这种情况下,一小部分分片承载了集群大部分的数据,系统并不能很好地进行扩展.



基于哈希的分片方式以范围查询性能的损失为代价,保证了集群中数据的均衡.哈希值的随机性，使数据随机分布在每个数据块中,因此也随机分布在不同分片中.但是也正由于随机性,一个范围查询很难确定应该请求哪些分片,通常为了返回需要的结果,需要请求所有分片.



如无特殊情况，一般推荐使用 Hash Sharding。而使用 _id 作为片键是一个不错的选择，因为它是必有的，你可以使用数据文档 _id 的哈希作为片键。

这个方案能够是的读和写都能够平均分布，并且它能够保证每个文档都有不同的片键所以数据块能够很精细。似乎还是不够完美，因为这样的话对多个文档的查询必将命中所有的分片。虽说如此，这也是一种比较好的方案了。




# 美文佳句

一个人的自愈能力越强，才越有可能接近幸福。做一个寡言，却心有一片海的人，不伤人害己，于淡泊中，平和自在。