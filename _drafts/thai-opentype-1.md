---
layout: post
title: "โอเพ่นไทป์สำหรับฟอนต์ไทย : ตอนที่ 1 (อุดมคติ)"
author: สังศิต ไสววรรณ
date: 2015/11/02 14:45 +0700
tag: ["opentype"] 
---

<style>@import url(//fontuni.com/vain/css/vain-all.css)</style>

ในอุดมคตินั้นการทำ [ฟีเจอร์โอเพ่นไทป์](https://www.microsoft.com/typography/otspec/featurelist.htm) สำหรับฟอนต์ไทย (และลาว) โดยใช้เฉพาะชุดตัวอักษรไทยเท่าที่ [Unicode ระบุไว้](http://unicode.org/charts/PDF/U0E00.pdf) นั้นซับซ้อนน้อยกว่าวิธีอื่น (แต่ไม่ได้หมายความว่าง่ายกว่า) ที่จำเป็นต้องเพิ่มก็มีแค่พยัญชนะที่ต้องตัดเชิง (ฐ, ญ) แล้วจัดตำแหน่งด้วยฟีเจอร์ `mark` ([Mark Positioning](https://www.microsoft.com/typography/otspec/features_ko.htm#mark)) กับ `mkmk` ([Mark to Mark Positioning](https://www.microsoft.com/typography/otspec/features_ko.htm#mkmk))  ไม่ต้องมีสระบน-ล่างและวรรณยุกต์หลายชุด ในที่นี้ขอพักเรื่องขนาดของสระและวรรณยุกต์ไว้ก่อนนะครับ มาทำความเข้าปัญหาขั้นพื้นฐานกันก่อน (ถ้าสนใจวิธีที่ซับซ้อนกว่านี้ ก็ลองอ่าน [Spec for Thai OpenType Font Creation](http://linux.thai.net/~thep/th-otf/) ที่คุณเทพพิทักษ์ การุญบุญญานันท์ เขียนไว้)

ในทางปฏิบัติ ปัญหาไม่ได้อยู่ที่ตัวฟอนต์แต่อยู่ที่ระบบปฏิบัติการหรือแอพพลิเคชั่นรองรับฟีเจอร์เหล่านี้ได้ไม่เท่ากัน ยกตัวอย่างเช่น Mac OS เพิ่งรองรับ `mark` & `mkmk` ในรุ่น 10.10 และ ถ้าต้องการใช้งาน `mark` & `mkmk` กับฟอนต์ไทยได้สมบูรณ์ในซอฟต์แวร์ของ Adobe ก็ต้องติดตั้งเวอร์ชั่นที่รองรับวิธีเขียนที่ซับซ้อนของภูมิภาคตะวันออกกลางและเอเชียใต้ เป็นต้น (เมื่อก่อนผมเข้าใจผิดว่าซอฟต์แวร์ของ Adobe ไม่มีความสามารถพอที่จะรองรับวิธีเขียนที่ซับซ้อนแบบภาษาไทย แต่จริงๆ มันอยู่ที่ผู้ใช้จะเลือกติดตั้งเวอร์ชั่นที่เหมาะกับภาษาของตัวเองหรือไม่ต่างหาก) ใน Windows ผมไม่ทราบว่าดีหรือแย่แค่ไหน แต่สำหรับ GNU/Linux desktop และเว็บบราวเซอร์ที่มี [HarfBuzz](http://www.freedesktop.org/wiki/Software/HarfBuzz/) (Text Shaper) การทำฟอนต์ไทยและลาวในอุดมคตินั้นสะดวกมาก (Uniscribe ของ Windows กับ HarfBuzz ทำหน้าที่คล้ายกันมาก ผมเลยสันนิษฐานว่า Windows คงรองรับ `mark` & `mkmk` ได้ดีเช่นกัน)
{: .vain-mon}

มาลองเขียนโค้ดโอเพ่นไทป์เพื่อพิสูจน์สมมติฐานนี้กัน!

### ระบุปัญหาสำหรับวิธีเขียนภาษาไทยมาตรฐาน

มาดูปัญหาเบื้องต้นที่ต้องแก้ทีละขั้นสำหรับวิธีเขียนภาษาไทยมาตรฐานกันก่อน (หลังแก้ขั้นนี้ได้แล้วเราจึงจะเจอปัญหาขั้นต่อไป)

เพื่อให้เข้าใจง่ายเวลาเขียนโค้ดโอเพ่นไทป์ ขอกำหนดไว้เป็น class ตามนี้ (ขอข้ามการอธิบาย syntax ถ้าสนใจพื้นฐานก็ลองอ่าน [OpenType CookBook](http://opentypecookbook.com/))

    # Normal (Baseline) Consonants
    @NC = [ uni0E01 uni0E02 uni0E03 uni0E04 uni0E05 uni0E06 uni0E07 uni0E08 uni0E09 uni0E0A uni0E0B uni0E0C uni0E11 uni0E12 uni0E13 uni0E14 uni0E15 uni0E16 uni0E17 uni0E18 uni0E19 uni0E1A uni0E1C uni0E1E uni0E20 uni0E21 uni0E22 uni0E23 uni0E24 uni0E25 uni0E26 uni0E27 uni0E28 uni0E29 uni0E2A uni0E2B uni0E2C uni0E2D uni0E2E uni0E2F uni25CC ];

    # Ascender Consonants (ป, ฝ, & ฟ) 
    @AC = [ uni0E1B uni0E1D uni0E1F ];
    
    # Strict Descender Consonants (ฎ, ฏ)
    @DC = [ uni0E0E uni0E0F ];
    
    # Removable Descender Cnsonants (ญ, ฐ)
    @RC = [ uni0E0D uni0E10 ];
    @RC.rd = [ uni0E0D.rd uni0E10.rd ];

    # Above Vowels/Diacritics
    @AV = [ uni0E31 uni0E34 uni0E35 uni0E36 uni0E37 uni0E47 uni0E4D uni0E4E ];

    # Below Vowels / Diacritics
    @BV = [ uni0E38 uni0E39 uni0E3A ];

    # Tones / Diacritics
    @T = [ uni0E48 uni0E49 uni0E4A uni0E4B uni0E4C ];

- `@NC` = พยัญชนะปกติบนเส้นฐาน ในที่นี้ รวม `uni25CC` (&#x25CC; = Dotted Circle) ไว้ด้วย
- `@AC` = พยัญชนะหางยาวขึ้นด้านบน (ป, ฝ, & ฟ)
- `@DC` = พยัญชนะหางยาวลงด้านล่าง (ฎ, ฏ)
- `@RC` = พยัญชนะที่มีเชิงด้านล่าง (ญ, ฐ)
- `@RC.rd` = พยัญชนะที่ตัดเชิงด้านล่างออก (ไม่มีใน Unicode)
- `@AV` = สระบน + ไม้ไต่คู้ นิคหิต และ ยามักการ
- `@BV` = สระล่าง + พินทุ
- `@T` = วรรณยุกต์ + ทัณฑฆาต (ตำแหน่งเริ่มต้นคือวางไว้สูงเยื้องขวา)

โอเพ่นไทป์จัดฟีเจอร์เป็น 2 กลุ่ม คือ `GSUB` ([Glyph Substitution Table](https://www.microsoft.com/typography/otspec/gsub.htm)) กับ `GPOS` ([Glyph Positioning Table](https://www.microsoft.com/typography/otspec/gpos.htm)) โดยทั่วไปเราจะจัดการ `GSUB` ให้เสร็จก่อน แล้วค่อยยกหน้าที่ให้ `GPOS` จัดการต่อ

#### Thai GSUB

ปัญหาที่เราต้องแก้ด้วยฟีเจอร์ในกลุ่ม `GSUB` คือ

1. ตัดเชิง ฐ, ญ เมื่อมีสระล่าง (เปลี่ยน `@RC` เป็น `@RC.rd` เมื่อตามด้วย `@BV`)
2. เปลี่ยนวรรณยุกต์เป็น นิคหิต+วรรณยุกต์ และเปลี่ยนสระอำเป็นสระอา เมื่อพิมพ์พยัญชนะ + วรรณยุกต์ + สระอำ (เปลี่ยน `@T` เป็น `uni0E4D`+`@T` และเปลี่ยน `uni0E33` เป็น `uni0E32` )

และฟีเจอร์ที่เหมาะสำหรับการแก้ปัญหาเหล่านี้คือ `ccmp` ([Glyph Composition / Decomposition](https://www.microsoft.com/typography/otspec/features_ae.htm#ccmp)) ไม่ใช่ `liga` ([Standard Ligatures](https://www.microsoft.com/typography/otspec/features_ko.htm#liga)) เพราะ Ligature หมายถึงการรวม glyph หลายตัวให้เป็นตัวเดียวกัน ไม่ใช่การสับเปลี่ยน glyph อย่างที่เรากำลังจะทำ โค้ดในส่วน `GSUB` ก็ได้ดังนี้ (สำหรับปัญหาข้อแรก ผมแยกเป็น 2 lookups เพื่อจะใช้ `ThaiRC.rd` กับภาษาบาลี-สันสกฤต ที่จะพูดถึงทีหลัง)

    #
    # GSUB 1. ตัดเชิง
    #

    # Remove descender
    lookup ThaiRC.rd {
      sub @RC by @RC.rd;
    } ThaiRC.rd;
    
    lookup ThaiContextRC.rd {
      sub @RC' lookup ThaiRC.rd @BV;
    } ThaiContextRC.rd;

    #
    # GSUB 2. จัดการวรรณยุกต์กับสระอำ
    #

    # Change Mai Ek to Nighahit + Mai Ek
    lookup Thai0E48.0E4D {
      sub uni0E48 by uni0E4D uni0E48;
    } Thai0E48.0E4D;

    # Change Mai Tho to Nighahit + Mai Tho
    lookup Thai0E49.0E4D {
      sub uni0E49 by uni0E4D uni0E49;
    } Thai0E49.0E4D;

    # Change Mai Tri to Nighahit + Mai Tri
    lookup Thai0E4A.0E4D {
      sub uni0E4A by uni0E4D uni0E4A;
    } Thai0E4A.0E4D;

    # Change Mai Jattawa to Nighahit + Mai Jattawa
    lookup Thai0E4B.0E4D {
      sub uni0E4B by uni0E4D uni0E4B;
    } Thai0E4B.0E4D;

    # Change Sara Am to Sara AA
    lookup Thai0E33.0E32 {
      sub uni0E33 by uni0E32;
    } Thai0E33.0E32;

    # Shorthand for all Thai consonants
    @Cons = [ @NC @AC @DC @RC @RC.rd ];
    
    # Tones & Sara AM contextual substitutions
    lookup ThaiContextTone.0E33 {
      sub @Cons' uni0E48'lookup Thai0E48.0E4D uni0E33'lookup Thai0E33.0E32;
      sub @Cons' uni0E49'lookup Thai0E49.0E4D uni0E33'lookup Thai0E33.0E32;
      sub @Cons' uni0E4A'lookup Thai0E4A.0E4D uni0E33'lookup Thai0E33.0E32;
      sub @Cons' uni0E4B'lookup Thai0E4B.0E4D uni0E33'lookup Thai0E33.0E32;
    } ThaiContextTone.0E33;

    # Apply features
    feature ccmp {
      lookup ThaiContextRC.rd;
      lookup ThaiContextTone.0E33;
    } ccmp;

#### Thai GPOS

1. ดึงวรรณยุกต์ลงมา เมื่อมันตามพยัญชนะปกติที่ไม่มีสระบนคั่น
2. ดึงสระล่างให้ต่ำลง เมื่อมันตามพยัญชนะที่ยาวกว่าเส้นฐาน (ฎ, ฏ)
1. ดึงวรรณยุกต์ลงมาและเลื่อนไปทางซ้าย เมื่อมันตามพยัญชนะหางยาว (ฟ, ป, ฝ) และไม่มีสระบนขั้น


