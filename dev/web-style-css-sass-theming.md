---
title: web-style-css-sass-theming
tags: [sass, style, theming]
created: '2020-11-01T06:18:50.917Z'
modified: '2021-01-01T20:07:04.485Z'
---

# web-style-css-sass-theming

# guide

- 切换主题的重点
  - 如何生成多套主题：主题公共部分拆分，基于scss变量、css vars
  - 如何切换主题：切换类名，动态下载解析渲染
- 一套主题包含所有组件 vs 一个组件的样式包含多套主题
  - theme-ui给出的方案是前者，使用带约束的样式值

# sass-theming

- ## [SCSS Theming with Dynamic Variables](https://stackoverflow.com/questions/57815278/scss-theming-with-dynamic-variables)
- 使用scss变量和mixin生成多套theme
  - The problem about this approach (apart from being tedious to maintain) is that it will bloat your CSS with things that are not related to theming – in the example above border will be repeated.

``` SCSS
// 声明多套主题的tokens
$themes: (
  light: (
      'text': dodgerblue,
      'back': whitesmoke 
  ),
  dark: (
      'text': white,
      'back': darkviolet
  )
);

// 生成多套主题样式的mixin
@mixin themify($themes) {
  @each $theme, $map in $themes {
    .theme-#{$theme} {
      $theme-map: () !global;
      @each $key, $submap in $map {
        $value: map-get(map-get($themes, $theme), '#{$key}');
        $theme-map: map-merge($theme-map, ($key: $value)) !global;
      }
      @content;
      $theme-map: null !global;
    }
  }
}
@function themedVal($key) {
  @return map-get($theme-map, $key);
}
@mixin themed {
    @include themify($themes){
        $text: themedVal('text') !global;
        $back: themedVal('back') !global;      
        @content;
    }
}
@include themed {
    div {
        background: $back;
        color: $text; 
        border: 1px solid; 
    }
}
// 最终生成的css，会有border重复
.theme-light div {
  background: whitesmoke;
  color: dodgerblue;
  border: 1px solid; //  <= 
}
.theme-dark div {
  background: darkviolet;
  color: white;
  border: 1px solid; // <=
}
```

- 使用scss结合css variables
  - You only need to add the theme class to e.g. the `body` tag and the nested elements will inherit the values

``` SCSS
@each $name, $map in $themes {
    .theme-#{$name} {
        @each $key, $value in $map {
            --#{$key}: #{$value};
        }
    }
} 

div {
    background: var(--back);
    color: var(--text); 
    border: 1px solid;
}

// 最终生成的css
.theme-light {
  --text: dodgerblue;
  --back: whitesmoke;
}

.theme-dark {
  --text: white;
  --back: darkviolet;
}

div {
  background: var(--back);
  color: var(--text);
  border: 1px solid;
}
```

- ## [Sass Theming: The Neverending Story_2015](https://www.sitepoint.com/sass-theming-neverending-story/)
- **The individual mixins approach**
- Thanks to property-named mixins, the API is both clean and clear, even to a non-experienced developer.
- This approach involves several mixins instead of one which might or might not be considered as extra complexity, even if most of them are just clones.
- Because the colors are directly fetched from the color map based on their key, it is not possible to manipulate them with color functions such as lighten or mix. 
  - It might be doable with an extended version of the mixin though.

``` SCSS
.media__title {
  font-size: 1em;
  margin: 0 0 10px;
  @include color('primary'); /* 1 */
}

@mixin themify($property, $key, $themes: $themes) {
  // Iterate over the themes
  @each $theme, $colors in $themes {
    // Create a selector (e.g. `.media.theme-unicorn, .theme-unicorn .media`)
    &.theme-#{$theme},
    .theme-#{$theme} & {
      // Output the declaration
      #{$property}: map-get($colors, $key);
    }
  }
}

@mixin color($arguments...) {
  @include themify('color', $arguments...);
}

@mixin background-color($arguments...) {
  @include themify('background-color', $arguments...);
}

@mixin border-color($arguments...) {
  @include themify('border-color', $arguments...);
}
```

- **The block mixin approach**
- The block mixin approach uses a single mixin instead of several one and relies heavily on the usage of the `@content` directive. 
- Contrary to the individual mixins solution, the block mixin gives the ability to manipulate colors with functions since we have direct access to the colors stored in theme variables.
- I feel like the API is still quick clear with this approach, especially since we use actual CSS declarations inside the mixin call, which might be easier to understand for some people.
- The use of global variables in such a way is kind of hacky I must say. No big deal, but code quality is not really the plus side here

``` SCSS
.media__title {
  font-size: 1em;
  margin: 0 0 10px;
  @include themify {
    color: $color-primary; /* 1 */
  }
}

@mixin themify($themes: $themes) {
  // Iterate over the themes
  @each $theme, $colors in $themes {
    // Create a selector (e.g. `.media.theme-unicorn, .theme-unicorn .media`)
    &.theme-#{$theme},
    .theme-#{$theme} & {
      // Set the theme variables with `!global`
      $color-primary: map-get($colors, 'primary') !global;
      $color-secondary: map-get($colors, 'secondary') !global;

      // Output user content
      @content;

      // Unset the theme variables with `!global`
      $color-primary: null !global;
      $color-secondary: null !global;
    }
  }
}
```

- **The big ol’ theme mixin approach**
- this mixin is the same for all components across the project. 
- If you want to make this new component themified in some way, you need to open the file where the themify mixin lives and add a couple of extra rules in there.
- Since the mixin content is manually maintained, it gives a high flexibility with selectors. You can pretty much do whatever you want in there.
- For the same reason, it also gives the ability to manipulate colors with functions like darken.
- Because everything themed is stored in this mixin’s content, it is not well suited for a modular approach. It is probably okay on small to medium projects with global stylesheets though.
- It might be confusing to have component styles divided into several places, i.e. the module stylesheet and the theme mixin.

