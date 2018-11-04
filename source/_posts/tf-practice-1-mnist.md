---
title: 'TensorFlow练习一:mnist数字识别'
tags:
  - TensorFlow
date: 2018-11-04 12:22:13
thumbnail: img/mikoto.jpg
---

# tensorflow官方示例
```python
import tensorflow as tf
mnist = tf.keras.datasets.mnist

(x_train, y_train),(x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(),
  tf.keras.layers.Dense(512, activation=tf.nn.relu),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

model.fit(x_train, y_train, epochs=5)
model.evaluate(x_test, y_test)
```
运行结果:
![](/img/tf1-20181104124539.png )

分分钟跑到98%的准确率

完毕！！！

好吧，实际应用不会那么简单，所以下面主要实现用到大多数的步骤
> 1、用Eager模式搭建原型</br>
> 2、**用Datasets处理数据**</br>
> 3、用Feature Columns提取特征</br>
> 4、**用Keras搭建模型**</br>
> 5、借用Canned Estimators</br>
> 6、用SavedModel打包模型</br>
> 来自[《Google开发者大会：你不得不知的Tensorflow小技巧》](https://juejin.im/post/5baae0afe51d450e6c74d0d5)

# DataSet数据预处理
```python
# 数据集
def getDataset(x, y, batch_size=32):
    # 数据转换，将x归一化，y变为one_hot向量
    def _parse_data(x, y):
        return tf.div(tf.cast(x, tf.float32), 255.0), tf.one_hot(y, 10)

    dataset = tf.data.Dataset.from_tensor_slices((x, y))
    # 数据集
    dataset = dataset.shuffle(60000)
                     .map(_parse_data)
                     .prefetch(batch_size * 10)
                     .batch(batch_size)
                     .repeat(100000)
    return dataset
```
**from_tensor_slices**： 初始化dataset，dataset会有多次数据复制，所以如果输入是图片的数组，可能会直接导致能存不够，所以此处的输入最好是图片地址这类不大的输入，具体图片处理由内部处理
> [官网API](https://www.tensorflow.org/api_docs/python/tf/data/Dataset#from_tensor_slices)

**shuffle**：洗牌，将数据随机组合

**map**：使用_parse_data函数逐条处理数据，一般情况下用户输入可以是一组图片地址，处理函数就可以加载图片，然后转化成需要的数据形式

**prefetch**：预加载，主要设置预加载的数据量

**batch**：批数据量

**repeat**：数据集重复次数

使用dataset的顺序很重要，map要在shuffle之后，因为map处理后的数据将会变成很大的图片数据，如果shuffle的buffer_size大一些，就会导致内存不够（实际上buffer_size最好和数据集大小相同），如果在map之前处理，shuffle的实际是图片地址，相对来数内存可能没法处理10W图片，但10W地址字符串轻轻松松，这段主要是下面的神级回答的一个简单理解：
> [Olivier Moindrot](https://stackoverflow.com/users/5098368/olivier-moindrot)的[回答](https://stackoverflow.com/questions/46444018/meaning-of-buffer-size-in-dataset-map-dataset-prefetch-and-dataset-shuffle)

# Keras搭建模型
```python
#定义网络结构
model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(input_shape=(28, 28)),
    tf.keras.layers.Dense(512, activation=tf.nn.relu),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])
#
model.compile(optimizer="Adam",
              loss="categorical_crossentropy",
              metrics=["accuracy"])
```
keras接口确实方便所以这边也没有太多要说的，主要要提的一点是要在第一层指定input_shape，由于TensorFlow官网示例第一层直接是Flatten()，导致我在修改使用dataset的时候一直出问题，后来发现是input_shape没指定。如果想下原理其实也很简单，y=wx+b的w和x两个矩阵相乘形状必须满足[a,b]矩阵乘[b,c]得到[a,c]形状，参数数要匹配，所以必须是已知x的形状的，如果是卷积神经网络，在全连接层之前倒是可以不知道数据的形状

# 模型保存
```python
# 常用callback
def getCallBacks():
    # tensorbord日志
    tensorboard = TensorBoard(log_dir="./logs")
    # 保存最佳的模型
    checkpoint = ModelCheckpoint(filepath="./mnist.h5", save_best_only=True, monitor="loss")
    # 当学习停滞时，自动降低学习率
    reduceLROnPlateau = ReduceLROnPlateau(monitor="loss")
    return [tensorboard, checkpoint, reduceLROnPlateau]
```
模型保存主要是使用ModelCheckpoint这个callback，这里另外的两个callback我觉的也比较重要，一个是TensorBoard可视化的，另一个是自动修改学习率的，具体参考自：
> [苟且偷生小屁屁](https://www.jianshu.com/u/e95732444cf5)的[Keras保存最好的模型](https://www.jianshu.com/p/0711f9e54dd2)

说道模型保存，就会有模型的加载：
```python
model=tf.keras.models.load_model("./mnist.h5")
loss, accuracy = model.evaluate(x_test, tf.keras.utils.to_categorical(y_test, 10))
print(loss, accuracy)
```

# 整体代码
```python
import tensorflow as tf

from tensorflow.keras.callbacks import TensorBoard
from tensorflow.keras.callbacks import ModelCheckpoint
from tensorflow.keras.callbacks import ReduceLROnPlateau


# 常用callback
def getCallBacks():
    # tensorbord日志
    tensorboard = TensorBoard(log_dir="./logs")
    # 保存最佳的模型
    checkpoint = ModelCheckpoint(filepath="./mnist.h5", save_best_only=True, monitor="loss")
    # 当学习停滞时，自动降低学习率
    reduceLROnPlateau = ReduceLROnPlateau(monitor="loss")
    return [tensorboard, checkpoint, reduceLROnPlateau]

# 数据集
def getDataset(x, y, batch_size=32):
    # 数据转换，将x归一化，y变为one_hot向量
    def _parse_data(x, y):
        return tf.div(tf.cast(x, tf.float32), 255.0), tf.one_hot(y, 10)

    dataset = tf.data.Dataset.from_tensor_slices((x, y))
    # 数据集
    dataset = dataset.shuffle(60000).map(_parse_data).prefetch(batch_size * 10).batch(batch_size).repeat(100000)
    return dataset


mnist = tf.keras.datasets.mnist
(x_train, y_train), (x_test, y_test) = mnist.load_data()

#定义网络结构
model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(input_shape=(28, 28)),
    tf.keras.layers.Dense(512, activation=tf.nn.relu),
    tf.keras.layers.Dropout(0.2),
    tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])
model.compile(optimizer="Adam",
              loss="categorical_crossentropy",
              metrics=["accuracy"])

#训练
model.fit(getDataset(x_train, y_train), epochs=1, callbacks=getCallBacks(), steps_per_epoch=2000)
loss, accuracy = model.evaluate(x_test, tf.keras.utils.to_categorical(y_test, 10))
print(loss, accuracy)
```

# 额外：用SavedModel打包模型
TensorFlow小技巧推荐使用SavedModel打包模型，模型打包后配合TensorFlow Serving直接上线使用了
```python
def export_savedmodel(model):
    model_path = "model"
    model_version = 1
    model_signature = tf.saved_model.signature_def_utils.predict_signature_def(
        inputs={'input': model.input}, outputs={'output': model.output})
    export_path = os.path.join(compat.as_bytes(model_path), compat.as_bytes(str(model_version)))

    builder = tf.saved_model.builder.SavedModelBuilder(export_path)
    with tf.keras.backend.get_session() as sess:
        builder.add_meta_graph_and_variables(
            sess=sess,
            tags=[tf.saved_model.tag_constants.SERVING],
            clear_devices=True,
            signature_def_map={
                tf.saved_model.signature_constants.DEFAULT_SERVING_SIGNATURE_DEF_KEY:
                    model_signature
            })
    builder.save()
```
运行得到模型：
![](/img/model.png)

> 参考自[tobe](https://www.zhihu.com/people/tobegit3hub)的[我们给你推荐一种TensorFlow模型格式](https://zhuanlan.zhihu.com/p/34471266)