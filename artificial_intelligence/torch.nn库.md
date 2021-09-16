### torch.nn库



torch.nn是专门为神经网络设计的模块化接口。nn构建于autograd之上，可以用来定义和运行神经网络。

- nn.Parameter
- nn.Linear&nn.conv2d等等
- nn.functional
- nn.Module
- nn.Sequential



#### nn.Parameter

- 定义可训练参数
- selfmy param=nn.Parameter（torch.randn（1））
- selfregister_parameter
- nn.ParameterList&nn.ParameterDict

· nn. ParameterList & nn. ParameterDict 

```
self.params=nn. ParameterList([ nn. Parameter(torch. randn(10,10)) for i in range(10)])
```

```
self.params=nn. ParameterDict({ left': nn. Parameter(torch. randn(5,10)),
								  right': nn. Parameter(torch. randn(5,10)) })
```



#### nn.Linear & nn.conv2d & nn.ReLU & nn.MaxPool2d（2））& nn.MSELoss等等

- 各种神经网络层的定义，继承于nn.Module的子类

  - selfconv1=nn.Conv2d（1，6，（5，5））

  - 调用时：self.conv1（x）

- 参数为parameter类型

  - layer=nn.Linear（1，1）
  - layer.weight=nn.Parameter（torch.Float Tensor（ [ [ 0 ] ] ) )
  - layer.bias=nn.Parameter（torch.Float Tensor（ [ 0 ] ] ) )



#### nn.functional

- 包含torch.nn库中所有函数，包含大量loss和activation function
  - torch.nn.functional.conv2d（jnput，weight，bias=None，stride=1，padding=0，dilation=1，groups=1）
- nn.functional.xxx是函数接口
- nn.functional.xxx无法与nn.Sequential 结合使用
- ·没有学习参数的（eg.maxpool，loss func，activation func）等根据个人选择使用nn.functional.xxx或nn.Xxx
- 需要特别注意dropout层

- nn与nn.functional 有什么区别？·

  - nn.functional.xxx是函数接口

  - nn.Xxx是.nn.functional.xxx的类封装，并且nn.Xxx都继承于一个共同祖先nn.Module

  - nn.Xxx除了具有nn.functional.xxx功能之外，内部附带nn.Module相关的属性和方法，eg.train()，eval()，load_state_dict，state_dict

    

#### nn.Sequential

```
# Example of using Sequential 卷积层串联成一个序列
mode1=nn. Sequential(
	nn. Conv2d(1,20,5), 
	nn. ReLU(), 
	nn. Conv2d(20,64,5), 
	nn. ReLU()
	)
	
# Example of using Sequential with OrderedDict  字典定义卷积层，定向访问
mode1=nn. Sequential(OrderedDict([      
	(' conv1', nn. Conv2d(1,20,5)),
	(' relu1', nn. ReLU()),
	(' conv2', nn. Conv2d(20,64,5)),
	(' relu2', nn. ReLU())
]))
```



#### 自定义网络模型

- nn. ModuleList

  ```
  class MyModule(nn. Module): ##继承nn.moudlee
  	def __init__(self): ##初始化函数
  		super(MyModule, self).__init_()
    		self. linears=nn. Modulelist([ nn. Linear(10,10) for i in range(10)]) ##线性结构
    	
      ##前向推理
    	def forward(self,x):
  	#ModuleList can act as an iterable, or be indexed using ints 
  	for i,1 in enumerate(self. linears): 
  		x=self. linears[i //2](x)+1(x) #前向处理
  	return x
  ```

- nn.ModuleDict

  ```
  class MyModule(nn. Module): 
  	def __init__(self): 
  		super(MyModule, self).__init__()
  		self. choices=nn. ModuleDict({ 
  			'conv': nn. Conv2d(10,10,3),
  		    'poo1': nn. MaxPool2d(3)
  		}) 
  		self. activations=nn. ModuleDict([
  			['1relu', nn. LeakyReLU()],
  			['prelu', nn. PReLU())]
  		])
  		
  	def forward(self,x, choice, act): 
  		x=self. choices[choice](x)
  		x=self. activations[act](x)
  		return x
  ```



#### nn.Module

- 它是一个抽象概念，既可以表示神经网络中的某个层（layer），也可以表示一个包含很多层的神经网络

- model.parameters()   可训练的参数

- model.buffers()          不可训练的参数

- model.state_dict()      访问网络结构中的所有参数

- model.modules()        模型中包含的所有模块

- forward()，to()

- 具体文档 https://pytorch.org/docs/stable/nn.html#torch.nn.Module

  ```
  import torch. nn as nn 
  import torch. nn. functional as F 
  ##通过继承nn. Module实现自定义模块，可能是一个层也可能是一个网络
  class Model(nn. Module): 
  	def__init__(self): 
  		super(Model, self).__init_()
  		self. convl=nn. Conv2d(1,20,5) ##两个卷积
  		self. conv2=nn. Conv2d(20,20,5)
  		
  	def forward(self,x): 
  		x=F. relu(self. convl(x))
  		return F. relu(self. conv2(x))
  ```

- Parameters VS buffers 

  - 一种是反向传播需要被optimizer更新的，称之为parameter （需要训练）

    - self.register parameter（"param"，param）
    - selfparam=nn.Parameter（torch.randn（1））

  - 一种是反向传播不需要被optimizer更新，称之为buffer （不需要训练）

    - self.register_buffer（'my_buffer'，torch.randn（1））#注册，方便获取

      

- state_dict()  &  load_state_dict

  - torch. save(obj=model. state_dict),f="models/net. pth") 保存模型

  - model. load_state_dict(torch. load("models/net. pth")) 加载模型