``` SCSS
@mixin themify($theme, $colors) {
  // Output a theme selector
  .theme-#{$theme} {
    // Create the two variations of our selector
    // e.g. `.theme .component, .theme.component`
    .media,
    &.media {
      border-color: map-get($colors, 'primary');
    }

    .media__title
    &.media__title {
      color: map-get($colors, 'secondary');
    }
  }
}

.media__title {
  font-size: 1em;
  margin: 0 0 10px;
}

@each $theme, $colors in $themes {
  @include themify($theme, $colors);
}
```

- **The class approach**
- The class approach is actually a DOM-driven one. 
- The idea is that instead of applying specific theme styles from the stylesheet, you instead add theme classes to your markup. 
- These classes, generated with Sass, do nothing on their own but apply some styles when used in combination with our eternal `theme-$theme` classes.
- This solution has the benefit of being a DOM-based approach which turns out to be very interesting when having to manipulate themes on the fly with JavaScript. 
  - Indeed, it’s only a matter of adding/removing theme classes to/from elements; very handy.
- While the output of the themify mixin might look big, it actually is a quite DRY approach since every themed color, border-color, background-color and whatelse is applied through these classes.
- In some cases, a DOM-based approach might not be the correct way to proceed for instance when the markup is not hand-crafted (CMS, user-generated content).

``` SCSS

@mixin themify($themes: $themes) {
  // Properties to output, more can be added (e.g. `border-left-color`)
  $properties: ('border-color', 'background-color', 'color');

  // Iterate over the themes
  @each $theme, $colors in $themes {
    // Iterate over the colors from the theme
    @each $color-name, $color in $colors {
      // Iterate over the properties
      @each $property in $properties {
        // Create a selector
        // e.g. `.theme .color-primary, .theme.color-primary`
        .theme-#{$theme} .#{$property}-#{$color-name},
        .theme-#{$theme}.#{$property}-#{$color-name} {
          #{$property}: $color;
        }
      }
    }
  }
}
```

- ## [Is there a way to add dark mode to my application with SCSS?](https://stackoverflow.com/questions/57017955/is-there-a-way-to-add-dark-mode-to-my-application-with-scss)
- 基于scss变量和mixin编译出多主题的样式到同一个文件
  - Javascript is only used to toggle the class of your root element.
  - You don't have to define separate classes of themes for each element.
  - 注意，这里可以实现将一个组件的所有主题编译到一个文件

``` SCSS
// 组件的样式
.content {
  padding: 32px;
  @include theme() {
    color: theme-get('text-color');
    background-color: theme-get('bg-color');
  }
}

// 所有主题的tokens
$themes: (
  darkTheme: (
    'text-color': white,
    'bg-color': #424242
  ),
  lightTheme: (
    'text-color': black,
    'bg-color': #f5f5f5
  )
);

// 遍历themeTokens，生成多套主题
@mixin theme() {
  @each $theme, $map in $themes {
    // $theme: darkTheme, lightTheme
    // $map: ('text-color': ..., 'bg-color': ...)

    // make the $map globally accessible, so that theme-get() can access it
    $theme-map: $map !global;

    // make a class for each theme using interpolation -> #{}
    // use & for making the theme class ancestor of the class
    // from which you use @include theme() {...}
    .#{$theme} & {
      @content;    // the content inside @include theme() {...}
    }
  }
  // no use of the variable $theme-map now
  $theme-map: null !global;
}

@function theme-get($key) {
  @return map.get($theme-map, $key);
}

```

``` CSS
/* 最终编译出的css */

.content {
  padding: 32px;
}

.darkTheme .content {
  color: white;
  background-color: #424242;
}

.lightTheme .content {
  color: black;
  background-color: #f5f5f5;
}
```

# pieces

- 3 easy steps:
  - Compile all themes into different files upon deploy. This will take care of timestamping, zipping, etc.
  - Render page with default theme.
  - Use javascript to load alternate theme CSS.
- No need to mess with dynamic compilation and all that.
- To load a CSS dynamically you can use something like this:

``` JS
function loadCSS(url) {
  var cssfile = document.createElement("link");
  cssfile.setAttribute("rel", "stylesheet");
  cssfile.setAttribute("type", "text/css");
  cssfile.setAttribute("href", url);
}
```

- Unless you're trying to do something extreme like CSSZenGarden with hundreds of themes, or each theme is thousands of lines, I'd recommend setting each theme as it's own CSS class rather than it's own file.
  - It's straightforward to switch theme classes with JQuery
  - you will have to tag the elements you want the update with the ThemedElement class
- If you think you can manage your themes with classes rather than files, here's how we generate them with SASS. 
  - SASS doesn't support json style objects, so we have to reach way back and set up a bunch of parallel arrays with the theme properties. 
  - Then we iterate over each theme, substitute the dynamic properties into the auto generated theme class, and you're off to the races
  - 写theme样式时多用scss变量，然后通过循环逻辑编译出不同theme的样式类

# ref

- [Theming Web Apps with SASS_2017](https://medium.com/@dmitriy.borodiy/easy-color-theming-with-scss-bc38fd5734d1)
- [User theme switching with SASS - Ruby on Rails](https://stackoverflow.com/questions/8744941/user-theme-switching-with-sass-ruby-on-rails)
- [How to implement switchable themes in scss?](https://stackoverflow.com/questions/64390664/how-to-implement-switchable-themes-in-scss)
