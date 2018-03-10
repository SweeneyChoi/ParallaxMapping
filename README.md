# ParallaxMapping

使用视差贴图，极大提升表面细节，使之具有深度感

## 依赖
* glfw3.lib 推荐在[官方网站](http://www.glfw.org/download.html)下载源代码，然后自行编译。本项目编译使用的是CMake和Visual Studio 2015.
* GLAD 打开GLAD的[在线服务](http://glad.dav1d.de/)可轻松配置。本项目使用OpenGL 4.3.
* stb_image.h 是[Sean Barrett](https://github.com/nothings)的一个非常流行的单头文件图像加载库，可以在[这里](https://github.com/nothings/stb/blob/master/stb_image.h)下载。本项目使用其来加载纹理图片。
* GLM 一个只有头文件的库，不用链接和编译。可以在它们的[网站](http://glm.g-truc.net/0.9.5/index.html)上下载。本项目使用其作为数学库。
* Assimp 一个非常流行的模型导入库，可以在[下载页面](http://assimp.org/main_downloads.html)选择相应的版本，自行使用CMake 和 Visual Studio 2015编译。

## 思想

视差贴图属于 **位移贴图(Displacement Mapping)** 技术的一种，它对根据储存在纹理中的几何信息对顶点进行位移或偏移。比如，每个纹理像素包含了高度值的纹理叫做 **高度贴图** 。

视差贴图的思想是修改纹理坐标使一个fragment的表面看起来比实际的更高或更低。

法线贴图通常根据高度贴图生成，法线贴图和高度贴图一起用能保证光照能和唯一相匹配。

使用 **反色高度贴图 ** （也叫 **深度贴图** ）去模拟深度比模拟高度容易。

## 实现

1. 使用高度贴图对纹理坐标进行位移,同样是在切线空间中进行计算

2. 使用这些经位移的纹理坐标进行diffuse和法线贴图的采样。最后fragment的diffuse颜色和法线向量就正确的对应于表面的经位移的位置上了

## 改进

- **陡峭视差映射(Steep Parallax Mapping)** 是视差映射的扩展，原则是一样的，但不是使用一个样本而是多个样本来采样。

- **视差遮蔽映射(Parallax Occlusion Mapping)** 和陡峭视差映射的原则相同，但不是用触碰的第一个深度层的纹理坐标，而是在触碰之前和之后，在深度层之间进行线性插值。根据表面的高度距离哪个深度层的深度层值的距离来确定线性插值的大小。

## 效果

![效果1](https://github.com/SweeneyChoi/ParallaxMapping/blob/master/images/parallaxMapping1.png)

![效果2](https://github.com/SweeneyChoi/ParallaxMapping/blob/master/images/parallaxMapping2.png)
