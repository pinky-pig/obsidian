
```css
/* 滚动条 */
::-webkit-scrollbar{
  width:6px;
  height:6px;
  background-color: transparent;
  border-radius: 8px;
}

::-webkit-scrollbar-track-piece{
  width:24px;
  background-color:transparent;
  border-radius: 8px;
}

::-webkit-scrollbar-thumb:vertical{
  width:24px;
  height:24px;
  background: rgb(214, 212, 212);
  border-radius: 8px;
}

::-webkit-scrollbar-thumb:horizontal{
  width:24px;
  height:24px;
  background: rgb(214, 212, 212);
  border-radius: 8px;
}

::-webkit-scrollbar-button{
  display:none;
}

::-webkit-scrollbar-corner{
  display:none;
}


/* 文字选中颜色 */
::selection {
  background-color: #fff;
  color: #000;
}

/* 设置字体 */
@font-face {
  font-family: 'Digital';
  src: url('/fonts/DS-DIGIB.TTF');
  font-weight: normal;
  font-style: normal;
}

```