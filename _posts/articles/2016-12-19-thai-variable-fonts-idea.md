---
layout: post
title: สมมติว่าฟอนต์ไทยแปลงร่างได้
date: 2016/12/19 18:59 +0700
tag: ["svg", "smil", "interpolation", "font", "variable fonts"]
cover:
  path: /images/articles/multiple-axes-explosion.png
  width: 1550
  height: 600
excerpt: "เห็นนักออกแบบฟอนต์หลายสำนักกำลังเห่อความสามารถใหม่ใน OpenType v1.8 คือ Variable Fonts หรือ ฟอนต์แปลงร่างได้ เลยอยากทดลองกับตัวอักษรไทยบ้าง"
---

[![Weight Axis](/images/articles/weight-axis-interpolation.svg)](/images/articles/weight-axis-interpolation.svg)
<small>Fig. 1: Weight Axis (คลิกที่ภาพเพื่อดาวน์โหลดไฟล์ SVG)</small>

เห็นนักออกแบบฟอนต์หลายสำนักกำลังเห่อความสามารถใหม่ใน [OpenType v1.8](https://www.microsoft.com/typography/otspec180/) คือ [Variable Fonts](https://medium.com/@tiro/https-medium-com-tiro-introducing-opentype-variable-fonts-12ba6cd2369#.53bttfb4u) หรือ *ฟอนต์แปลงร่างได้* เลยอยากทดลองกับตัวอักษรไทยบ้าง แต่ปัจจุบันยังไม่มีเครื่องมือที่จะทำหรือใช้ความสามารถของฟอนต์แบบนั้นได้อย่างสมบูรณ์ เลยลองใช้ [SVG-SMIL](https://www.w3.org/TR/SVG/animate.html) มาเขียนโค้ดสำหรับทดลองความเป็นไปได้ในเว็บบราวเซอร์ดูก่อน (เห็น [Glyphs 2.4](https://glyphsapp.com/blog/new-features-in-glyphs-2-4) โฆษณาว่าเริ่มรองรับแล้ว และ [FontLab VI](http://blog.fontlab.com/fontlab-vi/fontlab-opentype-variations/) ก็วางแผนจะรองรับเหมือนกัน แต่ผมไม่ได้ใช้ทั้งสองโปรแกรม)

อธิบายแบบสั้นๆ ได้ว่า Variable Font คือ *ฟอนต์ไฟล์เดียวที่สามารถแสดงผลได้หลากหลายรูปแบบ แล้วแต่ว่า "เราจะปรับค่า" ให้มันแสดงผลแบบไหน* ส่วนคำอธิบายอื่นๆ ลองหาอ่านเพิ่มเติมเอาเองในอินเตอร์เน็ต ถ้าต้องการรู้เชิงลึกก็อ่านใน [OpenType Specification](https://www.microsoft.com/typography/otspec/otvaroverview.htm) ไปเลยครับ

ผมอ่านบทความใน [TypeNetwork](https://www.typenetwork.com/brochure/opentype-variable-fonts-moving-right-along/) เห็นเขาใช้ไฟล์ SVG แสดงตัวอย่าง เลยนึกขึ้นได้ว่าปกติผมก็วาดตัวอักษรเป็นไฟล์ SVG ก่อนทำเป็นฟอนต์อยู่แล้ว และ SVG-SMIL ก็แสดงภาพแอนิเมชั่นแบบง่ายๆ ได้ดีด้วย เลยลองเอามาแสดงตัวอย่างให้พอนึกภาพออก ([แต่ IE/EDGE แสดงผลไม่ได้นะฮะ](http://caniuse.com/#feat=svg-smil))

ภาพ SVG ด้านบนคือ การ Interpolate [ฟอนต์ F0nt](/f0nt/) จากน้ำหนักบางสุดไปถึงหนาสุด ในภาษาของ Variable Fonts คือ weight axis แปลว่า *ผมวาดตัวอักษรแค่ 2 น้ำหนัก ส่วนน้ำหนักที่อยู่ระหว่างบางสุดกับหนาสุดให้ซอฟต์แวร์ที่มีความสามารถคำนวณจากค่าตัวแปร* แต่ Variable Fonts ยืดหยุ่นกว่านั้นมาก ไม่ได้จำกัดแค่ **แกนน้ำหนัก** อย่างเดียว ลองดูในบทความของ TypeNetwork ก็ได้ครับว่ามีแกนอะไรที่เป็นไปได้อีกบ้าง เช่น  width axis, contrast axis, xHeight axis หรือแม้แต่ serif axis

เอาไว้เครื่องมือพร้อมกว่านี้คงได้เอาจริงเอาจังกับ  Variable Fonts ในอนาคต

## เพิ่มเติม (Dec 20 2016)
{: .section-title }

หลังจากทำแค่แกนน้ำหนักอย่างเดียวแล้วมันไม่สะใจ เพื่อให้เห็นภาพว่าแกนอื่นๆ ก็ interpolate ได้ เลยลองเพิ่ม *แกนความกว้าง (width axis)* สำหรับทำฟอนต์แบบ condensed และ *แกนความต่าง (contrast axis)* สำหรับสร้างความรู้สึกโปร่งทึบหรือสะโอดสะองไม่เหมือนกัน ตามภาพ Fig. 2 & 3 เลย

[![Width Axis](/images/articles/width-axis-interpolation.svg)](/images/articles/width-axis-interpolation.svg)
<small>Fig. 2: Width Axis (คลิกที่ภาพเพื่อดาวน์โหลดไฟล์ SVG)</small>

[![Contrast Axis](/images/articles/contrast-axis-interpolation.svg)](/images/articles/contrast-axis-interpolation.svg)
<small>Fig. 3: Contrast Axis (คลิกที่ภาพเพื่อดาวน์โหลดไฟล์ SVG)</small>

และเมื่อรวมทั้ง 3 แกนเข้าด้วยกัน ก็ได้แบบภาพ Fig. 4 ด้านล่างนี้

[![Multiple Axes](/images/articles/multiple-axes-interpolation.svg)](/images/articles/multiple-axes-interpolation.svg)
<small>Fig. 4: Multiple Axes (คลิกที่ภาพเพื่อดาวน์โหลดไฟล์ SVG)</small>

ส่วน Fig. 5 คือ การระเบิดความเป็นไปได้ออกมาดูทีละตัวเลย โดยมีน้ำหนัก 10 ระดับ มีคอนทราสต์ 5 ระดับ และมีความกว้าง 5 ระดับ รวมเป็น 10 x 5 x 5 = 250!

[![Multiple Axes Explosion](/images/articles/multiple-axes-explosion.png)](/images/articles/multiple-axes-explosion.svg)
<small>Fig. 5: Multiple Axes Explosion (คลิกที่ภาพเพื่อดาวน์โหลดไฟล์ SVG)</small>

คงไม่มีใครบ้าทำฟอนต์ 250 ตัวสำหรับตระกูลเดียว แต่สำหรับ Variable Fonts มันไม่ได้จำกัดแค่ 250 ตัว! เพราะมีความเป็นไปได้ไม่รู้จบ โดยวาดมาสเตอร์ไม่กี่แบบ นั่นคือเหตุผลที่คนทำฟอนต์เขาตื่นเต้นกันครับ!

