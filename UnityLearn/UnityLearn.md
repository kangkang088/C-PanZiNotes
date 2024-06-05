# UnityLearn

山佩歌津，2023年8月14日，QQ：2426966358

# DrawCall

渲染流水线的第一步是【CPU和GPU之间的通信】，有如下3个步骤：

1. 把数据加载到显存中：把网格和纹理等数据从硬盘加载到显存中（因为显卡对显存的访问速度更快）
2. 设置渲染状态：CPU根据材质球设置渲染状态，比如，使用哪个顶点着色器/片元着色器、光源属性、纹理等
3. 调用Draw Call：准备好上述工作后，CPU就调用一个渲染命令(Draw Call)来告诉GPU可以开始渲染啦。

> [Unity渲染优化的4种批处理：静态批处理，动态批处理，SRP Batcher 与 GPU Instancing - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/432223843)

# 四种批处理



动态批处理限制：

- 顶点属性最大限制900,
- 使用lightmap的物体不行进行批处理
- 使用MultiplePass的shader也不会进行批处理
- 接受实时阴影的物体也不会进行批处理