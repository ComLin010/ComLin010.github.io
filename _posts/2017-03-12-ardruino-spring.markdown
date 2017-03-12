---
layout:     post
title:      "spring_LED灯带项目"
subtitle:   " \"随着舞动，亮起来\""
date:       2017-03-12 13:09:16
author:     "Comlin010"
header-img: "img/post-bg-perfume.jpg"
catalog: true
tags:
    - Arduino
---

>缓慢推行

##spring of lite

3年前？从第一眼看到 [perfume-spring of lite](http://music.163.com/#/mv?id=5224) 的效果就一直很像要做，那种和音乐的完美结合，科技与艺术的相互结合，那种美，真的是让人无比的惊叹。

一开始完全没有头绪，也不知道要从那里入手，在慢慢摸索的过程中，学会了Spring of lite舞蹈，但是那时还不知道树莓派和Arduino，觉得那是个无比艰巨的项目，想过树莓派，想过单片机中间停停歇歇。直到去年我才知道Arduino控制器，买来以后 发现搭配上 **WS2812B** 灯带，能实现我想要的结果，不过最近又遇到了瓶颈。

---

##技术实现

[Adafruit_NeoPixel](learn.adafruit.com/adafruit-neopixel-uberguide/arduino-library) 是一个LED控制库，对WS2812B有很好的兼容性，通过加载 Adafruit_NeoPixel.h库 就能实现对WS2812的控制。

```c
#define PIN 6

// Parameter 1 = number of pixels in strip
// Parameter 2 = pin number (most are valid)
// Parameter 3 = pixel type flags, add together as needed:
//   NEO_KHZ800  800 KHz bitstream (most NeoPixel products w/WS2812 LEDs)
//   NEO_KHZ400  400 KHz (classic 'v1' (not v2) FLORA pixels, WS2811 drivers)
//   NEO_GRB     Pixels are wired for GRB bitstream (most NeoPixel products)
//   NEO_RGB     Pixels are wired for RGB bitstream (v1 FLORA pixels, not v2)
Adafruit_NeoPixel strip = Adafruit_NeoPixel(60, PIN, NEO_GRB + NEO_KHZ800);
```
第一个参数是灯珠数量，要根据实际的数量填写。
**PS：假若是两条灯带串联在一起则是两条灯带灯珠的总和。**

第二个参数是定义针脚。

第三个是颜色和灯珠的频率,可以根据上面代码注释选择自己灯带对于的颜色编码和频率。

初始化完成后 我们要对灯带进行启动。

```c
void setup() {
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
}
```

设置颜色，然后对灯珠进行设定

```c
uint32_t c;
 c = strip.Color(255, 255, 255);
 //设定为白色
 strip.setPixelColor(0, c);
 //对第一个灯珠进行设定
 strip.show()；
 //灯带显示
```
***注意：setPixelColor()后要使用strip.show()不然灯带不会显示***

