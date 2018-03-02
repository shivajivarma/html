Tablet 
=====

### FIX 1

```css
.outer {
  overflow: scroll;
  -webkit-overflow-scrolling: touch;
  /* More properties for a fixed height ... */
}

.inner {
  height: calc(100% + 1px);
}
```

### FIX 2
```css
.outer:before {
  content:””;
  width: 1px;
  float: left;
  height: calc(100% + 1px);
  margin-left: -1px;
  display: block;
}
.outer:after{
  content:””;
  width: 100%;
  clear: both;
  display: block;
}
```

### FIX 3
```js
var isIPad = navigator.userAgent.match(/iPad/i) != null;
if(isIPad){
  setTimeout(function(){
    angular.element('.wrapper').css('overflow', 'auto');
    angular.element('.wrapper').css('-webkit-overflow-scrolling', 'touch');
    fixHeight();
  }, 300);
  angular.element($window).on("DOMContentLoaded orientationchange", function(){
    $timeout(function(){
      fixHeight();
    });
  });
}
function fixHeight() {
  angular.element('.wrapper').height($window.screen.height);
}
```
http://patrickmuff.ch/blog/2014/10/01/how-we-fixed-the-webkit-overflow-scrolling-touch-bug-on-ios/
