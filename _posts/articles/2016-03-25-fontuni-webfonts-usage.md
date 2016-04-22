---
layout: post
title: วิธีใช้งานเว็บฟอนต์ของฟอนต์อยู่นี่ โดยไม่ต้องดาวน์โหลด
author: สังศิต ไสววรรณ
date: 2016/03/25 06:12 +0700
tag: ["css","webfont"]
excerpt: "ตั้งใจจะเขียนบอกนักพัฒนาเว็บทั้งหลายไว้นานแล้วว่า “คุณสามารถทดลองใช้งานฟอนต์เกือบทุกตัวของฟอนต์อยู่นี่ได้โดยไม่ต้องดาวน์โหลดครับ”"
---

<style>@import url(/boon/css/boon-all.css)</style>

**คำเตือนก่อนอ่าน:** บทความนี้ใช้ฟอนต์ได้เละเทะมากทีเดียว!

ตั้งใจจะเขียนบอกนักพัฒนาเว็บทั้งหลายไว้นานแล้วว่า “**คุณสามารถทดลองใช้งานฟอนต์เกือบทุกตัวของฟอนต์อยู่นี่ได้โดยไม่ต้องดาวน์โหลดครับ**” เพียงแค่เพิ่ม stylesheet กับ class ใน HTML ก็พอ วิธีการก็คล้ายๆ กับที่เราใช้ Google Fonts API นั่นแหละครับ (แต่ยังไม่มีวิธีเลือกใช้ฟอนต์แบบซับซ้อนเหมือนเขา) เช่น ถ้าต้องการใช้ [ฟอนต์บุญ](/boon/) ก็เรียก stylesheet ดังนี้

~~~html
<link rel="stylesheet" href="https://fontuni.com/boon/css/boon-all.css">
~~~

ถ้าคุณคุ้นกับ CSS และดูในไฟล์ [boon-all.css](/boon/css/boon-all.css) จะเห็นว่าผมเขียน `@font-face` ไว้สำหรับฟอนต์ทั้งตระกูลแล้ว พร้อมระบุน้ำหนักกับสไตล์ของฟอนต์ และมี class สำหรับฟอนต์แต่ละตัวแยกไว้ให้ด้วย เช่น `.boon-400`, `.boon-400i` เป็นต้น (ใครใช้ SASS ก็ดูซอร์สสั้นๆ ได้ในไฟล์  [boon-all.scss](/boon/css/boon-all.scss) )

