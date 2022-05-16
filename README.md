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
