# Natours
hands-on project from the udemy course by Jonas Schmedtmann.

## Notes

### About Section 

h2標題 `.heading-secondary`

* 文字漸變效果 - `-webkit-background-clip`
```scss
.heading-secondary {
  // 略...
  background-image: linear-gradient(
    to right,
    $color-primary-light,
    $color-primary-dark
  );
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent; // 讓文字是透明的
}
```

* hover 特效 - `skewX() skewY()`
```scss
.heading-secondary {
  // 略...
  transition: all 0.2s;

  &:hover {
    transform: skewY(2deg) skewX(15deg) scale(1.1);
    text-shadow: 0.5rem 1rem 2rem rgba($color-black, 0.2);
  }
}
```
圖片組合 hover 效果 `.composition__photo`

* outline-offset 讓外邊框向外擴展

```scss
.composition {
  // 略...

  &__photo {
    // 略...
    outline-offset: 2rem;

    // 略...

    &:hover {
      outline: 1.5rem solid $color-primary;
      transform: scale(1.05) translateY(-0.5rem);
      box-shadow: 0 2.5rem 4rem rgba($color-black, 0.5);
      z-index: 10;
    }
  }

  // 在觸發懸浮時 讓不是被摸到的圖片縮小一點
  &:hover &__photo:not(:hover) {
    transform: scale(0.95);
  }
}
```

### Features Section 

背景歪斜效果

```scss
.section-features {
  padding: 20rem 0;
  background-image: linear-gradient(
      to right bottom,
      rgba($color-primary-light, 0.8),
      rgba($color-primary-dark, 0.8)
    ),
    url(../img/nat-4.jpg);
  background-size: cover;

  transform: skewY(-7deg);
  margin-top: -10rem;

  // 選取所有第一個 child (此處選擇到 .row) 讓它偏移回來
  & > * {
    transform: skewY(7deg);
  }
}
```

### Tours Section

卡片 `.card`

* 翻轉效果

```scss
.card {
  position: relative;
  // perspective transform 的 3D 透視效果
  // 參考文章：https://www.casper.tw/css/2013/10/11/css-perspective/
  perspective: 150rem;
  -moz-perspective: 150rem; // 針對老版本火狐的適配
  height: 50rem;

  &__side {
    // 使用絕對定位使兩張卡片疊在一起
    position: absolute;
    top: 0;
    left: 0;
    height: 50rem;
    width: 100%;
    transition: all 0.8s ease;
    // backface-visibility 設定成 hidden, 讓背面為不可視
    backface-visibility: hidden;

    &--front {
      background-color: $color-white;
    }

    &--back {
      // 背面一開始是反轉的, hover 後翻回 0
      transform: rotateY(180deg);
    }
  }

  &:hover &__side--front {
    transform: rotateY(-180deg);
  }

  &:hover &__side--back {
    transform: rotateY(0);
  }
}
```

* 背景圖特效 - `background-blend-mode` 

```scss
&__picture {
  background-size: cover;
  height: 23rem;
  // 背景混合模式, 參考文章：https://ithelp.ithome.com.tw/articles/10194930
  background-blend-mode: screen;
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);

  &--1 {
    background-image: linear-gradient(
        to right bottom,
        $color-secondary-light,
        $color-secondary-dark
      ),
      url(/img/nat-5.jpg);
  }
}
```

* 卡片標題文字 - `box-decoration-break`

> box-decoration-break 屬性規定當元素框被分段時，如何應用元素的 background、padding、border、border-image、box-shadow、margin 以及 clip-path。

```scss
&__heading {
  position: absolute;
  top: 12rem;
  right: 2rem;

  text-align: right;
  width: 75%;
  // 略...
}

&__heading-span {
  padding: 1rem 1.5rem;
  box-decoration-break: clone;

  &--1 {
    background-image: linear-gradient(
      to right bottom,
      rgba($color-secondary-light, 0.85),
      rgba($color-secondary-dark, 0.85)
    );
  }
}
```

### Stories Section

