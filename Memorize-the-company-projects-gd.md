#### I. Memorize the company project GD
---

**1. ABC projects**
- JS.

>JavaScript Code:
```javascript
//CMS-8341用JS
/* ==================================================

 * gd-1.4.8.min.js
 *
 * Version: 1.4.8
 * Last Modified: 2014/2/21
 * Library&Plugin: jQuery 1.7.1, jQuery.cookie, jQuery.attrrep

----------------------------------------------------

 * $.gd.Uri
 
 * yuga.js
 * http://kyosuke.jp/yugajs/
 
================================================== */

/**
 * Cookie plugin
 *
 * Copyright (c) 2006 Klaus Hartl (stilbuero.de)
 * Dual licensed under the MIT and GPL licenses:
 * http://www.opensource.org/licenses/mit-license.php
 * http://www.gnu.org/licenses/gpl.html
 *
 */
jQuery.cookie=function(a,b,c){if(typeof b!='undefined'){c=c||{};if(b===null){b='';c.expires=-1}var d='';if(c.expires&&(typeof c.expires=='number'||c.expires.toUTCString)){var e;if(typeof c.expires=='number'){e=new Date();e.setTime(e.getTime()+(c.expires*24*60*60*1000))}else{e=c.expires}d='; expires='+e.toUTCString()}var f=c.path?'; path='+(c.path):'';var g=c.domain?'; domain='+(c.domain):'';var h=c.secure?'; secure':'';document.cookie=[a,'=',encodeURIComponent(b),d,f,g,h].join('')}else{var j=null;if(document.cookie&&document.cookie!=''){var k=document.cookie.split(';');for(var i=0;i<k.length;i++){var l=jQuery.trim(k[i]);if(l.substring(0,a.length+1)==(a+'=')){j=decodeURIComponent(l.substring(a.length+1));break}}}return j}};

/* ==================================================

 * jquery.attrrep.js
 *
 * Copyright (c) Global design, Inc. All rights reserved.
 * http://www.glode.co.jp/ 
 * Version: 1.0.0
 * Last Modified: 2009/4/4
 * Library&Plugin: jQuery 1.3.2
 
================================================== */
;(function($){var e='attrRep';$.fn[e]=function(a){var c=$.extend({name:'src',ret:'',rep:''},a);var b=this;var d=$(b).attr(c.name);if(d){$(this).data('before',d);d=d.replace(c.ret,c.rep);$(this).data('after',d);$(b).attr(c.name,d)}return this}})(jQuery);

//gd.js
(function($) {
    $.gd = {
        Uri: function(d) {
            var e = this;
            var d = htmlescape(d || window.location.href);
            this.originalPath = d;
            this.absolutePath = (function() {
                var a = $('<a>').attr({
                    href: d
                });
                var b = $('<span>').append(a);
                var c = b.find('a').get(0).href;
                return c
            })();
            var f = {
                'schema': 2,
                'username': 5,
                'password': 6,
                'host': 7,
                'path': 9,
                'query': 10,
                'fragment': 11
            };
            var r = /^((\w+):)?(\/\/)?((\w+):?(\w+)?@)?([^\/\?:]+):?(\d+)?(\/?[^\?#]+)?\??([^#]+)?#?(\w*)/.exec(this.absolutePath);
            for (var g in f) {
                this[g] = r[f[g]]
            }
            this.directory = r[9] ? r[9].replace(/[^\/]+$/, '') : '';
            var h = '';
            if (r[1]) h += r[1];
            if (r[3]) h += r[3];
            if (r[7]) h += r[7];
            if (r[9]) h += r[9];
            h = (h).replace(/\/index\..+$/, '');
            this.trimPath = (h).replace(/\/$/, '');
            this.querys = {};
            if (this.query) {
                var j = e.query.split('&');
                j.sort();
                for (var i = 0, l = j.length; i < l; i++) {
                    var k = j[i].split('=');
                    if (k.length == 2) {
                        e.querys[k[0]] = k[1]
                    } else if (k.length == 1) {
                        e.querys[k[0]] = ''
                    }
                }
                this.query = j.join('&')
            }

            function htmlescape(a) {
                var b = [
                    [/</g, '#%3C'],
                    [/>/g, '#%3E'],
                    [/"/g, '#%22'],
                    [/'/g, '#%27']
                ];
                for (var i in b) {
                    a = a.replace(b[i][0], b[i][1])
                }
                return a
            }
        },
        wrapperWidth: function(b) {
            var c = $.extend({
                area: '#tmp_wrapper',
                defWidth: '100%',
                maxWidth: 1280,
                minWidth: 780
            }, b);
            var d = c.maxWidth + 'px',
                minWidthSet = c.minWidth + 'px',
                minWidthStyle = $(c.area).css('minWidth'),
                scrollWidth = 20;

            function resiser() {
                if (!minWidthStyle) {
                    var a = $('body').width();
                    if (a > c.maxWidth + scrollWidth) {
                        $(c.area).width(d)
                    } else if (a < c.minWidth) {
                        $(c.area).width(minWidthSet)
                    } else {
                        $(c.area).width(c.defWidth)
                    }
                }
            }
            resiser();
            $(window).resize(function() {
                resiser()
            })
        },
        searchText: function(e) {
            var c = $.extend({
                area: '#tmp_query',
                keyword: 'キーワードを入力'
            }, e);
            var f = $(c.area).each(function() {
                var b = $(this);
                b.on('focus.searchText', function() {
                    if (b.val() == c.keyword) {
                        b.val('')
                    }
                }).on('blur.searchText', function() {
                    if (b.val() == '') {
                        b.val(c.keyword)
                    }
                });
                if (b.val() == '') {
                    b.val(c.keyword)
                }
                var d = b.parents('form').each(function() {
                    var a = $(this);
                    a.on('submit.searchText', function() {
                        if (b.val() == c.keyword) {
                            b.val('')
                        }
                    })
                })
            })
        },
        googleSearchImage: function(b) {
            var c = $.extend({
                area: '#tmp_query',
                backgroundProperty: '#FFFFFF url(/shared/images/gsearch/google_custom_search_watermark.gif) no-repeat left center',
                focusBackgroundProperty: '#FFFFFF'
            }, b);
            $(c.area).each(function() {
                var a = $(this);
                a.css({
                    background: c.backgroundProperty
                }).on('focus.googleSearchImage', function() {
                    $(this).css({
                        background: c.focusBackgroundProperty
                    })
                }).on('blur.googleSearchImage', function() {
                    if ($(this).val() == '') {
                        $(this).css({
                            background: c.backgroundProperty
                        })
                    }
                });
                if (a.val() != '') {
                    a.css({
                        background: c.focusBackgroundProperty
                    })
                }
            })
        },
        textSize: function(d) {
            var c = $.extend({
                area: '#tmp_header',
                cookieName: 'text_size',
                cookieValue: {
                    expires: 365,
                    path: '/'
                },
                sizeUpClass: '.text_size_up',
                sizeDownClass: '.text_size_down',
                sizeNormalClass: '.text_size_normal',
                size: '75%,87.5%,130%,175%',
                defaultSize: '87.5%',
                smallStr: 'これ以上文字を縮小することはできません。',
                bigStr: 'これ以上文字を拡大することはできません。'
            }, d);
            var e = $(c.area),
                cookieData = $.cookie(c.cookieName),
                body = $(document.body);
            if (!cookieData) {
                body.css('fontSize', c.defaultSize)
            } else {
                body.css('fontSize', cookieData)
            }
            var f = c.size.split(',');
            var g = f[0];
            var h = f[f.length - 1];
            var j = body.get(0).style.fontSize;
            var k = numSelect(f, j);
            e.find(c.sizeUpClass).each(function() {
                $(this).on('click.textSize', function() {
                    if (j == h) {
                        alert(c.bigStr)
                    } else {
                        body.css('fontSize', f[k + 1]);
                        j = body.get(0).style.fontSize;
                        k++
                    }
                    $.cookie(c.cookieName, j, c.cookieValue);
                    return false
                })
            });
            e.find(c.sizeDownClass).each(function() {
                $(this).on('click.textSize', function() {
                    if (j == g) {
                        alert(c.smallStr)
                    } else {
                        body.css('fontSize', f[k - 1]);
                        j = body.get(0).style.fontSize;
                        k--
                    }
                    $.cookie(c.cookieName, j, c.cookieValue);
                    return false
                })
            });
            e.find(c.sizeNormalClass).each(function() {
                $(this).on('click.textSize', function() {
                    body.css('fontSize', c.defaultSize);
                    j = body.get(0).style.fontSize;
                    k = numSelect(f, j);
                    $.cookie(c.cookieName, j, c.cookieValue);
                    return false
                })
            });

            function numSelect(a, b) {
                for (var i = 0; i < a.length; i++) {
                    if (b == a[i]) {
                        var c = i;
                        break
                    }
                }
                return c
            }
        },
        changeStyle: function(g) {
            var c = $.extend({
                area: '#tmp_header',
                switchClass: 'changestyle',
                switchChooseClass: 'changestyle_c',
                switchChooseBtn: 'changestyle_c_btn',
                switchChoosedefBtn: 'changestyle_d_btn',
                defaultLinkName: 'default',
                cookieValue: {
                    expires: 365,
                    path: '/'
                }
            }, g);
            var h = $(c.area),
                myCookieName = 'cookies',
                cookieNameList = $.cookie(myCookieName);
            h.find('.' + c.switchClass).each(function() {
                $(this).on('click.changeStyle', function() {
                    var a = $(this).attr('id'),
                        changeLink;
                    if (a.indexOf('_' + c.defaultLinkName) > -1) {
                        var b = a.replace('_' + c.defaultLinkName, '');
                        a = c.defaultLinkName;
                        changeLink = $('link[title=' + a + '][id=' + b + ']')
                    } else {
                        a = a.replace(/^tmp_(.*)/, '$1');
                        changeLink = $('link[title=' + a + ']')
                    }
                    var d = changeLink.attr('class');
                    styleSet(a, d, changeLink);
                    return false
                })
            });
            h.find('.' + c.switchChooseBtn).each(function() {
                $(this).on('click.changeStyle', function() {
                    var a = $(this).attr('name'),
                        checked = h.find('.' + c.switchChooseClass).filter('[name=' + a + ']').filter(':checked'),
                        styleName = checked.attr('value'),
                        changeLink;
                    if (styleName == c.defaultLinkName) {
                        changeLink = $('link[title=' + styleName + '][id=' + a + ']')
                    } else {
                        changeLink = $('link[title=' + styleName + ']')
                    }
                    styleSet(styleName, a, changeLink);
                    return false
                })
            });
            h.find('.' + c.switchChoosedefBtn).on('click.changeStyle', function() {
                var a = c.defaultLinkName,
                    styleGloup = $(this).attr('name'),
                    defaultInput = h.find('.' + c.switchChooseClass).filter('[value=' + c.defaultLinkName + '][name=' + styleGloup + ']');
                if (a == c.defaultLinkName) {
                    changeLink = $('link[title=' + a + '][id=' + styleGloup + ']')
                } else {
                    changeLink = $('link[title=' + a + ']')
                }
                styleSet(a, styleGloup, changeLink);
                defaultInput.attr('checked', true);
                return false
            });

            function styleSet(a, b, d) {
                var e = d.attr('href'),
                    defaultLink = $('#' + b),
                    defaultLinkHref = defaultLink.attr('href'),
                    defaultLinkPath = $.cookie(b);
                if ((defaultLinkPath) == null) {
                    defaultLinkPath = defaultLinkHref + ',' + a;
                    $.cookie(b, defaultLinkPath, c.cookieValue)
                } else {
                    var f = $.cookie(b),
                        allCookies = f.split(','),
                        str;
                    allCookies[1] = a;
                    str = allCookies.join(',');
                    $.cookie(b, str, c.cookieValue)
                }
                if (d.attr('id') == d.attr('class')) {
                    if (!allCookies) return false;
                    defaultLink.attr('href', allCookies[0])
                } else {
                    defaultLink.attr('href', e)
                }
                if (cookieNameList == null) {
                    cookieNameList = b
                } else if (cookieNameList.indexOf(b) == -1) {
                    cookieNameList += (',' + b)
                }
                $.cookie(myCookieName, cookieNameList, c.cookieValue)
            }
        },
        activeLink: function(f) {
            var c = $.extend({
                area: 'body',
                level: 1,
                activeClass: 'active',
                activeThisClass: 'active_this',
                referId: '#tmp_pankuzu',
                query: false
            }, f);
            var g = new $.gd.Uri(String(window.location.href));
            var h = c.query ? [g.query, '?', g.trimPath].join('') : g.trimPath;
            var j = $(c.area);
            var k = j.find('a');
            var l = $(c.referId).find('a:visible').eq(c.level);
            var m = l.length ? l.get(0).getAttribute('href') : '';
            var l = m ? new $.gd.Uri(m) : '';
            var n = c.query ? [l.query, '?', l.trimPath].join('') : l.trimPath;
            k.each(function(i) {
                this.hrefdata = new $.gd.Uri(this.getAttribute('href'));
                var b = this.hrefdata;
                b = c.query ? [b.query, '?', b.trimPath].join('') : b.trimPath;
                var d = $(this).parent();
                if (d.get(0) && d.get(0).tagName == 'SPAN') {
                    d = $(this).parent().parent()
                }
                var e = $(this).parents().filter(j.find('li'));
                if (h == b) {
                    $(this).addClass(c.activeThisClass);
                    d.addClass(c.activeClass);
                    e.each(function(a) {
                        if (e.length - 1 != a) {
                            $(this).addClass(c.activeClass)
                        }
                    })
                }
                if (n == b) {
                    d.addClass(c.activeClass);
                    e.each(function(a) {
                        if (e.length - 1 != a) {
                            $(this).addClass(c.activeClass)
                        }
                    })
                }
            })
        },
        rollover: function(f) {
            var c = $.extend({
                area: 'body',
                onSuffix: '_on.',
                offSuffix: '_off.',
                activeSuffix: '_on.',
                activeClass: 'active'
            }, f);
            $(c.area).each(function() {
                var e = $(this).find('img').filter('[src*="' + c.offSuffix + '"]').each(function() {
                    var a = $(this);
                    var b = a.parents('a');
                    var d = a.attr('src');
                    this.onImg = new Image();
                    this.activeImg = new Image();
                    this.onImg.src = d.replace(c.offSuffix, c.onSuffix);
                    this.activeImg.src = d.replace(c.offSuffix, c.activeSuffix);
                    if (a.parent().parent().hasClass(c.activeClass)) {
                        this.src = this.activeImg.src;
                        return true
                    }
                    a.on('mouseover.rollover', function() {
                        this.src = this.onImg.src
                    }).on('mouseout.rollover', function() {
                        this.src = d
                    });
                    b.on('focus.rollover', function() {
                        a.trigger('mouseover.rollover')
                    }).on('blur.rollover', function() {
                        a.trigger('mouseout.rollover')
                    })
                })
            })
        },
        tab: function(f) {
            var c = $.extend({
                area: 'body',
                type: 'normal',
                easing: 'swing',
                speead: 300,
                naviClass: 'tab_menu',
                activeClass: 'active',
                onSuffix: '_on.',
                offSuffix: '_off.',
                cookie: false,
                cookieValue: {
                    expires: 365,
                    path: '/'
                }
            }, f);
            $(c.area).find('.' + c.naviClass).each(function(i) {
                var e = $(this).find('a[href*="#"], area[href*="#"]').not('a[href="#"], area[href="#"]').filter(function() {
                        this.hrefdata = new $.gd.Uri(this.getAttribute('href'));
                        var a = $('#' + this.hrefdata.fragment);
                        return a.length
                    }),
                    tabBodyList, activeImg = e.find('img[src*="' + c.offSuffix + '"]'),
                    thisURLFragment = new $.gd.Uri().fragment,
                    thisURLFragmentObj = e.filter('[href*="#' + thisURLFragment + '"]'),
                    defaultIdName = new $.gd.Uri(e.filter(':first').attr('href')).fragment,
                    activeMenu = defaultIdName,
                    cookieName = c.naviClass + i,
                    cookieData = $.cookie(cookieName),
                    times = 0;
                e.each(function() {
                    this.hrefdata = new $.gd.Uri(this.getAttribute('href'));
                    var d = '#' + this.hrefdata.fragment;
                    if (tabBodyList) {
                        tabBodyList = tabBodyList.add(d)
                    } else {
                        tabBodyList = $(d)
                    }
                    $(this).off('click.tab').on('click.tab', function() {
                        $.cookie(cookieName, d, c.cookieValue);
                        var a = $(this).closest('.' + c.naviClass);
                        a.removeClass(activeMenu).addClass(this.hrefdata.fragment);
                        activeMenu = this.hrefdata.fragment;
                        e.parent().removeClass(c.activeClass);
                        $(this).parent().addClass(c.activeClass);
                        activeImg.each(function() {
                            $(this).attrRep({
                                name: 'src',
                                ret: c.onSuffix,
                                rep: c.offSuffix
                            })
                        });
                        $(this).find('img[src*="' + c.offSuffix + '"]').each(function() {
                            $(this).attrRep({
                                name: 'src',
                                ret: c.offSuffix,
                                rep: c.onSuffix
                            })
                        });
                        var b;
                        if (times == 0) {
                            b = 'normal';
                            times++
                        } else {
                            b = c.type
                        }
                        switch (b) {
                            case 'normal':
                                tabBodyList.hide();
                                $(d).show();
                                break;
                            case 'fade':
                                tabBodyList.filter(':visible').fadeOut('slow', function() {
                                    $(d).fadeIn('fast')
                                });
                                break;
                            case 'slide':
                                tabBodyList.filter(':visible').animate({
                                    height: '1px'
                                }, c.speed, c.easing, function() {
                                    tabBodyList.filter(':visible').css('height', 'auto');
                                    tabBodyList.filter(':visible').hide();
                                    $(d).slideDown('fast')
                                });
                                break;
                            default:
                                tabBodyList.filter(':visible').hide();
                                $(d).show();
                                break
                        }
                        return false
                    })
                });
                if (thisURLFragment && thisURLFragmentObj.length) {
                    thisURLFragmentObj.trigger('click.tab')
                } else if (c.cookie && $.cookie(cookieName)) {
                    e.filter('[href*=' + $.cookie(cookieName) + ']').trigger('click.tab')
                } else {
                    e.filter(':first').trigger('click.tab')
                }
            })
        },
        switchMenu: function(m) {
            var c = $.extend({
                area: 'body',
                type: 'normal',
                easing: 'swing',
                speead: 300,
                naviClass: 'switch_menu',
                switchClass: 'switch',
                cntClass: 'switch_cnt',
                activeClass: 'active',
                onSuffix: '_on.',
                offSuffix: '_off.',
                onAlt: 'メニューを閉じます',
                offAlt: 'メニューを開きます',
                targetParentLevel: 1
            }, m);
            $(c.area).find('.' + c.naviClass).each(function() {
                var f = $(this);
                var g = f.find('.' + c.activeClass).parent();
                if (g.hasClass(c.cntClass)) {
                    g.addClass(c.activeClass)
                };
                var h = f.find('.' + c.cntClass).each(function() {
                    if ($(this).hasClass(c.activeClass)) {
                        $(this).parent().addClass(c.activeClass);
                        return true
                    } else {
                        $(this).hide()
                    }
                });
                var j = f.find('.' + c.activeClass).not('.' + c.cntClass).each(function() {
                    $(this).find('.' + c.cntClass).eq(0).addClass(c.activeClass).show()
                });
                var k = f.find('.' + c.switchClass).css('cursor', 'pointer').on('click.switchMenu', function() {
                    var a = $(this).parent();
                    for (var i = 0; i < c.targetParentLevel - 1; i++) {
                        a = a.parent()
                    }
                    if (a.get(0) && a.get(0).tagName == 'SPAN') {
                        a = $(this).parent().parent()
                    }
                    var b = a.find('.' + c.cntClass).eq(0),
                        img = $(this).find('img[src*="' + c.offSuffix + '"], img[src*="' + c.onSuffix + '"]'),
                        src = img.attr('src');
                    a.toggleClass(c.activeClass);
                    b.toggleClass(c.activeClass);
                    switch (c.type) {
                        case 'normal':
                            b.toggle();
                            break;
                        case 'slide':
                            b.filter(':visible').animate({
                                height: '1px'
                            }, c.speead, c.easing, function() {
                                b.css('height', 'auto');
                                b.hide()
                            }).end().filter(':hidden').slideDown("fast");
                            break;
                        default:
                            b.toggle();
                            break
                    }
                    changeImg($(this), src, img);
                    return false
                }).find('img[src*="' + c.offSuffix + '"]').each(function() {
                    var a = $(this).attr('src');
                    this.preImg = new Image();
                    this.preImg.src = a.replace(c.offSuffix, c.onSuffix)
                });
                var l = $(this).find('li.' + c.activeClass).each(function() {
                    var a = $(this).find('img[src*="' + c.offSuffix + '"], img[src*="' + c.onSuffix + '"]');
                    var b = a.attr('src');
                    changeImg($(this).find('a').eq(0), b, a)
                });

                function changeImg(a, b, d) {
                    var e = a.parent();
                    for (var i = 0; i < c.targetParentLevel - 1; i++) {
                        e = e.parent()
                    }
                    if (e.get(0) && e.get(0).tagName == 'SPAN') {
                        e = a.parent().parent()
                    }
                    if (b) {
                        if (e.hasClass(c.activeClass)) {
                            b = b.replace(c.offSuffix, c.onSuffix);
                            d.attr('alt', c.onAlt)
                        } else {
                            b = b.replace(c.onSuffix, c.offSuffix);
                            d.attr('alt', c.offAlt)
                        }
                        a.find('img[src*="' + c.offSuffix + '"], img[src*="' + c.onSuffix + '"]').attr('src', b)
                    }
                }
            })
        },
        labelClickable: function(d) {
            if (!$.browser.msie) return;
            var c = $.extend({
                area: 'body'
            }, d);
            $(c.area).find('label:has(img)').each(function() {
                var a = $(this).attr('for');
                var b = $('#' + a);
                $(this).toggle(function() {
                    b.attr('checked', true).select()
                }, function() {
                    if (b.attr('type') == 'radio') return;
                    b.attr('checked', false).select()
                })
            })
        },
        blockSkipExpander: function(b) {
            if (!$.browser.msie) return;
            var c = $.extend({
                area: 'a.skip'
            }, b);
            var d = $(c.area);

            function resiser() {
                var a = document.body.clientWidth;
                d.width(a)
            }
            resiser();
            $(window).resize(function() {
                resiser()
            })
        },
        directoryFlg: function(a) {
            var c = $.extend({
                directory: '/'
            }, a);
            var b = new $.gd.Uri(String(window.location.href));
            var d = b.path.replace(/index\..*/, '');
            var e = false;
            var f = c.directory.split(',');
            for (var i = 0; i < f.length; i++) {
                if (d.search(f[i]) == 0) {
                    e = true;
                    break
                }
            }
            return e
        }
    };
    var o = $.cookie('cookies');
    if (o) {
        var p = o.split(',');
        for (var i = 0; i < p.length; i++) {
            var o = $.cookie(p[i]),
                cookieArray = o.split(','),
                value = cookieArray[1],
                href = $('link[title=' + value + ']').attr('href'),
                target = $('#' + p[i]);
            target.attr('href', href)
        }
    }
})(jQuery);
```

**2. **
- Text.

>JavaScript Code:
```javascript

```

**3. **
- Text.

>JavaScript Code:
```javascript

```

**4. **
- Text.

>JavaScript Code:
```javascript

```

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
