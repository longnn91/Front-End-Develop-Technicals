
**1. one() :**
<hr />
- one(): Chèn một hoặc nhiều sự kiện cho một thành phần được chọn, xác định một function để chạy khi xảy ra một sự kiện.

- Khi sử dụng .one(), function xử lý sự kiện chỉ chạy một lần duy nhất cho mỗi thành phần.

```javascript.one('Sự kiện',function(){...})```

```javascript
$('.test').one('click',function(){
    alert('Sự kiện này chỉ hiển thị một lần.');
});
```

```javascript.one('Sự kiện','bộ chọn',function(){...})```

```javascript
$('body').one('click','.test',function(){
    alert('Sự kiện này chỉ hiển thị một lần.');
});
```

```javascript
$("p").one("click", function(){
    $(this).animate({fontSize: "+=6px"});
});
```
**2. .append(), prepend(), .after() and .before():**
<hr />
**suppose:**

```
<div class='a'> //<---you want div c to append in this
  <div class='b'>b</div>
</div>
```

**2.1 .append() puts data inside an element at last index and**
___

```javascript
//when .append() executes it will look like this:
$('.a').append($('.c'));
//after execution:
<div class='a'> //<---you want div c to append in this
  <div class='b'>b</div>
  <div class='c'>c</div>
</div>
```
**2.2 .prepend() puts the prepending elem at first index**
___

```javascript
//when .prepend() executes it will look like this:

$('.a').prepend($('.c'));
//after execution:

<div class='a'> //<---you want div c to append in this
  <div class='c'>c</div>
  <div class='b'>b</div>
</div>
```
**3 .after() puts the element after the element**
___

```javascript
//using after:

$('.a').after($('.c'));
//after execution:

<div class='a'>
  <div class='b'>b</div>
</div>
<div class='c'>c</div> //<----this will be placed here
```
**4. .before() puts the element before the element**
___
```javascript
//using before:

$('.a').before($('.c'));
//after execution:

<div class='c'>c</div> //<----this will be placed here
<div class='a'>
  <div class='b'>b</div>
</div>
```

**1. Bạn có thể gọi một chức năng thiết lập lại trước khi sử dụng append(). Ví dụ như dưới đây :**
<hr />
```javascript
function resetNewReviewBoardForm() {
    $("#Description").val('');
    $("#PersonName").text('');
    $("#members").empty(); //this one what worked in my case
    $("#EmailNotification").val('False');
}
```
**1. :*How to dynamically remove elements from the DOM via jQuery*
<hr />
**id:**
```
<div id="removeMe" style="background-color: #333333; color: #FFFFFF; padding: 10px;">Remove me by clicking the button below.</div>
<button onclick="removeDiv('removeMe');">Remove</button>
```

```javascript
function removeDiv(divId) {
   $("#"+divId).remove();
}
```

**class:**

```
<div class="blueBox">Blue box #1</div>
<div class="blueBox">Blue box #2</div>
<div class="blueBox">Blue box #3</div>
<div class="redBox">Red box #1</div>
<div class="redBox">Red box #2</div>
<div class="redBox">Red box #3</div>
<div style="clear: both;"></div>
<button onclick="removeByClass('blueBox');">Remove just the blue boxes</button>
<button onclick="removeByClass('redBox');">Remove just the red boxes</button>
```

```javascript
function removeByClass(className) {
   $("."+className).remove();
}
```
**1. :this.id vs. $(this).attr('id')**
<hr />
They'll both return the element's ID, but if the element has no ID, then ```this.id``` will return a blank string while ```$(this).attr("id")``` will ```return undefined```

**1. :How to append a lot of divs with a unique id's**
<hr />
```
<button class="button">Press me</button>
<div class="body_div"></div>
```

```javascript
var counter = 1;

$('.button').click(function(){
  var $newDiv = $("<div></div>");
  $newDiv.attr("id", "newDiv" + counter++);
  $(".body_div").append($newDiv);
});
```

**1. jQuery removeAttr() Method :**
- Remove the style attribute from all ```<p>``` elements:

```
<p style="font-size:120%;color:red">This is a paragraph.</p>
<p style="font-weight:bold;color:blue">This is another paragraph.</p>
```

```javascript
$("button").click(function(){
    $("p").removeAttr("style");
});
```

**1. :**

**1. :**