故事卡片 `.story`

* 文繞圖(圓弧狀) - `float`、`shape-outside`、`clip-path`

```scss
&__shape {
  position: relative;
  width: 15rem;
  height: 15rem;
  float: left;
  // 讓文字繞著圓弧排版
  shape-outside: circle(50% at 50% 50%);
  // 將圖片切成圓形
  clip-path: circle(50% at 50% 50%);
  transform: translateX(-3rem) skewX(12deg);
  // 去除 hover 時出現的邊線
  overflow: hidden;
}
```

* 模糊效果 - `filter`

```scss
.story {
  &__img {
    height: 100%;
    transform: translateX(-4rem) scale(1.4);
    backface-visibility: hidden;
    transition: all 0.5s;
  }

  &:hover &__img {
    transform: translateX(-4rem) scale(1);
    // blur 模糊, brightness: > 100% 變亮, < 100% 變暗
    filter: blur(3px) brightness(80%);
  }
}
```

### Booking Section

"solid color gradients" (透過漸層切出兩個區塊)

```scss
.book {
  // 漸層方向亦可設置為角度, 延伸到 50% 後將剩下的改成透明 (transparent)
  background-image: linear-gradient(
      105deg,
      rgba($color-white, 0.9) 0%,
      rgba($color-white, 0.9) 50%,
      transparent 50%
    ),
    url(/img/nat-10.jpg);
}
```
輸入框 `.form__input`

* focus 底線效果

```scss
.form {
  &__input {
    // 略...
    border: none;
    // 預留 border-bottom 位置
    border-bottom: 3px solid transparent;
    transition: all 0.3s;

    &:focus {
      outline: none;
      box-shadow: 0 1rem 2rem rgba($color-black, 0.1);
      border-bottom: 3px solid $color-primary;
    }

    &:focus:invalid {
      border-bottom: 3px solid $color-secondary-dark;
    }
  }
}
```

* placeholder 滑動特效 - `:placeholder-shown`

```scss
.form {
  &__input {
    // 略...
    &::placeholder {
      color: $color-grey-dark-2;
    }
  }

  &__label {
    // 略...
    display: block;
    transition: all 0.3s;
  }

  &__input:placeholder-shown + &__label {
    opacity: 0;
    visibility: hidden;
    transform: translateY(-4rem);
  }
}
```

radio 單選框

> 使用 `::after` 及 `<span>` 客製化單選框
```html
<div class="form__radio-group">
  <input
    type="radio"
    class="form__radio-input"
    id="small"
    name="size"
  />
  <label for="small" class="form__radio-label">
    <span class="form__radio-button"></span>
    Small tour group
  </label>
</div>
```

```scss
&__radio-group {
  width: 49%;
  display: inline-block;
}
// 將原本的 input 給隱藏掉
&__radio-input {
  display: none;
}

&__radio-label {
  position: relative;
  padding-left: 4.5rem;
  font-size: $default-font-size;
  cursor: pointer;
}

&__radio-button {
  position: absolute;
  left: 0;
  top: -0.4rem;
  display: inline-block;
  height: 3rem;
  width: 3rem;
  border: 5px solid $color-primary;
  border-radius: 50%;

  &::after {
    content: '';
    display: block;
    height: 1.3rem;
    width: 1.3rem;
    border-radius: 50%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: $color-primary;
    opacity: 0;
    transition: opacity 0.2s;
  }
}

&__radio-input:checked ~ &__radio-label &__radio-button::after {
  opacity: 1;
}
```

### Navigation

Nav 導覽列 hover 效果 - `.navigation__link`

* 使用 `background-size` `background-position` 做到從右下至左上的背景位移

```scss
&__link {
  &:link,
  &:visited {
    // 設置為 inline-block 讓 padding 及 translateX 生效
    display: inline-block;
    
    // 略...

    background-image: linear-gradient(
      120deg,
      transparent 0%,
      transparent 50%,
      $color-white 50%
    );
    background-size: 220%;
    transition: all 0.4s;

    // 略...
  }

  &:hover,
  &:active {
    background-position: 100%;
    color: $color-primary;
    transform: translateX(1rem);
  }
}
```
導覽選單的縮放特效

