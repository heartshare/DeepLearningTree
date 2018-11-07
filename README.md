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

<pre>
Bazel
     Bazel是谷歌开源的自动化构建工具，谷歌内部大部分的应用都是通过它来编译的，相比传统的Makefile, Ant， Maven,  Bazel在速度，可伸缩性，灵活性以及对不同程序语言和平台的支持上都要更加出色，
</pre>

<pre>
TensorFlow计算模型-----计算图
     计算图是TensorFlow中最基本的概念，TensorFlow中的所有计算都会转化为计算图上的节点。

     TensorFlow的名字中已经说明了它最重要的两个概念------Tensor和Flow。
     Tensor就是张量，张量这个概念在数学或者物理学中可以有不同的解释，在TensorFlow中，张量可以被简单的理解为多维数组，
     Flow翻译成中文就是流，它直观的表达了张量之间通过计算相互转化的过程，TensorFlow是一个通过计算图的形式来表述计算的编程系统，
</pre>

<pre>
计算图的使用
     TensorFlow程序一般可以分为两个阶段。
           第一阶段：
                  定义计算图中所有的计算
           第二阶段：
                  执行结算

     TensorFlow中的计算图不仅仅可以用来隔离张量和计算，它还提供了管理张量和计算的机制，计算图可以通过tf.Graph.device函数来指定运行计算的设备，这为TensorFlow使用GPU提供了机制。
           g = tf.Graph()
           with g.device('/gpu:0'):
                result = a + b
     有效的整理TensorFlow程序中的计算资源也是计算图的一个重要功能。可以通过集合来管理不同类型的资源，比如通过 tf.add_to_collection函数将资源加入一个或者多个集合中，然后通过
     tf.get_collection获取一个集合里边的所有资源。
</pre>
