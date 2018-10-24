---
layout: post
title: Image IO 踩过的坑
categories: [Experience]
description: ImageIO 踩过的坑
keywords: Experience
---

记录一些 Image IO 常见的问题和解决方案。

---

# from numpy to PIL image 注意 data type 不一致的问题

numpy 默认 int64，转化为灰度 "L" 模式 需要转换成 "uint8"

```python
a = np.array([[0, 128], [210, 255]])
# print(a.dtype) # int64
im = Image.fromarray(a.astype('uint8'), mode = "L") # convert to uint8
print(np.array(im))
```





