# I. Memorize the company Project Outsite

**1. 20180328_I_DESIGN**
- Switch screen with smartphone.

>JavaScript Code:
```javascript
function myResizeFunction() {
  if($(window).width() <= 1100){
    // do something
  }
}
$(myResizeFunction); // Do on DOM ready
$(window).on("load resize", myResizeFunction); 
```

```javascript
$(window).resize(function() {
  calcHeight();
}).load(function() {
  calcHeight();
});
```

>JavaScript Code hiệu quả: Cái này có 1 cái hại là mỗi khi resize nó thực thi lại hành động
```javascript
// Bind to the resize event of the window object
$(window).on("resize", function () {
  // Set .right's width to the window width minus 480 pixels
  $(".content .right").width( $(this).width() - 480 );
// Invoke the resize event immediately
}).resize();
```

>JavaScript Code hiệu quả: 
```javascript
$('.nav-icons').click(function(e) {
  if($(window).width()<=1000){
    $(this).toggleClass('open');
  }
});
```

>JavaScript Code EventListener sẽ không hiểu:
```javascript
if($(window).width()<=1000){
  $('.nav-icons').click(function(e) {
    $(this).toggleClass('open');
  });
}
```

**2. ForEach**: item sẽ hiểu từng thẻ ```<li>```.
>JavaScript Code:
```javascript
var Navigation = {
  selector: {
    nav_item: document.querySelectorAll('.navigation ul li')  
  },
  init: function(){
    Navigation.nav_reset();
  },
  nav_reset: function(){
    if ($(window).width() > 1000) {
      Navigation.selector.nav_item.forEach(function(item) {
        item.style.WebkitOpacity = "1";
        item.style.msOpacity = "1";
        item.style.opacity = "1";
        item.style.WebkitTransform = "translate3d(0, 0, 0)";
        item.style.msTransform = "translate3d(0, 0, 0)";
        item.style.transform = "translate3d(0, 0, 0)";
      });
    } else if ($(window).width() <= 1000) {
      Navigation.selector.nav_item.forEach(function(userItem) {
        item.style.WebkitOpacity = "0";
        item.style.msOpacity = "0";
        item.style.opacity = "0";
        item.style.WebkitTransform = "translate3d(0, 40px, 0)";
        item.style.msTransform = "translate3d(0, 40px, 0)";
        item.style.transform = "translate3d(0, 40px, 0)";
      });
    }
  }
}
```

**3. TweenMax:** Thuộc tính ```autoAlpha: 0``` tương đương với ```opacity: 0```.

