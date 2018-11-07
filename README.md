# DeepLearningTree
深度学习技术

<pre>
   深度学习最早兴起于图像识别，但是在短短几年时间内，深度学习推广到了机器学习的各个领域，
   如今，深度学习在很多机器学习领域都有着非常出色的表现，在图像识别，语音识别，音频处理，
   自然语言处理，机器人，生物信息处理，化学，电脑游戏，搜索引擎，网络广告投放，医学自动
   诊断，金融等各大领域均有应用。
</pre>

<pre>
Protocol Buffer
     Protocol Buffer是谷歌开发的处理结构化数据的工具
     所谓序列化：是将结构化的数据变成数据流的形式，简单地说就是变成一个字符串。如何将结构化的数据序列化，并从序列化之后的数据流中还原出原来的结构化数据，统称为 处理为处理结构化数据，这就是Protocol Buffer要解决的问题
     除了Protocol Buffer之外，XML, JSON是两种比较常用的结构化数据处理工具。

     Protocol Buffer格式的数据和XML或者JSON格式的数据有比较大的去呗，首先，Protocol Buffer序列化之后得到的数据不是可读的字符串，而是二进制流。其次，XML或者JSON格式的数据信息都包含在了序列化之后的数据中，不需要任何其他信息就能还原序列之后的数据。但使用Protocol Buffer时需要先定义数据的格式（schema），还原一个序列化之后的数据将需要使用到这个定义好的数据格式。
     因为这些差别，Protocol Buffer序列化出来的数据要比XML格式的数据小3到10倍，解析的时间要快20-100倍。

     Protocol Buffer是TensorFlow系统中使用到的重要工具，TensorFlow中的数据基本上是通过Protocol Buffer来组织的，分布式TensorFlow的通信协议gRPC也是以Protocol Buffer作为基础的。
</pre>