ตัวอย่างแบบสุดโต่ง วิธีใช้งาน **ฟอนต์เวร** ในเว็บไซต์อื่นโดยไม่ต้องดาวน์โหลดฟอนต์และไม่ต้องเขียน CSS คือ [หน้าปล่อยฟอนต์เวรใน f0nt.com](//www.f0nt.com/release/vain/) ซึ่งผมมีสิทธิเพิ่มได้แค่เนื้อหาที่เป็น HTML แต่ต้องการอิมพอร์ตฟอนต์เวรเพื่อแสดงวิธีเซ็นเซอร์ของมัน

<p class="vain-mon" style="background:#333; color:#eee; padding:1em;">
<style scoped>@import url(/vain/css/vain-all.css)</style>
ข้อความนี้ไม่ต้องการให้คุณอ่าน เพราะผมอิมพอร์ตฟอนต์เวรมาใช้ ด้วย `vain-mon` class
</p>

~~~html
<p class="vain-mon">
<style scoped>@import url(https://fontuni.com/vain/css/vain-all.css)</style>
...
</p>
~~~

ส่วนตัวอย่างการใช้งานหลายฟอนต์ในคราวเดียวกัน ก็เช่น

<p style="background:#333; color:#eee; padding:1em;">
<style scoped>@import url(/boonbaan/css/boonbaan-all.css)</style>
<style scoped>@import url(/boontook/css/boontook-all.css)</style>
<span class="boonbaan-700i">ข้อความนี้อิมพอร์ตฟอนต์บุญบ้านตัวเอนมาใช้ ด้วย boonbaan-700i class</span>
<span class="boon-300">ข้อความนี้อิมพอร์ตฟอนต์บุญตัวบางมาใช้ ด้วย boon-300 class</span>
<span class="boontook">ข้อความนี้อิมพอร์ตฟอนต์บุญถึกตัวตรงมาใช้ ด้วย boontook class</span>
<span class="boon-700i">(กรุณาอย่าใช้ฟอนต์มั่วซั่วแบบนี้ เพราะมันเลอะเทอะรุงรัง!)</span>
</p>

เหตุผลที่ผมเขียน stylesheet ไว้สำหรับฟอนต์ทุกตระกูลที่พร้อมเผยแพร่ ก็เพื่อใช้งานในเว็บไซต์ตัวเองเป็นหลัก ให้มันแสดงผลเว็บฟอนต์ในแต่ละหน้าโปรเจ็คต์แตกต่างกันไป (ส่วนมากเป็นตัวพาดหัว) แล้วที่เขียนบอกไว้ตรงนี้ก็เพราะมันอาจมีประโยชน์กับนักพัฒนาเว็บคนอื่นด้วยครับ

และผมก็ไม่ได้ใจดีแจกแบนด์วิดธ์ฟรีด้วยตัวเองแต่อย่างใด เพราะทุกอย่างในฟอนต์อยู่นี่อยู่ใน [GitHub](https://github.com/) ทั้งหมด! [แค่แยกแต่ละโปรเจ็คต์เป็น submodule](https://github.com/fontuni/fontuni.github.io) แล้วใช้ [GitHub Pages](https://pages.github.com/) (หรือ [Jekyll](https://jekyllrb.com/)) แปลงเป็นเว็บไซต์เท่านั้นเอง แปลว่าวิธีการนี้จะใช้ไม่ได้ก็ต่อเมื่อ GitHub ล่ม ซึ่งคงไม่บ่อย (หรือ [CloudFlare](https://www.cloudflare.com/) ล่ม เพราะผมใช้ระบบ CDN cache ของเขาอยู่)

### ไฟล์ CSS ที่สามารถอิมพอร์ตไปใช้ได้ตอนนี้ คือ
{: .section-title }

- ฟอนต์บุญ: `https://fontuni.com/boon/css/boon-all.css`
- ฟอนต์บุญบ้าน: `https://fontuni.com/boonbaan/css/boonbaan-all.css`
- ฟอนต์บุญถึก: `https://fontuni.com/bootook/css/boontook-all.css`
- ฟอนต์บุญจด: `https://fontuni.com/boonjot/css/boonjot-all.css`
- ฟอนต์เวร: `https://fontuni.com/vain/css/vain-all.css`

**คำเตือนก่อนจบ:**

- CSS ของฟอนต์อยู่นี่ยังไม่นิ่ง และไม่รองรับ IE8 ลงไปนะครับ (ไม่อยากให้ใครใช้บราวเซอร์โบราณ เลยไม่มีไฟล์ `eot` ให้!)
- วิธีการที่ว่ามายังไม่เหมาะกับการใช้งานจริงจัง แต่เหมาะกับขั้นเริ่มพัฒนาเว็บไซต์โดยไม่ต้องเสียเวลาดาวน์โหลดฟอนต์
- และอย่าใช้วิธีอิมพอร์ต CSS แบบนี้กับเว็บไซต์อื่นที่เขาไม่อนุญาตล่ะ!

ในอนาคตก็อยากทำเป็น API ให้เป็นเรื่องเป็นราวกับเขาเหมือนกัน จะได้ไม่ต้องรอ Google Fonts! (แต่ตอนนี้ผมอยากทำฟอนต์อย่างเดียวมากกว่า) ใครมีไอเดียจะเสนอหรืออยากช่วยเรื่องเว็บฟอนต์ก็คุยกันได้นะครับ [ถ้าคุณใช้ GitHub ก็เปิด issue ได้](https://github.com/fontuni/fontuni.github.io/issues) คุยกันใน Twitter, Facebook หรือส่งอีเมลมาก็ได้ แล้วแต่สะดวก
