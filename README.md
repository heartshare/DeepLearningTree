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

<pre>
张量
     从TensorFlow的名字就可以看出张量是一个很重要的概念，在TensorFlow程序中，所有的数据都是通过张量的形式来表示，从功能的角度上看，张量可以被简单理解为多维数组，第n阶张量就是n维数组。
     但是张量在TensorFlow中的实现并不是直接采用数组的形式，它只是对TensorFlow中运算结果的引用。在张量中并没有真正保存数字，它保存的是如何得到这些数字的计算过程。

         import tensorflow as tf
         
         a = tf.constant([1.0, 2.0], name = "a")
         b = tf.constant([2.0, 3.0], name = "b")
         result = tf.add(a, b, name = "add")
         print result

         输出:
             Tensor("add:0", shape=(2,), dtype = float32)
     一个张量中主要保存了三个属性：名字（name） 维度(shape)  类型（type）
     "add：0" 模式为"node:src_output"， 标识result这个张量时计算节点"add"输出的第一个结果
     "shape=(2,)"说明了张量result是一个一维数组，这个数组的长度为2，
     "type" 每个张量会有一个唯一的类型，TensorFlow会对参与运算的所有张量进行类型的检查，当发现类型不匹配时会报错。

     TensorFlow 支持14中不同的类型，主要包括了实数(tf.float32, tf.float64,)， 整数(tf.int8, tf.int16, tf.int32, tf.int64, tf.uint8)

     张量的使用
           和TensorFlow的计算模型相比，TensorFlow的数据模型相对比较简单，张量使用主要归结为两大类
                 1）对中间计算结果的引用。
                        当一个计算包括很多中间结果时，使用张量可以大大提高代码的可读性。
                 2）当计算图构造完成之后，张量可以用来获得计算结果，也就是得到真实的数字，虽然张量本身没有存储具体的数字，但是通过session就可以得到具体的数字。
</pre>

<pre>
TensorFlow运行模型------会话
      会话拥有管理TensorFlow程序运行时的所有资源，当所有计算完成之后需要关闭会话来帮助系统回收资源，否则就可能出现资源泄漏的问题，TensorFlow中使用会话的模式一般有两种：
             1）第一种模式需要明确调用会话生成函数和关闭会话函数
                     sess = tf.Session
                     sess.run(***)
                     sess.close()
             2) 通过Python的上下文管理器模式来使用会话
                     with tf.Session as sess
                          sess.run(***)
                不需要调用sess.close，当上下文退出时，会话关闭和资源释放也自动完成了

      TensorFlow会自动生成一个默认的计算图，如果没有特殊指定，运算会自动加入这个计算图中，TensorFlow中的会话也有类似的机制，但是TensorFlow不会自动生成默认是的会话，而是需要手动指定，当默认的会话被指定之后可以通过tf.Tensor.eval函数来计算一个张量的取值。
             sess = tf.Session()
             with sess.as_default():
                  print(result.eval())
             在交互式环境下
                  sess = tf.InteractiveSession()
                  print(result.eval())
                  sess.close()
       无论使用哪种方法都可以通过ConfigProto Protocol Buffer来配置需要生成的会话，
                  config = tf.ConfigProto(allow_soft_placement=True,
                                          log_device_placement=True)
                  sess1 = tf.InteractiveSession(config=config)
                  sess2 = tf.Session(config = config)

                  通过ConfigProto可以配置类似并行的线程数，GPU分配策略，运算超时时间等参数。
                      allow_soft_placement 
                          为True，在以下任意一个条件成立时，GPU上的运算可以放到CPU上执行
                              1）运算无法在GPU上执行
                              2）没有GPU资源（比如运算被指定在第二个GPU，而机器实际只有一个GPU）
                              3）运算输入包括对CPU计算结果的引用
                      
                      log_device_placement
                          这也是一个布尔型的参数，当它为True时日志中将会记录每个节点被安排在了哪个设备上以方便调式，而在生产环境中可以将这个参数置为False可以减少日志。
</pre>