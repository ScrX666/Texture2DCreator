# Texture2DCreator
这个工具旨在将Texture2D的资产生成Texture2DArray格式以及生成一张TextureAtlas的图集来优化游戏贴图大小。
该工具是从[https://gist.github.com/Cyanilux/e672f328c4cafb361b490a5943c1c211#file-tex2darraycreator-cs-L140](https://gist.github.com/Cyanilux/e672f328c4cafb361b490a5943c1c211#file-tex2darraycreator-cs-L140)，在此基础上添加了生成Atlas功能，修改了部分功能，并优化了部分编辑器格式。
矩形填充排序算法使用MaxRectsBinPack库。[https://github.com/juj/RectangleBinPack/blob/master/MaxRectsBinPack.h#L1](https://github.com/juj/RectangleBinPack/blob/master/MaxRectsBinPack.h#L1)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/38597961/1695091802655-ad7f6678-cd61-49ba-b01b-090373372e3b.png#averageHue=%233d3d3d&clientId=uf23794f5-d3d1-4&from=paste&height=821&id=ua30eb97b&originHeight=821&originWidth=533&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73654&status=done&style=none&taskId=u9932fec2-5e6d-4f26-bf3a-010ed6a371c&title=&width=533)
## LoadTexture2DArray
可以将Texture2DArray资产反加载为一张张的贴图，并且可以直接替换或删除其中的某一张贴图，也可以在此基础上继续增加贴图。
## Texture Array Slices
用下面的加减号选中对于行添加或删除指定贴图，这个是存在一个List<Texture2D>中，无最大限制。
但是第一张贴图的大小和格式，决定了Texture2DArray的格式和大小，如果要生成Texture2DArray，所有texture的大小和格式需要相同。
## Mip Maps Enabled?
决定了是否为Array写入mipmap，不影响Atlas的mip生成，因为目前是由硬件直接支持的，但是你可以通过替换源码中的SaveTextureAtlas()函数，实现图集中每个子图的mip生成。（BUG）
## Save Texture Array
保存为Texture2D Array，格式为asseet。
## Save to Tex2D Atlas
保存为Atlas，格式为TGA，若需要其他格式，可以在源码中修改。
## Rect Method
生成Atlas的矩形填充算法，不同的List顺序会影响算法输出的结果，具体算法请阅读MaxRectsBinPack库。
```javascript
		RectBestShortSideFit, ///< -BSSF: Positions the rectangle against the short side of a free rectangle into which it fits the best.
		RectBestLongSideFit, ///< -BLSF: Positions the rectangle against the long side of a free rectangle into which it fits the best.
		RectBestAreaFit, ///< -BAF: Positions the rectangle into the smallest free rect into which it fits.
		RectBottomLeftRule, ///< -BL: Does the Tetris placement.
		RectContactPointRule ///< -CP: Choosest the placement where the rectangle touches other rects as much as possible.
```

