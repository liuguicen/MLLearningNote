# 基本技巧
将Tanh层作为生成器最后输出层
现在流行使用PixelNorm和InstanceNorm[3]，如果要用BN的话，只能在all-fake或all-real的mini-batch中使用。

# 使用leakyRelu不要使用relu
如果我们的像素值是在-1~1之间，relu直接就把像素截断，
最后一层要求数据在-1~1



# 数据增强 似乎很有用
一些论文里面提到
将所需数据量从70k降低到1-2k
Diffenentiable Augmentation For Data-Efficient GAN Training
论文
但是，在2020年五月，世界范围内的研究者们独立的发现一个简单的技术，可以将所需训练样本的数量降低到1-2k。那个简单的想法就是在训练过程中，对输入判别器的所有图像，不管是真实的，还是生成的，进行可微分的增强
论文：
Diffenentiable Augmentation For Data-Efficient GAN Training
解读：
https://blog.csdn.net/qq_30125323/article/details/113338327


If one were to augment at a low enough probability, the augmentations will not 'leak' into the generations.
如果一个“图片”以足够低的概率增强，增强就不会扩展到后代中。

By default, the augmentations used are `translation` and `cutout`. If you would like to add `color`, you can do so with the `--aug-types` argument.
默认情况下，增强使用平移和裁剪。你也可以通过上面的命令增加比如颜色这样的增强

You can customize it to any combination of the three you would like. The differentiable augmentation code was copied and slightly modified from <a href="https://github.com/mit-han-lab/data-efficient-gans/blob/master/DiffAugment_pytorch.py">here</a>.
你也可以定制化为任意你喜欢的3中组合。数据增强的代码来自。。。并做了简单的修改。



# 截断
GAN里面一些文章提到的一个技巧，降低多样性，提高生成质量。styleGAN 附录B有提到。


# 加速


# 减少模型大小


# 训练
GAN自推出以来就以训练困难著称，因为它的训练过程并不是寻找损失函数的最小值，而是寻找生成器和判别器之间的纳什均衡。前者可以直接通过梯度下降来完成，而后者除此之外，还需要其它的训练技巧。

csdn 文章
我们知道在图像分类任务中，较大的batch size有助于提升分类性能
目前已经有些实验表明提高batch size有助于提高生成图片的质量，也有助于减少训练的时间

# 模式崩溃
模式崩溃中的反复横跳问题，unrolled GAN中提到
就是生成器模式崩溃进入到图片流形的某个局部区域，判别器最优之后会对这个区域打低分，对真实数据的其它部分打高分，
然后更新生成器的时候，生成器会直接跳到其它高分区域，也就是真实数据的其它区域，然后这样一直循环，就是生成器的反复横跳，
停下训练之后，模式崩溃出现在不同的区域，生成结果就是单一但是每次不同的样本。

文章：How to Train a GAN? Tips and tricks to make GANs work