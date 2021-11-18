# 接口说明<a name="ZH-CN_TOPIC_0000001119076262"></a>

**表 1**  内存调测模块接口

<a name="table1415203765610"></a>
<table><thead align="left"><tr id="row134151837125611"><th class="cellrowborder" valign="top" width="12.821282128212822%" id="mcps1.2.4.1.1"><p id="p16415637105612"><a name="p16415637105612"></a><a name="p16415637105612"></a>功能分类</p>
</th>
<th class="cellrowborder" valign="top" width="29.832983298329836%" id="mcps1.2.4.1.2"><p id="p11415163718562"><a name="p11415163718562"></a><a name="p11415163718562"></a>接口名</p>
</th>
<th class="cellrowborder" valign="top" width="57.34573457345735%" id="mcps1.2.4.1.3"><p id="p1641533755612"><a name="p1641533755612"></a><a name="p1641533755612"></a>描述</p>
</th>
</tr>
</thead>
<tbody><tr id="row12171174434013"><td class="cellrowborder" rowspan="4" valign="top" width="12.821282128212822%" headers="mcps1.2.4.1.1 "><p id="p989011256471"><a name="p989011256471"></a><a name="p989011256471"></a>内存调测功能</p>
</td>
<td class="cellrowborder" valign="top" width="29.832983298329836%" headers="mcps1.2.4.1.2 "><p id="p15630114884017"><a name="p15630114884017"></a><a name="p15630114884017"></a>mem_check_init</p>
</td>
<td class="cellrowborder" valign="top" width="57.34573457345735%" headers="mcps1.2.4.1.3 "><p id="p4171244164013"><a name="p4171244164013"></a><a name="p4171244164013"></a>初始化内存检测模块。</p>
</td>
</tr>
<tr id="row17223043124018"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1730695210400"><a name="p1730695210400"></a><a name="p1730695210400"></a>watch_mem</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p202242431404"><a name="p202242431404"></a><a name="p202242431404"></a>获取线程级堆内存使用信息。</p>
</td>
</tr>
<tr id="row536885134010"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p236819594010"><a name="p236819594010"></a><a name="p236819594010"></a>check_leak</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p736918564019"><a name="p736918564019"></a><a name="p736918564019"></a>检查是否有堆内存泄漏。</p>
</td>
</tr>
<tr id="row11567448194112"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p0568204814115"><a name="p0568204814115"></a><a name="p0568204814115"></a>check_heap_integrity</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p05681348204114"><a name="p05681348204114"></a><a name="p05681348204114"></a>检查堆内存的完整性。</p>
</td>
</tr>
<tr id="row1141513373562"><td class="cellrowborder" rowspan="3" valign="top" width="12.821282128212822%" headers="mcps1.2.4.1.1 "><p id="p16235102710486"><a name="p16235102710486"></a><a name="p16235102710486"></a>调用栈回溯功能</p>
</td>
<td class="cellrowborder" valign="top" width="29.832983298329836%" headers="mcps1.2.4.1.2 "><p id="p17765212416"><a name="p17765212416"></a><a name="p17765212416"></a>backtrace</p>
</td>
<td class="cellrowborder" valign="top" width="57.34573457345735%" headers="mcps1.2.4.1.3 "><p id="p1972971913115"><a name="p1972971913115"></a><a name="p1972971913115"></a>获取调用栈地址信息。</p>
</td>
</tr>
<tr id="row18483936115014"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p14833367501"><a name="p14833367501"></a><a name="p14833367501"></a>backtrace_symbols</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p174842362505"><a name="p174842362505"></a><a name="p174842362505"></a>根据地址信息获取符号信息。</p>
</td>
</tr>
<tr id="row101737479509"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p21741147125016"><a name="p21741147125016"></a><a name="p21741147125016"></a>print_trace</p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><p id="p15174184755019"><a name="p15174184755019"></a><a name="p15174184755019"></a>输出函数调用栈信息。</p>
</td>
</tr>
</tbody>
</table>

