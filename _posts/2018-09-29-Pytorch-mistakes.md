---
layout: post
title: PyTorch 踩过的坑
categories: [PyTorch]
description: PyTorch 踩过的坑
keywords: PyTorch
---

记录一些 Pytorch 常见的问题和解决方案。

---

# 打印 Summary

记得把模型转化为 GPU 模式。

```Python
from model import UNet
from torchsummary import summary

model = UNet(1, 1).cuda()
print(summary(model, (1, 32, 32)))
```

# 多输出

```Python
def forward(self, x):
    # Do your stuff here
    ...
    x1 = F.log_softmax(x) # class probabilities
    x2 = ... # bounding box calculation
    return x1, x2
```

```Python
out1, out2 = model(data)
loss1 = criterion1(out1, target1)
loss2 = criterion2(out2, target2)
loss = loss1 + loss2
loss.backward()
```

## torchvision.transforms.ToTensor 对图片已经做了归一化

Converts a PIL Image or numpy.ndarray (H x W x C) in the range [0, 255] to a torch.FloatTensor of shape (C x H x W) in the range [0.0, 1.0].


