# HDF5的操作
## 使用Python中的h5py
This part cites from this [Blog](http://www.cnblogs.com/Ponys/p/3671458.html)
### 写入文件
```Python
import numpy as np
import h5py
# 数据需要是np.array格式的
data = np.array( [222,333,444] )
label = np.array( [0,1,0] )
img_num = np.array( [0,1,2] )
# 新建一个h5文件
file = h5py.File('TrainSet_rotate.h5','w')
# 建立名为'train_set_x'的数据集，数据来源为'data'
file.create_dataset('train_set_x', data = data)
file.create_dataset('train_set_y', data = label)
file.create_dataset('train_set_num',data = img_num)
file.close()
```

### 读取文件
```Python
import numpy as np
import h5py
# 读方式打开文件
file=h5py.File('TrainSet_rotate.h5','r')
train_set_data = file['train_set_x']
train_set_y = file['train_set_y']
train_set_img_num =file['train_set_img_num']
file.close()
```
# Convert HDF5 to txt
## 使用cmd下的h5dump
[参考来源](http://stackoverflow.com/questions/23237159/convert-hdf5-file-to-other-formats)

You can use ```h5dump -o dset.asci -y -w 400 dset.h5```

```-o dset.asci``` specifies the output file

```-y -w 400``` specifies the dimension size multiplied by the number of positions and spaces needed to print each value. You should take a very large number here.

```dset.h5``` is of course the hdf5 file you want to convert

I think this is the easiest way to convert it to an ascii file, which you can import to excel or whatever you want. I did it a couple of times, and it worked for me.

但是这样做亲测会有个问题，当一个h5文件中包含多个数据集的时候，这样无法分别导出到多个文件。

