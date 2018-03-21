---
layout: default
title: 基于css变量利用input实现自由的网站换肤
---


2018-3-21-基于css变量利用input自由实现网站换肤
===================
众所周知，在过去的很长时间里，网站换肤的基本原理都是通过提前写好几套css，通过使用js更换相应的css来实现的。前几天看到好基友[@MechanicianW](https://github.com/MechanicianW)翻译的一篇文章[关于 CSS 变量，你需要了解的一切](https://github.com/MechanicianW/gold-miner/blob/2c8ccaaf227a84122eb3e30664af857044a394e7/TODO/everything-you-need-to-know-about-css-variables.md)，意识到换肤的新时代来了（当然如果新时代还有换肤的需求的话）。
想了一下，想要实现自由换肤，那么肯定要一个能够自由选择颜色的工具，第一反应就是使用H5的<code><input type="color"></code>你可以点这个试试👉<input type="color">，它的兼容状态如下：
![color兼容](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/typecolor.png)
css变量的兼容状态如下：
![css变量](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/cssvar.png)
本文暂且只基于新版Chrome往下进行。
<input type="color">的使用非常简单，点击input框就会弹出系统的色盘，点击颜色就会更新input的value值。结合css变量就能实现同步更换。
![color](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/syscolor.png)
```html
<input id="picker" type="color"/>

```
```css
body {
		/*以两个横线--开头的“属性”都是 CSS 变量，通过 var() 函数来引用变量*/
    background-color: var(--bg-color, #fff);
}

```
```javascript
const root = document.documentElement;
const Picker = document.getElementById("picker");
Picker.addEventListener("change", function(e) {
  //通过设置'--bg-color'属性来改变css中body的background-color
  root.style.setProperty('--bg-color', e.target.value);
})

```
是的你没看错，上面这些代码就能异常方便地实现网站换肤了，你要是嫌默认的样式丑，还可以这样改一下：

```css
input[type="color"] {
    width: 40px;
    height: 40px;
    border: 0;
    padding: 0;
    border-radius: 40px;
    outline: none;
    -webkit-appearance: none;
}
input[type="color"]::-webkit-color-swatch-wrapper {
    border-radius: 40px;
    background: radial-gradient(red, orange, yellow, springgreen, deepskyblue, skyblue);
}
input[type="color"]::-webkit-color-swatch {
    display: none;
}

```

仔细观察一下会发现上面的实现方式有个小小的遗憾，就是不能选择透明度，那么怎么办呢，我又想到了input的另一种type：range，range的兼容状态如下：
![range兼容](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/range.png)

利用range结合设置rgba中各项的值，不仅能更改颜色，还能设置颜色的透明度。

想要用户对颜色进行选择，肯定需要一个视觉的入口，那么对 input[type="range"] 进行一个背景的设置就可以了：
```html
<input id="range-picker" type="range" class="rgb"/>

```
```css
input[type="range"] {
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);
}
input[type="range"].rgb {
    margin-top: 2px;
    /*设置渐变的背景色，以rgb值的方式进行设置，方便后续计算*/
    background: linear-gradient(to right,rgb(255,0,0), rgb(255,0,255), rgb(0,0,255),rgb(0,255,255), rgb(0,255,0), rgb(255,255,0), rgb(255,0,0) );
    width: 480px;
    -webkit-appearance: none;
    height: 12px;
    outline: none;
}
/*设置小滑块的样式*/
input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    cursor: default;
    height: 16px;
    width: 16px;
    background: none repeat scroll 0 0 #fff;
    border-radius: 8px;
    z-index: 5;
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);
    position: relative;
}

```

而设置透明度需要另一个range，同样通过设置背景来实现视觉入口：
```html
<input id="alpha-picker" type="range" class="alpha"/>

```
```css
input[type="range"].alpha {
    margin-top: 6px;
    width: 480px;
    -webkit-appearance: none;
    height: 12px;
    outline: none;
    position: relative;
}
input[type="range"].alpha::before{
    display: block;
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 480px;
    height: 12px;
    background: linear-gradient(to right,rgba(255,0,0,0), rgba(255,0,0,1) );
}

```
获取透明度的值比较简单，需要思考的就是如何利用range的值就算出颜色值。观察一下range的渐变背景色: linear-gradient(to right,rgb(255,0,0), rgb(255,0,255), rgb(0,0,255),rgb(0,255,255), rgb(0,255,0), rgb(255,255,0), rgb(255,0,0) );
可以看出总共分为6个区间，每个区间的距离值为17，在这6个区间里分别确定具体的颜色值就可以了，比如在第一区间，rgb(255,0,0) 到 rgb(255,0,255)，变动的就是rgb值的第三个数值，那么获取到当前range值，假设为val，计算它在该区间内的比例 per = val / 17，然后用比例乘以255就可以获得当前的颜色值了。
具体代码如下：
```javascript
	const root = document.documentElement;
  const rangePicker = document.getElementById("range-picker");
  const alphaPicker = document.getElementById("alpha-picker");
  let alpha = 1;
  let color = 'pink';
  rangePicker.addEventListener("change", function(e) {
    const rangeValue = parseInt(e.target.value, 10);
    let colorStep = 0;
    if (0 <= rangeValue && rangeValue < 17) {
      colorStep = (rangeValue / 17) * 255;
      color = `rgba(255, 0, ${colorStep}, `;
    } else if (17 <= rangeValue && rangeValue < 33) {
      colorStep = 255 - ((rangeValue - 17) / 17) * 255;
      color = `rgba(${colorStep}, 0, 255, `;
    } else if (33 <= rangeValue && rangeValue < 50) {
      colorStep = ((rangeValue - 33) / 17) * 255;
      color = `rgba(0, ${colorStep}, 255, `;
    } else if (50 <= rangeValue && rangeValue < 67) {
      colorStep = 255 - ((rangeValue - 50) / 17) * 255;
      color = `rgba(0, 255, ${colorStep}, `;
    } else if (67 <= rangeValue && rangeValue <83) {
      colorStep = ((rangeValue - 67) / 17) * 255;
      color = `rgba(${colorStep}, 255, 0, `;
    } else if (83 <= rangeValue && rangeValue <= 100) {
      colorStep = 255 - ((rangeValue - 83) / 17) * 255;
      color = `rgba(255, ${colorStep}, 0, `;
    }
    let colorValue = `${color}${alpha})`;
    root.style.setProperty('--bg-color', colorValue)
  })
  alphaPicker.addEventListener("change", function(e) {
    alpha = parseInt(e.target.value, 10) / 100;
    let colorValue = `${color}${alpha})`;
    root.style.setProperty('--bg-color', colorValue)
  })

```

效果如下：
![效果](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/result.png)

