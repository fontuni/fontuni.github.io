---
layout: post
title: สมมติว่าฟอนต์ไทยแปลงร่างได้
date: 2016/12/19 18:59 +0700
tag: ["svg", "smil", "interpolation", "font", "variable fonts"]
excerpt: "เห็นนักออกแบบฟอนต์หลายสำนักกำลังเห่อความสามารถใหม่ใน OpenType v1.8 คือ Variable Fonts หรือ ฟอนต์แปลงร่างได้ เลยอยากทดลองกับตัวอักษรไทยบ้าง"
---

[![SVG Animation](/images/articles/weight-axis-interpolation.svg)](/images/articles/weight-axis-interpolation.svg)
<small>คลิกที่ภาพเพื่อดาวน์โหลดไฟล์ SVG ตัวอย่างไปดูซอร์สโค้ดได้นะครับ</small>

เห็นนักออกแบบฟอนต์หลายสำนักกำลังเห่อความสามารถใหม่ใน [OpenType v1.8](https://www.microsoft.com/typography/otspec180/) คือ [Variable Fonts](https://medium.com/@tiro/https-medium-com-tiro-introducing-opentype-variable-fonts-12ba6cd2369#.53bttfb4u) หรือ *ฟอนต์แปลงร่างได้* เลยอยากทดลองกับตัวอักษรไทยบ้าง แต่ปัจจุบันยังไม่มีเครื่องมือที่จะทำหรือใช้ความสามารถของฟอนต์แบบนั้นได้อย่างสมบูรณ์ เลยลองใช้ [SVG-SMIL](https://www.w3.org/TR/SVG/animate.html) มาเขียนโค้ดสำหรับทดลองความเป็นไปได้ในเว็บบราวเซอร์ดูก่อน (เห็น [Glyphs 2.4](https://glyphsapp.com/blog/new-features-in-glyphs-2-4) โฆษณาว่าเริ่มรองรับแล้ว และ [FontLab VI](http://blog.fontlab.com/fontlab-vi/fontlab-opentype-variations/) ก็วางแผนจะรองรับเหมือนกัน แต่ผมไม่ได้ใช้ทั้งสองโปรแกรม)

อธิบายแบบสั้นๆ ได้ว่า Variable Font คือ *ฟอนต์ไฟล์เดียวที่สามารถแสดงผลได้หลากหลายรูปแบบ แล้วแต่ว่า "เราจะปรับค่า" ให้มันแสดงผลแบบไหน* ส่วนคำอธิบายอื่นๆ ลองหาอ่านเพิ่มเติมเอาเองในอินเตอร์เน็ต ถ้าต้องการรู้เชิงลึกก็อ่านใน [OpenType Specification](https://www.microsoft.com/typography/otspec/otvaroverview.htm) ไปเลยครับ

ผมอ่านบทความใน [TypeNetwork](https://www.typenetwork.com/brochure/opentype-variable-fonts-moving-right-along/) เห็นเขาใช้ไฟล์ SVG แสดงตัวอย่าง เลยนึกขึ้นได้ว่าปกติผมก็วาดตัวอักษรเป็นไฟล์ SVG ก่อนทำเป็นฟอนต์อยู่แล้ว และ SVG-SMIL ก็แสดงภาพแอนิเมชั่นแบบง่ายๆ ได้ดีด้วย เลยลองเอามาแสดงตัวอย่างให้พอนึกภาพออก ([แต่ IE/EDGE แสดงผลไม่ได้นะฮะ](http://caniuse.com/#feat=svg-smil))

ภาพ SVG ด้านบนคือ การ Interpolate [ฟอนต์ F0nt](/f0nt/) จากน้ำหนักบางสุดไปถึงหนาสุด ในภาษาของ Variable Fonts คือ weight axis แปลว่า *ผมวาดตัวอักษรแค่ 2 น้ำหนัก ส่วนน้ำหนักที่อยู่ระหว่างบางสุดกับหนาสุดให้ซอฟต์แวร์ที่มีความสามารถคำนวณจากค่าตัวแปร* แต่ Variable Fonts ยืดหยุ่นกว่านั้นมาก ไม่ได้จำกัดแค่ **แกนน้ำหนัก** อย่างเดียว ลองดูในบทความของ TypeNetwork ก็ได้ครับว่ามีแกนอะไรที่เป็นไปได้อีกบ้าง เช่น  width axis, contrast axis, xHeight axis หรือแม้แต่ serif axis

เอาไว้เครื่องมือพร้อมกว่านี้คงได้เอาจริงเอาจังกับ  Variable Fonts ในอนาคต

