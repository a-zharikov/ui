# zui
Простой и легкий SCSS фреймворк

## Установка пакета
`npm install zharikov-ui`

# Миксины
## _align
Предназначен для абсолютного `position: absolute;` выравнивания элементов.
### Вызов
`@include center` - по центру;  
`@include top_center` - вверху по центру;  
`@include top_left` - вверху слево;  
`@include top_right` - вверху с право;  
`@include bottom_center` - снизу по центру;  
`@include bottom_left` - снизу слево;  
`@include bottom_right` - снизу справа;  
`@include left_center` - слева по центру;  
`@include right_center` - справа по центру.
#### SCSS
```scss
.block {
  @include center;
}
```
#### CSS
```css
.block {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## _breakpoint
### Основные поинты
```scss
@mixin mq($media) {
  @if $media == mobile {
    @media only screen and (max-width: 649px) {
      @content;
    }
  }
  @else if $media == tablet {
    @media only screen and (min-width: 650px) and (max-width: 1023px) {
      @content;
    }
  }
  @else if $media == laptop {
    @media only screen and (min-width: 1024px) and (max-width: 1239px) {
      @content;
    }
  }
  @else if $media == desktop {
    @media only screen and (min-width: 1240px) {
      @content;
    }
  }
}
```
### Вызов
**Телефон**  
```scss
@include mq(mobile) {
  // Твои стили для элемента
}
```
**Планшет**  
```scss
@include mq(tablet) {
  // Твои стили для элемента
}
```
**Ноутбук**  
```scss
@include mq(laptop) {
  // Твои стили для элемента
}
```
**Компуктер**  
```scss
@include mq(desktop) {
  // Твои стили для элемента
}
```
### DeБагер
`.__mqDebag` - данный класс выводит блок с названием брекпоинта в блоке на который повешен этот класс.  
```html
<div class="container __mqDebag"></div>
```
### Плавающий поинт
Используется для точной подстройки элементов. При помощи него можно переключать сетку блоков в нужном месте.
```scss
@mixin screen($min-width: null, $max-width: null) {
  @if $min-width != null and $max-width != null {
    // Если указаны оба параметра min-width и max-width
    @media only screen and (min-width: #{$min-width}px) and (max-width: #{$max-width}px) {
      @content;
    }
  }
  @else if $min-width != null and $max-width == null {
    // Если указан только min-width
    @media only screen and (min-width: #{$min-width}px) {
      @content;
    }
  }
  @else if $min-width == null and $max-width != null {
    // Если указан только max-width
    @media only screen and (max-width: #{$max-width}px) {
      @content;
    }
  }
}
```
Имеет три состояния вызова для более точной настройки переходов:  
### Минимальное значение
Указывается одно значение.

#### SCSS
```scss
@include screen(100) {
  // Твои стили для элемента
}
```
#### CSS
```css
@media only screen and (min-width: 100px) {
  // Твои стили для элемента
}
```
### Максимальное значение
Первое значение **обязательно** должен быть `0`.
#### SCSS
```scss
@include screen(0,100) {
  // Твои стили для элемента
}
```
#### CSS
```css
@media only screen and (max-width: 100px) {
  // Твои стили для элемента
}
```
### Минимальное и максимальное значение
Указываются оба значения через запятую.
#### SCSS
```scss
@include screen(100,200) {
  // Твои стили для элемента
}
```
#### CSS
```css
@media only screen and (min-width: 100px) and (max-width: 200px) {
  // Твои стили для элемента
}
```

## _element
`@include border` - создает бордер у элемента.  
#### SCSS
```scss
.block {
  @include border(1,0,0,0,$primary,.3);
}
```
#### CSS
```css
.block {
  border-top: 1px solid #3C4EFA;
  border-right: 0px solid #3C4EFA;
  border-bottom: 0px solid #3C4EFA;
  border-left: 0px solid #3C4EFA;
  border-color: rgba(60, 78, 250, 0.3);
}
```
### Обрез текста в три точки
`@include text_count` - Ограничит текст с высотой строки и скроет его в три точки `...`
#### SCSS
```scss
.block {
  @include text_count(3, 1.5, false);
}
```
#### CSS
```css
.block {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  line-height: 1.5;
}
```
### Настройки
`false` - без принудительного переноса слов;  
`true` - включит перенос слов

## _flex
### Настройки
`$df` - flex;  
`$di` - inline-flex;  

`$rw` - row;  
`$rr` - row-reverse;  
`$cl` - column;  
`$clr` - column-reverse;  

`$fs` - flex-start;  
`$fe` - flex-end;  
`$cr` - center;  
`$sb` - space-between;  
`$sa` - space-around;  
`$bl` - baseline;  
`$sh` - stretch;  

#### SCSS
```scss
.block {
  @include flex($rw,$fs,$fs,$zui-4);
}
```
#### CSS
```css
.block {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;
  gap: 4px;
}
```
### inline-flex
#### SCSS
```scss
.block {
  @include flex($rw,$fs,$fs,$zui-4,$di);
}
```
#### CSS
```css
.block {
  display: inline-flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;
  gap: 4px;
}
```

## _grid
#### SCSS
```scss
.block {
  @include grid(repeat(2,1fr),auto,$zui-4);
}
```
#### CSS
```css
.block {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: auto;
  gap: 4px;
}
```

## _tt
### transition
`@include transition` - плавно изменяет `css` свойства.  
#### SCSS
```scss
.block {
  @include transition;
}
```
#### CSS
```css
.block {
  transition: all 500ms ease-in-out;
}
```
#### SCSS
```scss
.block {
  @include transition(250);
}
```
#### CSS
```css
.block {
  transition: all 250ms ease-in-out;
}
```

### transition-delay
`@include transition-delay` - плавно изменяет `css` свойства с задержкой.  
#### SCSS
```scss
.block {
  @include transition-delay(500,250);
}
```
#### CSS
```css
.block {
  transition: all 500ms ease-in-out;
  transition-delay: 250ms;
}
```

## _typography
Дефолтное значение, если не указывать цвет, то применится цвет по умолчанию.
#### SCSS
```scss
.block {
  @include text($normal-x5);
}
```
#### CSS
```css
.block {
  color: #202327;
  font: 400 20px/28px "Montserrat", sans-serif;
}
```
Установит кастомный текст.
#### SCSS
```scss
.block {
  @include text($normal-x5,$caption);
}
```
#### CSS
```css
.block {
  color: #788394;
  font: 400 20px/28px "Montserrat", sans-serif;
}
```
# Переменные
`color` - цвтовая палитра;  
`fonts` - шрифты;  
`size` - 