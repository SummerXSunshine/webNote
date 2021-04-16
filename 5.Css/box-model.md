## 盒模型
## padding-box
### 百分比值
### 可以解决的问题
#### 保证图片的比例
```css
.img_container {
    position: absolute;
    width:100%;
    height:0;
    padding-top:56.25% //保持比例:16:9
    /*padding-bottom:56.25% //16:9*/
    /*padding-top:75% //4:3*/
    /*padding-bottom:75% //4:3*/
    overflow:hidden;
}
.img_item {
    position:absolute;
    object-fit:cover;
    max-width: 100%;
    min-height: none;// 可不加
    z-index: 1;
}
```