- Text.
```javascript
$(document).ready(function() {
    App.init();
    var currentSlide = 0;
    var slideItem = $('.slideItem');
    var countSlide = $('.slidersList .slideItem').length;
    var hgtWin = $(window).height();

    var Animation = {
        selector: {
            openning: '.openning',
            logo: '.logo',
            heading: '.slideTitle',
            balloons: '.balloonsImage',
            balloonsInner: '.imageRepresentInner',
            ellipseOne: '.ellipseOne',
            ellipseTwo: '.ellipseTwo',
            balloonsDetail: '.balloonsDetail',
            balloonTitle: '.balloonTitle',
            dateTime: '.dateTime',
            balloonsCaption: '.balloonsCaption',

        },
        handle: {
            logoTw: new TimelineMax(),
            mainTw: new TimelineMax()

        },
        init: function() {
            setTimeout(function(){
                Animation.show_logo();
            }, 150)
            Animation.animateTitle();
            Animation.change_slide();
        },
        show_logo: function(){
          Animation.handle.logoTw.fromTo(
                $(Animation.selector.logo), 0.5, 
                {css:{y: -160,opacity: 0,ease: Circ.easeOut}},
                {css:{y: 0,opacity: 1,ease: Circ.easeOut}}
            );  
        },
        animateTitle: function(){
            var titleChars = new SplitText($(Animation.selector.balloonTitle), { type: 'lines, words, chars' });
            var titleCharsTLM = new TimelineMax({ paused: !0 });
            titleCharsTLM.staggerFrom(titleChars.chars, 1, {y: 100+'%', opacity: 0, ease: Circ.easeOut }, .05, 0);
            titleCharsTLM.duration(1.4).restart(); 
        },
        slide: function() {
            var addtition_time = "-=0";
            var typeItem = '.slideItem' + currentSlide + ' ';
            if (currentSlide != 1) addtition_time = "-=0.5";
            Animation.handle.mainTw.to($(typeItem + Animation.selector.heading), 1, {x: '0%', opacity: 1, yoyo: true, ease: Circ.easeOut},addtition_time)
            if (currentSlide != countSlide){
                Animation.handle.mainTw.fromTo($(typeItem + Animation.selector.balloonsInner), 11, {y: hgtWin, opacity: 1, yoyo: true}, {y: -hgtWin-100, scale: 1.494, opacity: 1, yoyo: true, ease: SlowMo.ease.config(0.7, 0.7, false)},addtition_time)
            }else{
                Animation.handle.mainTw.fromTo($(typeItem + Animation.selector.balloonsInner), 11, {y: hgtWin, opacity: 1, yoyo: true}, {y: 0, scale: 1.494, opacity: 1, yoyo: true, ease: SlowMo.ease.config(0.7, 0.7, false)},addtition_time)
            }
            Animation.handle.mainTw.to($(typeItem + Animation.selector.ellipseOne), 6, {y: -hgtWin, opacity: 1, yoyo: true, ease: Power2.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.ellipseTwo), 6, {y: -hgtWin, opacity: 0.5, yoyo: true, ease: Power2.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.dateTime), 4, { y: 0, opacity: 1, yoyo: true, ease: Circ.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.balloonsCaption), 4, {y: 0, opacity: 1, yoyo: true, ease: Circ.easeOut}, "-=12")
                                   .to($(typeItem + Animation.selector.balloonsDetail),12, {y: '5%', opacity: 1, yoyo: true, ease: Circ.easeOut}, "-=11.5")
            if (currentSlide != countSlide){
                Animation.handle.mainTw.to($(typeItem + Animation.selector.balloonsDetail),12, {y: '-114%', opacity: 1, yoyo: true, ease: SlowMo.ease.config(0.7, 0.7, false),
                                        onComplete: function(){
                                            $(typeItem).removeClass('active');
                                        }
                                    }, "-=11.5")
                                   .to($(Animation.selector.heading), 0, {x: '-100%',opacity: 0, yoyo: true, ease: Circ.easeOut,onComplete: function(){
                                        setTimeout(Animation.change_slide, 0);
                                    }}, "-=1");
                                   Animation.animateTitle();
            }
        },
        change_slide: function() {
            var addtition_time = "-=0";
            if (currentSlide == countSlide) currentSlide = 0;
            if (currentSlide != 0) addtition_time = "-=2.0";
            var typeItem = '.slideItem' + (currentSlide + 1) + ' ';
            var position_balloon = (Math.round((Math.random() * 2) + 1) == 1) ? 'balloon_1' : 'balloon_2',
                position_eclip = (Math.round((Math.random() * 2) + 1) == 1) ? 'eclip_1' : 'eclip_2';
            $(typeItem).removeClass('balloon_1 balloon_2 eclip_1 eclip_2');
            $(typeItem).addClass(position_balloon + ' ' + position_eclip);
            Animation.handle.mainTw.to($(typeItem + Animation.selector.balloonsInner), 0, {y: hgtWin, opacity: 0, yoyo: true, scale: 1, ease: Power2.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.ellipseOne), 0, {y: hgtWin,scale: 1, opacity: 0, yoyo: true, ease: Power2.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.ellipseTwo), 0, {y: hgtWin, opacity: 0, yoyo: true, ease: Power2.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.balloonsDetail), 0, {y: '114%', yoyo: true, ease: Circ.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.dateTime), 0, {y: 70, opacity: 0, yoyo: true, ease: Circ.easeOut},addtition_time)
                                   .to($(typeItem + Animation.selector.balloonsCaption), 0, {y: 70, opacity: 0, yoyo: true, ease: Circ.easeOut,
                                        onComplete: function() {
                                            //Animation.slide();
                                            setTimeout(Animation.slide, 0)
                                        }
                                   },addtition_time);
            /*slideItem.removeClass('active');*/
            slideItem.eq(currentSlide).addClass('active');
            currentSlide++;
        }
    }
    
    Animation.init();
});
```

>JavaScript Code:
```javascript

```

**4. Hệ Thống Cảnh Báo Thiên Tai**
- https://www.windy.com/?2018-11-07-09,17.811,109.863,5

