 ### 1. Select change():
 
 ```
 <div class="control_select">
    <select class="form-control" id="change_value" onchange="scaleClock.scale();">
        <option value="1">1x</option>
        <option value="2">2x</option>
        <option value="3">3x</option>
        <option value="4">4x</option>
        <option value="5">5x</option>
    </select>
</div>
```

```javascript
var CLOCK = (function() {
    var drawClock = function() {
        var initial = 250;
        var zoom = document.getElementById("rangeinput").value;
        console.log(zoom);
        var value = initial * zoom;
        // Draw Circle
        var svg = document.getElementById("clock");
        svg.setAttribute('width', value);
        svg.setAttribute('height', value);
    };
    return {
        init: function() {
            drawClock();
        },
        scale: function() {
            drawClock();
        }
    };
})();
CLOCK.init();
```

- Chú ý ```javascript document.getElementById("change_value").value ```: là nó lấy tất cả các attribute ```value=""``` của thẻ ```<option>```, dù ```id``` nằm trong thẻ ```<select>```

 ### 2. typeof: giống một từ khóa được dùng để kiểm tra một biến nào đó (hoặc một giá trị nào đó) có kiểu dữ liệu là gì
 
-Thông thường chúng ta có một số loại dữ liệu như sau:
  - number - số
  - string - chuỗi
  - object - đối tượng
  - undefined - không xác định
  
  var x = typeof value;
