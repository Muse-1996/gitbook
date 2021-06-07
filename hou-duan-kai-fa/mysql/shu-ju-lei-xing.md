# 数据类型

### 数值类型

| 类型 | 大小 | 范围（有符号） | 范围（无符号） | 用途 |
| :--- | :--- | :--- | :--- | :--- |
| TINYINT | 1 byte | \(-128，127\) | \(0，255\) | 小整数值 |
| SMALLINT | 2 bytes | \(-32 768，32 767\) | \(0，65 535\) | 大整数值 |
| MEDIUMINT | 3 bytes | \(-8 388 608，8 388 607\) | \(0，16 777 215\) | 大整数值 |
| INT或INTEGER | 4 bytes | \(-2 147 483 648，2 147 483 647\) | \(0，4 294 967 295\) | 大整数值 |
| BIGINT | 8 bytes | \(-9,223,372,036,854,775,808，9 223 372 036 854 775 807\) | \(0，18 446 744 073 709 551 615\) | 极大整数值 |
| FLOAT | 4 bytes | \(-3.402 823 466 E+38，-1.175 494 351 E-38\)，0，\(1.175 494 351 E-38，3.402 823 466 351 E+38\) | 0，\(1.175 494 351 E-38，3.402 823 466 E+38\) | 单精度 浮点数值 |
| DOUBLE | 8 bytes | \(-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308\)，0，\(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308\) | 0，\(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308\) | 双精度 浮点数值 |
| DECIMAL | 对DECIMAL\(M,D\) ，如果M&gt;D，为M+2否则为D+2 | 依赖于M和D的值 | 依赖于M和D的值 | 小数值 |

### 日期和时间类型

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5927;&#x5C0F;
        <br />( bytes)</th>
      <th style="text-align:left">&#x8303;&#x56F4;</th>
      <th style="text-align:left">&#x683C;&#x5F0F;</th>
      <th style="text-align:left">&#x7528;&#x9014;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">DATE</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">1000-01-01/9999-12-31</td>
      <td style="text-align:left">YYYY-MM-DD</td>
      <td style="text-align:left">&#x65E5;&#x671F;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">TIME</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">&apos;-838:59:59&apos;/&apos;838:59:59&apos;</td>
      <td style="text-align:left">HH:MM:SS</td>
      <td style="text-align:left">&#x65F6;&#x95F4;&#x503C;&#x6216;&#x6301;&#x7EED;&#x65F6;&#x95F4;</td>
    </tr>
    <tr>
      <td style="text-align:left">YEAR</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">1901/2155</td>
      <td style="text-align:left">YYYY</td>
      <td style="text-align:left">&#x5E74;&#x4EFD;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">8</td>
      <td style="text-align:left">1000-01-01 00:00:00/9999-12-31 23:59:59</td>
      <td style="text-align:left">YYYY-MM-DD HH:MM:SS</td>
      <td style="text-align:left">&#x6DF7;&#x5408;&#x65E5;&#x671F;&#x548C;&#x65F6;&#x95F4;&#x503C;</td>
    </tr>
    <tr>
      <td style="text-align:left">TIMESTAMP</td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">
        <p>1970-01-01 00:00:00/2038</p>
        <p>&#x7ED3;&#x675F;&#x65F6;&#x95F4;&#x662F;&#x7B2C; <b>2147483647</b> &#x79D2;&#xFF0C;&#x5317;&#x4EAC;&#x65F6;&#x95F4; <b>2038-1-19 11:14:07</b>&#xFF0C;&#x683C;&#x6797;&#x5C3C;&#x6CBB;&#x65F6;&#x95F4;
          2038&#x5E74;1&#x6708;19&#x65E5; &#x51CC;&#x6668; 03:14:07</p>
      </td>
      <td style="text-align:left">YYYYMMDD HHMMSS</td>
      <td style="text-align:left">&#x6DF7;&#x5408;&#x65E5;&#x671F;&#x548C;&#x65F6;&#x95F4;&#x503C;&#xFF0C;&#x65F6;&#x95F4;&#x6233;</td>
    </tr>
  </tbody>
</table>

### 字符串类型

| 类型 | 大小 | 用途 |
| :--- | :--- | :--- |
| CHAR | 0-255 bytes | 定长字符串 |
| VARCHAR | 0-65535 bytes | 变长字符串 |
| TINYBLOB | 0-255 bytes | 不超过 255 个字符的二进制字符串 |
| TINYTEXT | 0-255 bytes | 短文本字符串 |
| BLOB | 0-65 535 bytes | 二进制形式的长文本数据 |
| TEXT | 0-65 535 bytes | 长文本数据 |
| MEDIUMBLOB | 0-16 777 215 bytes | 二进制形式的中等长度文本数据 |
| MEDIUMTEXT | 0-16 777 215 bytes | 中等长度文本数据 |
| LONGBLOB | 0-4 294 967 295 bytes | 二进制形式的极大文本数据 |
| LONGTEXT | 0-4 294 967 295 bytes | 极大文本数据 |

