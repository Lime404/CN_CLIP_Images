# 跨模态检索(文搜图/图搜图)
2024.06.19 本项目使用[Chinese-CLIP](https://github.com/OFA-Sys/Chinese-CLIP)搭建文搜图/图搜图页面,旨在帮助用户快速使用跨模态检索任务。本项目代码针对MUGE数据集约19w(189585张)数据作为底库数据。本项目提供了提取特征, 检索, 以及uI代码, 下文中将详细介绍细节。


# 开始用起来！
## 安装要求
本项目代码目前完全使用CPU版本, GPU版本需要代码稍作修改。

运行下列命令即可安装本项目所需的三方库,主要用到cn_clip库。
```bash
pip install -r requirements.txt
```

# cn_clip库 本人安装版本是python3.6  版本过高拉不到库

# 跨模态检索
## 代码组织
下载本项目后, 工作区目录结构如下：

```
search_text_img/ 
└── extract_features.py    #特征提取，可以单独每次提取图片，会把特征追加到[features.npy][photo_ids.csv]中， 
                            #提取完的图片全部丢到/Users/songyanan/MUGE/**根目录下面就行
└── [miniosync.py](miniosync.py) #同步图片到本地做数据集
└── search.py              #特征比对
└── web.py                 #gradio UI界面
└── assets                 # 界面图像展示
└── README.md
└── requirements.txt
└── models        #目录主要方便保存模型,若没有模型,会自动下载存放在该路径
└── features/
    ├── freatures.npy      #底库特征数据落盘
    ├── photo_ids.csv      #底库特征数据id落盘
```

## 修改/运行代码
### 修改代码
- search.py文件修改数据所在路径(和你本地保持一致),如下所示, 底库数据路径和模型路径: [底库数据和特征](https://pan.baidu.com/s/1St1Py5nLLxTjcWvU787f2A?pwd=urwv), 提取码: urwv。数据解压缩即可, 无需将多个文件夹内的图像放在一个文件夹内。
- 模型freatures.npy,photo_ids.csv下载后放在features文件夹内, 如上述工作目录所示。
```python
def display_pic(photos, file_list, top_k, top_p):
    path = r'/Users/songyanan/MUGE/'

    photos_path = Path(path)
    # print(os.listdir(path))
    # photos_files = list(photos_path.glob("**/*.jpg"))
```

### 运行代码
- 运行web.py 即可跳转到web界面,默认ip:http://0.0.0.0:8089

```
python web.py
```

## 界面展示
* 运行代码后,访问

<div align="center">
    <img src="assets/text_img.png" alt="文搜图"  />
    <img src="assets/img_img.png" alt="图搜图"  />
</div>


## 注意事项
* web界面上提供了多种模型的选择,不同模型对应的特征纬度不同。但是底库数据(MUGE)目前是使用vit-B-16模型提取特征的, 因此界面上检索只支持vit-B-16模型。 
* 若要支持使用其他模型检索, 需要使用相关模型重新对底库数据提取特征, 此处读者可自行修改。



# 引用
如果觉得本项目好用，希望能给我们提个star并分享给身边的用户，欢迎给相关工作citation，感谢支持！

