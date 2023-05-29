---
layout: post
title: Tips of Matplotlib in Python (画图小技巧)
tags: [python,matplotlib]
categories: [Python]
toc:  true
math: true
---

# colorbar相关

### imshow设置颜色范围
{% highlight python %}
ax.imshow(data, vmin = vm0, vmax = vm1)
{% endhighlight %}

### 对数颜色轴
{% highlight python %}
ax.imshow(data, norm = matplotlib.colors.LogNorm(vmin=vm0, vmax=vm1))
{% endhighlight %}

### 多子图的画布添加一个公共颜色棒/添加一个colorbar在最右侧
{% highlight python %}
cax = fig.add_axes([0.925, 0.1, 0.025, 0.85])
cb = plt.colorbar(im,cax=cax)
{% endhighlight %}

### 自定义颜色轴需要显示的刻度
（如果是对数坐标，需要第二行代码）
{% highlight python %}
cb = plt.colorbar(im, ticks=[0.05,0.1,0.2,0.3])
cb.set_ticklabels([0.05,0.1,0.2,0.3])
{% endhighlight %}

### 设置颜色图colormap上下限以外的值的颜色，bad/NaN值颜色
用copy不改变该cmap的默认值
{% highlight python %}
import copy
import matplotlib
cmap = copy.copy(matplotlib.cm.Spectral) #拷贝Spectral这个colormap
cmap.set_under('gray',0.7) #值低于下限的颜色，默认为cmap中的最小值
cmap.set_over('gray',0.7)  #值高于上限的颜色
cmap.set_bad('gray',0.7)   #NaN值颜色
plt.imshow(im, cmap=cmap)
{% endhighlight %}


# 画布布局相关

### 隐藏空白子图
{% highlight python %}
ax.set_visible(False)
{% endhighlight %}

### 对齐图中x/y/所有轴标签
{% highlight python %}
fig.align_xlabels()
fig.align_labels()
{% endhighlight %}

### 调整画布边缘白色区域
{% highlight python %}
plt.subplots_adjust(left=0.05, bottom=0.1, right=0.9, top=0.9, wspace=0.15)
{% endhighlight %}


# 轴(ax)相关

### 获得轴的上下限
{% highlight python %}
ax.get_xlim()
{% endhighlight %}

### x轴反向
{% highlight python %}
plt.gca().invert_xaxis()
ax.invert_xaxis()
{% endhighlight %}

### 对数y轴
{% highlight python %}
ax.set_yscale('log')
{% endhighlight %}

### 关闭、隐藏x轴刻度标签
{% highlight python %}
plt.setp(ax.get_xticklabels(), visible=False)
{% endhighlight %}

### 关闭y轴主/次刻度
{% highlight python %}
plt.setp(ax.get_yticklines(minor=True), visible=False)
{% endhighlight %}

### 图的右侧添加刻度和标签
{% highlight python %}
ax.tick_params(right = True, labelright = True)
{% endhighlight %}

### 双y轴/创建副y轴的ax
{% highlight python %}
ax2 = ax.twinx()
{% endhighlight %}

### 全局xlabel/总ylabel
{% highlight python %}
fig.supxlabel('x')
{% endhighlight %}

### 设置y刻度/刻度标签的颜色
{% highlight python %}
ax.tick_params(color='C0')
ax.tick_params('y',labelcolor='C0')
{% endhighlight %}


# 未整理

### imshow自定义长宽比（像素不固定为正方形/自动拉伸像素）
{% highlight python %}
ax.imshow(data, aspect='auto')
{% endhighlight %}

### 显示坐标网格（只对主刻度显示）
{% highlight python %}
plt.grid(True,ls=':',lw=0.2,zorder=1,color='dimgray', which="major")
# 若只画x轴的网格
ax.xaxis.grid(True)
{% endhighlight %}

### text文本右侧/上端/中心对齐
{% highlight python %}
plt.text(ha='right', va='top')
plt.text(va='center')
{% endhighlight %}

### text文本参照ax百分比确定位置，调整行距
{% highlight python %}
plt.text(transform = ax.transAxes, linespacing=1.5)
{% endhighlight %}

### 随机选1/10的点，常用于减少散点数量
{% highlight python %}
ind = np.random.randint(0,len(x),size=round(len(x)/10))
{% endhighlight %}

### 只在最外侧坐标轴显示label / 判断ax是否在边缘的命令
{% highlight python %}
if ax.is_last_row():   ax.set_xlabel('x')
if ax.is_first_col():  ax.set_ylabel('y')
{% endhighlight %}

### imshow以左下角为原点
{% highlight python %}
plt.imshow(origin='lower')
{% endhighlight %}

### imshow保存图片时候像素边界模糊/串色的问题，把默认的反锯齿插值设为none
{% highlight python %}
plt.imshow(data, interpolation='none')
{% endhighlight %}

### 设置子图投影法
{% highlight python %}
fig,axes = plt.subplots(1,1, figsize=(10,5), dpi=200, subplot_kw={'projection': 'mollweide'})
{% endhighlight %}

### 设置为默认风格
{% highlight python %}
import matplotlib.style as style
style.use('default')
{% endhighlight %}

### fits画图使用文件内含的坐标系
