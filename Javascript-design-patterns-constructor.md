#### I. JavaScript Design Pattern - Constructor Pattern
---
**Reference**: https://viblo.asia/p/javascript-design-pattern-constructor-pattern-bJzKmMyPK9N

- Đối với lập trình hướng đối tượng trong JavaScript, cách đơn giản nhất để tạo mới một object là sử dụng function kết hợp với từ khoá new. Bên trong hàm khởi tạo này, từ khoá this dùng để chỉ tới đối tượng mới. Thông thường, hàm khởi tạo được viết hoa chữ cái đầu tiên, dùng để phân biệt với các hàm số thông thường.

**1. Constructor cơ bản**
--- 
```javascript
function Animal(name, leg) {
  this.name = name;
  this.leg = leg;
  this.about = function () {
    return this.name + " has " + this.leg + " legs";
  };
}
  
// Usage:
var dog = new Animal("Dog", 4);
var bird = new Animal("Bird", 2);
console.log(dog.about()); // => Dog has 4 legs
console.log(bird.about());// => Bird has 2 legs
```
- Trong ví dụ trên, đối tượng sử dụng hàm khởi tạo **Animal** sẽ có 2 thuộc tính (name, leg) và 1 phương thức (about). Tuy nhiên, cách trên có nhược điểm là khó để kế thừa và phương thức about sẽ phải định nghĩa lại đối với mỗi đối tượng. Để khắc phục nhược điểm trên, ta có cách thứ hai là sử dụng **Prototypes**.

**2. Constructor với Prototypes**
--- 
- Trong JavaScript, mọi object (bao gồm **function**) đều tồn tại thuộc tính **prototype** - cũng là một object. Khi sử dụng hàm khởi tạo để tạo mới một object, mọi thuộc tính trong **prototype** đều được kế thừa cho các đối tượng mới.

```javascript
function Animal(name, leg) {
  this.name = name;
  this.leg = leg;
}
Animal.prototype.about = function() {
  return this.name + " has " + this.leg + " legs";
}

// Usage:
var dog = new Animal("Dog", 4);
var bird = new Animal("Bird", 2);
console.log(dog.about()); // => Dog has 4 legs
console.log(bird.about());// => Bird has 2 legs
```

**3. Constructor với từ khoá class**
--- 
- Từ khoá **class** thực chất là một hàm số đặc biệt. Sử dụng **class** cho phép khởi tạo đối tượng mới một cách trực quan, và gần với khái niệm class trong các ngôn ngữ lập trình khác như C++, Java,...

Một điểm khác giữa **class** và **function** là **function** thuộc dạng **hoisting**, còn **class** thì không. Nghĩa là bạn có thể sử dụng hàm số trước khi khai báo hàm. Trong khi nếu bạn sử dụng class trước khi khai báo class thì bạn sẽ nhận được thông báo lỗi **ReferenceError**.

```javascript
class Animal {
  constructor(name, leg) {
    this.name = name;
    this.leg = leg;
  }

  about() {
    return this.name + " has " + this.leg + " legs";
  };
}
 
// Usage:
var dog = new Animal("Dog", 4);
var bird = new Animal("Bird", 2);
console.log(dog.about()); // => Dog has 4 legs
console.log(bird.about());// => Bird has 2 legs
```

- Trong class, có một hàm duy nhất và đặc biệt là **constructor**, đây là hàm khởi tạo của class. Trong hàm này bạn có thể định nghĩa các thuộc tính (name, leg) giống như sử dụng function và phương thức (about). Ngoài ra, bạn có thể định nghĩa các **getter**, **setter** và các hàm **static**.
