---
layout: post
title: เครื่องตรวจแพนแกรม
author: สังศิต ไสววรรณ
date: 2016/03/29 02:47 +0700
tag: ["poetgram","pangram"] 
---

<style scoped> 
  #thai-pangram { margin-bottom: 10px; } 
  [contenteditable="true"] { padding: 1em; outline: 2px dashed #CCC; } 
  [contenteditable="true"]:hover { outline: 2px dashed #0090D2; } 
</style>

<pre id="thai-pangram" contenteditable="true">กีฬาบังลังก์ ลำดับที่ ๑,๒๓๔,๕๖๗,๘๙๐

๏ จับฅอคนบั่นต้อง	อาญา
ขุดฆ่าโคตรฃัตติยา	ซ่านม้วย
ธรรมฤๅผ่อนรักษา	ใจชั่ว โฉดแฮ
สืบอยู่เต็มศึกด้วย	ฝุ่นฟ้ากีฬา กามฦๅ ฯ
๏ กตัญญูไป่พร้อม	ปฐมฌาน
เกมส๎วัฒน์ปฏิภาณ	ห่อนล้ำ
ทฤษฎีถ่อยๆ สังหาร	เกณฑ์โทษ
โกรธจี๊ดจ๋อยจ่มถ้ำ	อยู่เฝ้า “อตฺตา” ๚ะ๛
</pre>

<div id="result"></div>


<script type="text/javascript">

function count(str,char) {
  var re = new RegExp(char,"gi");
  
  if (str.match(re) != undefined) {
    return str.match(re).length;
  }
  else {
    return 0;
  }
  
}

var str = document.getElementById("thai-pangram").textContent;

var regex = /[\u0e01-\u0e5b]/g;

var element = document.getElementById("result");

var para = document.createElement("p");

if (str.length > 0) {
  var node = document.createTextNode("แพนแกรมนี้ใช้ตัวอักษรไทยทั้งหมด " + count(str,regex) + " ตัว");
  element.appendChild(para);
  
  var list = document.createElement("ul");
  list.setAttribute("id", "charlist");
  element.appendChild(list);
} 
else {
  var node = document.createTextNode("กรุณาพิมพ์แพนแกรมที่ต้องการตรวจสอบ");
  element.appendChild(para);
}

para.appendChild(node);

function printChar(char) {
  var ul = document.getElementById("charlist")
  var li = document.createElement("li");
  ul.appendChild(li);
  
  charNode = document.createTextNode(char + " " + count(str, char) + " ตัว");
  li.appendChild(charNode);
  if (count(str, char) == 0) {
    li.style.color = "red";
  }
}

var thaiChar = [
  "ก", 
  "ข",
  "ฃ",
  "ค",
  "ฅ",
  "ฆ",
  "ง",
  "จ",
  "ฉ",
  "ช",
  "ซ",
  "ฌ",
  "ญ",
  "ฎ",
  "ฏ",
  "ฐ",
  "ฑ",
  "ฒ",
  "ณ",
  "ด",
  "ต",
  "ถ",
  "ท",
  "ธ",
  "น",
  "บ",
  "ป",
  "ผ",
  "ฝ",
  "พ",
  "ฟ",
  "ภ",
  "ม",
  "ย",
  "ร",
  "ฤ",
  "ล",
  "ฦ",
  "ว",
  "ศ",
  "ษ",
  "ส",
  "ห",
  "ฬ",
  "อ",
  "ฮ",
  "ฯ",
  "ะ",
  "ั",
  "า",
  "ำ",
  "ิ",
  "ี",
  "ึ",
  "ื",
  "ุ",
  "ู",
  "ฺ",
  "฿",
  "เ",
  "แ",
  "โ",
  "ใ",
  "ไ",
  "ๅ",
  "็",
  "่",
  "้",
  "๊",
  "๋",
  "์",
  //"ํ",
  "๎",
  "๏",
  "๐",
  "๑",
  "๒",
  "๓",
  "๔",
  "๕",
  "๖",
  "๗",
  "๘",
  "๙",
  "๚",
  "๛"
];



function setChangeListener (div, listener) {

    div.addEventListener("blur", listener);
    div.addEventListener("keyup", listener);
    div.addEventListener("paste", listener);
    div.addEventListener("copy", listener);
    div.addEventListener("cut", listener);
    div.addEventListener("delete", listener);
    div.addEventListener("mouseup", listener);

}

var div = document.getElementById("thai-pangram");

setChangeListener(div, function(event){
  for (var i = 0; i < thaiChar.length; i++){
    printChar(thaiChar[i]);
  }
    console.log(event);
});

</script>
