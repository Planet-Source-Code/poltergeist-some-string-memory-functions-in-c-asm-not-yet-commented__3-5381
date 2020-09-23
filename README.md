<div align="center">

## Some String/Memory Functions in C/ASM \(not yet commented\)


</div>

### Description

Some String/Memory Functions in C/ASM (no comments yet) I may submit some comments to when people ask for it. This code is IMO only usefull for who are coding an emulator and need some extra speed, which this code will probably give. Please note that a lot of the ASM code could still be optimized a bit, but that I leave to you ;)
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Poltergeist](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/poltergeist.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/poltergeist-some-string-memory-functions-in-c-asm-not-yet-commented__3-5381/archive/master.zip)





### Source Code

<p><font color="#0000FF">typedef unsigned char</font> BYTE;<br>
<font color="#0000FF">typedef unsigned short</font> WORD;<br>
<font color="#0000FF">typedef unsigned long</font> DWORD;<br>
<br>
DWORD MakeDWORD(WORD hb, WORD lb)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">eax</font>,
WORD PTR hb<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">shl</font> <font color="#0000FF">eax</font>,
8<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">or</font> <font color="#0000FF">eax</font>,
WORD PTR lb<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
BYTE HighByte(DWORD value)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">eax</font>,
wordval<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">shr</font> <font color="#0000FF">eax</font>,
8<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">and</font> <font color="#0000FF">eax</font>,
255<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
BYTE LowByte(DWORD value)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">eax</font>,
wordval<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">and</font> <font color="#0000FF">eax</font>,
255<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
DWORD StrLen(BYTE *src)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">xor</font> <font color="#0000FF">eax</font>,
<font color="#0000FF">eax</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> esi,
src<br>
_nextchar:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">cl</font>,
<font color="#FF0000">[<font color="#0000FF">esi</font>]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> esi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF">eax</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">cl</font>, 0<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jz</font> _exit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jmp</font> _nextchar<br>
_exit:<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
<font color="#0000FF">void</font> StrCopy(BYTE *src, BYTE *dst)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">esi</font>, src<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">edi</font>, dst<br>
_nextchar:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">al</font>, <font color="#FF0000">[<font color="#0000FF">esi</font>]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> esi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[<font color="#0000FF">edi</font>]</font>,
<font color="#0000FF"> al</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> edi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 0<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jz</font> _exit<br>
_exit:<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
<font color="#0000FF">void</font> StrLeft(BYTE *src, BYTE *dst, DWORD len)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">esi</font>, src<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">edi</font>, src<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">ecx</font>, len<br>
_nextchar:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">al</font>, <font color="#FF0000">[<font color="#0000FF">esi</font>]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> esi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[<font color="#0000FF">edi</font>]</font>,
<font color="#0000FF"> al</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> edi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 0<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jz</font> _exit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">dec</font> <font color="#0000FF">ecx</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jz</font> _addnull<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jmp</font> _nextchar<br>
_<font color="#000080">add</font>null:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[<font color="#0000FF">edi</font>]</font>, 0<br>
_exit:<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
<font color="#0000FF">void</font> StrLcase(BYTE *src)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">esi</font>, src<br>
_nextchar:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">al</font>, <font color="#FF0000">[<font color="#0000FF">esi</font>]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 'A'<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jb</font> _writeit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 'Z'<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">ja</font> _writeit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">add</font> <font color="#0000FF">al</font>, 32<br>
_writeit:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[<font color="#0000FF">esi</font>]</font>,
<font color="#0000FF"> al</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> esi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 0<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jne</font> _nextchar<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
<font color="#0000FF">void</font> StrUcase(BYTE *src)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">esi</font>, src<br>
_nextchar:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">al</font>, <font color="#FF0000">[<font color="#0000FF">esi</font>]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 'a'<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jb</font> _writeit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 'z'<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">ja</font> _writeit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">sub</font> <font color="#0000FF">al</font>, 32<br>
_writeit:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[<font color="#0000FF">esi</font>]</font>,
<font color="#0000FF"> al</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> esi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">cmp</font> <font color="#0000FF">al</font>, 0<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jne</font> _nextchar<br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
<br>
<font color="#0000FF">void</font> MemCopy(BYTE *src, BYTE *dst, DWORD len)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">esi</font>, src<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">edi</font>, dst<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">ecx</font>, len<br>
_next:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">al</font>, <font color="#FF0000">[<font color="#0000FF">esi</font>]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> esi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[<font color="#0000FF">edi</font>]</font>,
<font color="#0000FF"> al</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">inc</font> <font color="#0000FF"> edi</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">dec</font> <font color="#0000FF">ecx</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jz</font> _exit<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">jmp</font> _next<br>
_exit:<br>
&nbsp;&nbsp;&nbsp; }<br>
}</p>
<p><font color="#0000FF">void</font> SwapMem(DWORD *mem1, DWORD *mem2)<br>
{<br>
&nbsp;&nbsp;&nbsp; <font color="#0000FF">_asm</font> {<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">esi</font>,
mem1<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">edi</font>,
mem2<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">eax</font>,
<font color="#FF0000">[</font><font color="#0000FF">esi</font><font color="#FF0000">]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#0000FF">ecx</font>,
<font color="#FF0000">[</font><font color="#0000FF">edi</font><font color="#FF0000">]</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[</font><font color="#0000FF">esi</font><font color="#FF0000">]</font>,
<font color="#0000FF">ecx</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <font color="#000080">mov</font> <font color="#FF0000">[</font><font color="#0000FF">edi</font><font color="#FF0000">]</font>,
<font color="#0000FF">eax</font><br>
&nbsp;&nbsp;&nbsp; }<br>
}<br>
</p>