>JavaScript Code:
```javascript
$(document).ready(function() {
  //Handle no javascript
  $('body').removeClass('no_javascript');
  // Handle Suggest Search
  var data = [
    "Albania",
    "Andorra",
    "Armenia",
    "Austria",
    "Azerbaijan",
    "Belarus",
    "Belgium",
    "Bosnia & Herzegovina",
    "Bulgaria",
    "Croatia",
    "Cyprus",
    "Czech Republic",
    "Denmark",
    "Estonia",
    "Finland",
    "France",
    "Georgia",
    "Germany",
    "Greece",
    "Hungary",
    "Iceland",
    "Ireland",
    "Italy",
    "Kosovo",
    "Latvia",
    "Liechtenstein",
    "Lithuania",
    "Luxembourg",
    "Macedonia",
    "Malta",
    "Moldova",
    "Monaco",
    "Montenegro",
    "Netherlands",
    "Norway",
    "Poland",
    "Portugal",
    "Romania",
    "Russia",
    "San Marino",
    "Serbia",
    "Slovakia",
    "Slovenia",
    "Spain",
    "Sweden",
    "Switzerland",
    "Turkey",
    "Ukraine",
    "United Kingdom",
    "Vatican City"
  ];

  //create AutoComplete UI component
  $("#search-top").kendoAutoComplete({
      dataSource: data,
      filter: "startswith",
      separator: ", "
  }).keypress(function(e) {
    if (event.keyCode === 13) {
      $('.page-content').addClass('loading');
      function doneLoading(){
        $('.page-content').removeClass('loading');
      }
      setTimeout(function() {
        doneLoading();
      }, 2500);
      return false;
      //$(this).closest('form').trigger('submit');
    }
  });
  // Handle Tooltip
  function handleToolTip() {
    $('.control-right .tooltip').tooltipster({
      side: 'left',
      animation: 'fade',
      //trigger: 'click',
      theme: 'tooltipster-borderless'
    });
    $('.control-left .tooltip').tooltipster({
      side: 'right',
      animation: 'fade',
      //trigger: 'click',
      theme: 'tooltipster-borderless'
    });
  };
  // handleFullscreen
  var handleFullscreen = function(){
    var wrapper = $('#wrapper');
    var header = $('.header');
    var footer = $('.footer');
    var main_content = $('.page-container');
    var resetDefault = $(window).height() - ($('.header').height() + $('.footer').outerHeight()) + 'px';
    var is_check = true;
    
    $('.fullscreen-event').on('click', function(e){
      e.preventDefault();
      if($(this).hasClass('fullscreen')){
        $('.tool-map .tool-map-item a').removeClass('fullscreen');
        header.fadeOut(100);
        footer.fadeOut(100);
        wrapper.css({'margin-bottom':'0','padding-bottom':'0'});
        main_content.css({'height':'100%'});
        $('.page-content #map').css('height', $(window).height());
      } else {
        $(this).addClass('fullscreen');
        header.fadeIn(300);
        footer.fadeIn(300);
        wrapper.css({'margin-bottom':'-60px','padding-bottom':'60px'});
        main_content.css({'height':'100%'});
        $('.page-content #map').css('height', resetDefault);
      }
    });
  }
  // handleSearchSP
  var handleSearchSP = function(){
    if ($(window).width() < 870) {
      $('.js-search-sp').off('click')
      $('.js-search-sp').on('click', function(e){
        e.preventDefault();
        if($('.form-search-top').is(':visible')){
          $('.form-search-top').fadeOut(250);
        }
        else{
          $('.form-search-top').slideDown(200);
        }
      });
    }
  }

  // Handle sidebar menu
  var handleSidebarMenu = function() {
    jQuery('.js-page-sidebar').on('click', 'li > a', function(e) {
      if ($(this).next().hasClass('sub-menu') == false) {
        if ($('.btn-navbar').hasClass('collapsed') == false) {
          $('.btn-navbar').click();
        }
        return;
      }

      if ($(this).next().hasClass('sub-menu always-open')) {
        return;
      }
      var iscurrent = $(this).parent().hasClass('active');
      var parent = $(this).parent().parent();
      var the = $(this);
      var menu = $('.js-page-sidebar-menu');
      var sub = $(this).next();

      var slideSpeed = menu.data("slide-speed") ? parseInt(menu.data("slide-speed")) : 200;

      parent.children('li.is-open').children('a').children('.arrow').removeClass('is-open');
      parent.children('li.is-open').children('.sub-menu:not(.always-open)').slideUp(200);
      parent.children('li.is-open').removeClass('is-open');

      var slideOffeset = -200;

      if (sub.is(":visible")) {
        $('.arrow', $(this)).removeClass("is-open");
        $(this).parent().removeClass("is-open");
        sub.slideUp(slideSpeed);
      } else {
        $('.arrow', $(this)).addClass("is-open");
        $(this).parent().addClass("is-open");
        sub.slideDown(slideSpeed);
      }

      e.preventDefault();
    });
  };

  // Handle Scrollbar
  function handleScrollbar() {
    $(".tbody-scroll").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
    $(".road-panel .road-body").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
    $(".js-storm-scroll").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
    $(".sub-menu-scroll").mCustomScrollbar({
      theme: "minimal-dark",
      advanced: {
        updateOnBrowserResize: true,
        updateOnContentResize: true
      }
    });
  };

  // Handle OnResize
  var handleOnResizeScrollbar = function() {
    $(window).resize(function() {
      handleScrollbar();
    }).load(function() {
      handleScrollbar();
    });
  };

  // Handle Height Element
  var handleHeightElement = function() {
    var hgtWindow = $(window).height();
    var hgtHeader = $('.header').height();
    var hgtFooter = $('.footer').outerHeight();
    var distanceTop = hgtHeader + hgtFooter;
    var rest = hgtWindow - distanceTop + 'px';
    $('.page-sidebar').css('height', rest);
    $('#scroll-content').css('height', rest);
    $('.page-content .iframe-map').css('height', rest);
    $('.page-content #map').css('height', rest);
  };

  // only top
  var handleOnlyTop = function() {
    var topFlg = $('body').hasClass('format-top');
    if (topFlg) {
      $(window).resize(function() {
        handleHeightElement();
      }).load(function() {
        handleHeightElement();
      });
    }
  };

  function handleImageFile(input) {
    if (input.files && input.files[0]) {
      var reader = new FileReader();
      reader.onload = function(e) {
        $('#avatar-logo').attr('src', e.target.result);
        $('#avatar-logo').hide();
        $('#avatar-logo').fadeIn(550);
      }
      reader.readAsDataURL(input.files[0]);
    }
  }

  // Handle RangeSlider
  function handleRangeSlider() {
    if($('.js-range-slider').length){
      var min = +moment().format("X");
      var max = +moment().add(7, 'days').format("X");
      var from = +moment().subtract(1, "hours").format("X");
      var step = 4500;
      var $range2 = $('.js-range-slider');
      var instance2;
      $range2.ionRangeSlider({
        type: "single",
        min: min,
        max: max,
        from: from, 
        step: step,
        grid: true,
        force_edges: true,
        prettify: function (num) {
            var m = moment(num, "X").locale("vi");
            return m.format("Do ddd, HH:mm");
        },
        onStart: function (data) {
          console.log("onStart");
        },
        onChange: function (data) {
          console.log("onChange");
        },
        onFinish: function (data) {
          console.log("onFinish");
        },
        onUpdate: function (data) {
          console.log("onUpdate");
        }
      });
      instance2 = $range2.data("ionRangeSlider");
      function update(data) {
        instance2.update(data);
      }
      var updateRange = function(direction) {
        from += step * direction;
        if (from < min) {
            from = min;
        } else if (from > max) {
            from = max;
        }
        update({
            from: from
        });
      };
      var playTimer;
      function play() {
        playTimer = setTimeout(function(){
          if ( from == max ) {
            pause();
          } else {
            updateRange(1);
            play();
          }
        }, 250 ); // Timer
      }

      function pause() {
        clearTimeout(playTimer);
      }

      $('.time-ctrl').on('click', function(e){
        if(!$(this).hasClass('pause')){
          $(this).addClass('pause');
          play();
        }
        else{
          $(this).removeClass('pause');
          pause();
        }
        e.preventDefault();
      });
    }
  }
  // Function callback
  handleToolTip();
  handleFullscreen();
  handleSearchSP();
  handleSidebarMenu();
  handleScrollbar();
  handleOnResizeScrollbar();
  handleOnlyTop();
  handleRangeSlider();
  
  // Change image input file
  $("#logo-name").change(function() {
    handleImageFile(this);
  });
  // Event Click
  // action left
  $('.control-left .action-system .action-item').each(function(){
    $(this).find('a').on('click', function(e){
      e.preventDefault();
      var attrHref = $(this).attr('href');

      if(!$(this).hasClass('active')){
        $('.control-left .action-system .action-item a').removeClass('active');
        $(this).addClass('active');
        $('.portlet-pos-left').addClass('portlet-expend-left');
        $(attrHref).removeClass('portlet-expend-left');
      }
      else{
        $(this).removeClass('active');
        $('.portlet-pos-left').addClass('portlet-expend-left');
        $(attrHref).addClass('portlet-expend-left');
      }
    });
  });
  // action right
  $('.control-right .action-system .action-item').each(function(){
    $(this).find('a').on('click', function(e){
      e.preventDefault();
      var attrHref = $(this).attr('href');

      if(!$(this).hasClass('active')){
        $('.control-right .action-system .action-item a').removeClass('active');
        $(this).addClass('active');
        $('.portlet-pos-right').addClass('portlet-expend-right');
        $(attrHref).removeClass('portlet-expend-right');
      }
      else{
        $(this).removeClass('active');
        $('.portlet-pos-right').addClass('portlet-expend-right');
        $(attrHref).addClass('portlet-expend-right');
      }
    });
  });
  // close portlet
  $('.portlet-close-left').on('click', function(e){
    e.preventDefault();
    $('.control-left .action-system .action-item a').removeClass('active');
    $(this).parents().find('.portlet-box').addClass('portlet-expend-left');
  });
  $('.portlet-close-right').on('click', function(e){
    e.preventDefault();
    $('.control-right .action-system .action-item a').removeClass('active');
    $(this).parents().find('.portlet-box').addClass('portlet-expend-right');
  });
  // close alert
  $('.panel-alert-close').on('click', function(e){
    e.preventDefault();
    $('.panel-alert').fadeOut(500);
  });
  // Action loading popup login, registry
  $('#form-login').submit(function(e){
      $('.modal-login .login-inner').addClass('loading');
      function popLoading(){
        $('.modal-login .login-inner').removeClass('loading');
      }
      setTimeout(function() {
        popLoading();
      }, 2500);
      //$('#form-login').submit();
      e.preventDefault();
  });
  $('#form-registry').submit(function(e){
      $('.modal-login .login-inner').addClass('loading');
      function popLoading(){
        $('.modal-login .login-inner').removeClass('loading');
      }
      setTimeout(function() {
        popLoading();
      }, 2500);
      //$('#form-registry').submit();
      e.preventDefault();
  });
  // Function resize mobile
  var timer = false;
  $(window).resize(function(){
      if (timer !== false) {
          clearTimeout(timer);
      }
      timer = setTimeout(function() {
          handleSearchSP();
      }, 200);
  });

});

```
**Xử lý loading**
```javascript
// Action loading popup login, registry
$('#form-login').submit(function(e){
    $('.modal-login .login-inner').addClass('loading');
    function popLoading(){
      $('.modal-login .login-inner').removeClass('loading');
    }
    setTimeout(function() {
      popLoading();
    }, 2500);
    //$('#form-login').submit();
    e.preventDefault();
});
```