```scss
.navigation {
  // 略...

  &__background {
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    // radial-gradient 放射漸層
    background-image: radial-gradient(
      $color-primary-light,
      $color-primary-dark
    );
    z-index: 1000;
    transition: transform 0.8s cubic-bezier(0.83, 0, 0.17, 1);
  }

  &__nav {
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    z-index: 1500;

    // 初始狀態設置為隱藏且寬度為 0
    opacity: 0;
    width: 0;
    transition: all 0.8s cubic-bezier(0.68, -0.6, 0.32, 1.6);
  }

  // 略...

  // 透過 checkbox 的偽類 `:checked` 去觸發點擊實的效果
  &__checkbox:checked ~ &__background {
    transform: scale(80);
  }

  &__checkbox:checked ~ &__nav {
    opacity: 1;
    width: 100%;
  }
}
```
漢堡選單特效

```scss
&__button {
  // 略...
  text-align: center;
  cursor: pointer;
}

// 略...

// ICON
&__icon {
  position: relative;
  margin-top: 3.5rem;

  &,
  &::before,
  &::after {
    width: 3rem;
    height: 2px;
    background-color: $color-grey-dark-3;
    display: inline-block;
  }

  &::before,
  &::after {
    content: '';
    position: absolute;
    left: 0;
    transition: all 0.2s;
  }

  &::before {
    top: -0.8rem;
  }

  &::after {
    top: 0.8rem;
  }
}

&__button:hover &__icon::before {
  top: -1rem;
}

&__button:hover &__icon::after {
  top: 1rem;
}

&__checkbox:checked + &__button &__icon {
  background-color: transparent;
}

&__checkbox:checked + &__button &__icon::before {
  top: 0;
  transform: rotate(135deg);
}

&__checkbox:checked + &__button &__icon::after {
  top: 0;
  transform: rotate(-135deg);
}
```

### Popup box

彈出框 `.popup`

* 布局 

> 使用 `display: table` `display: table-cell` 來實現內部等高布局
```scss
.popup {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba($color-black, 0.8);
  z-index: 9999;

  &__content {
    @include absCenter;

    width: 75%;
    background-color: $color-white;
    box-shadow: 0 2rem 4rem rgba($color-black, 0.2);
    border-radius: 3px;
    overflow: hidden;
    display: table;
  }

  &__left {
    width: calc((1 / 3) * 100%);
    display: table-cell;
  }

  &__right {
    width: calc((2 / 3) * 100%);
    display: table-cell;
    vertical-align: middle;
    padding: 3rem 5rem;
  }

  &__img {
    display: block;
    width: 100%;
  }

  &__text {
    font-size: 1.4rem;
    margin-bottom: 4rem;

    // 將文字分成兩列
    column-count: 2;
    column-gap: 4rem;
    column-rule: 1px solid $color-grey-light-2;

    // 同個字分行時補上 "-"
    hyphens: auto;
  }
}
```

### Responsive Images in HTML
參考文章：[響應式圖片 (Responsive Images): img srcset 用法介紹](https://shubo.io/responsive-image/)

> img srcset 可以根據螢幕的 pixel density 或是圖片在螢幕上的實際寬度，決定要載入哪張圖片。亦可搭配 `<picture>` 標籤一起使用，相較於每個 <img> 只能定義一組 srcset，每個 <picture> 內可以定義多組 source，其中每個 source 可以各自用 media 屬性指定 media query，並且用 srcset 定義各自的圖片集。

```html
<picture class="footer__logo">
  <source
    srcset="
      img/logo-green-small-1x.png 1x,
      img/logo-green-small-2x.png 2x
    "
    media="(max-width: 37.5em)"
  />
  <!-- 超出 media query 範圍就走原本的 img -->
  <img
    srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x"
    alt="Logo"
  />
</picture>
```
