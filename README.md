# Natours
advanced css course project #1


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