```javascript
//create AutoComplete UI component
$("#search-top").kendoAutoComplete({
    dataSource: data,
    filter: "startswith",
    separator: ", "
}).keypress(function(e) {
  if (event.keyCode === 13) {
    $('.page-content').addClass('loading');
    function doneLoading(){
      $('.page-content').removeClass('loading');
    }
    setTimeout(function() {
      doneLoading();
    }, 2500);
    return false;
    //$(this).closest('form').trigger('submit');
  }
});
```
**Xử lý ionRangeSlider play/pause**

**5. **
- Text.

>JavaScript Code:
```javascript

```

**6. **
- Text.

>JavaScript Code:
```javascript

```

**7. **
- Text.

>JavaScript Code:
```javascript

```

**8. **
- Text.

>JavaScript Code:
```javascript

```

**9. **
- Text.

>JavaScript Code:
```javascript

```

**10. **
- Text.

>JavaScript Code:
```javascript

```

**11. **
- Text.

>JavaScript Code:
```javascript

```

**12. **
- Text.

>JavaScript Code:
```javascript

```

**13. **
- Text.

>JavaScript Code:
```javascript

```

**14. **
- Text.

>JavaScript Code:
```javascript

```

**15. **
- Text.

>JavaScript Code:
```javascript

```

**16. **
- Text.

>JavaScript Code:
```javascript

```

**17. **
- Text.

>JavaScript Code:
```javascript

```

**18. **
- Text.

>JavaScript Code:
```javascript

```
