- Integer 

    (positive and negative)

    - ^[+-]?\d+$
    - ^[+-]?[0-9]+$
    - *Matches: any signed integer*

- **Integer** 

    (positive)

    - ^[0-9]+$
    - *Matches: any positive signed integer*

- **Integer** 

    (negative)

    - ^[-][0-9]+$
    - *Matches: any negative signed integer*

- **Decimal** 

    (positive and negative)

    - ^[-+]?\d+(\.\d+)?$
    - ^[+-]?[0-9]*(?:\.[0-9]*)?$
    - *Matches: 123 | -123.45 | +123.56*

- Decimal 

    (positive)

    - ^[+]?[0-9]*(?:\.[0-9]*)?$
    - *Matches: 123 | 123.45 | +123.56*

- Decimal 

    (negative)

    - ^[-][0-9]*(?:\.[0-9]*)?$
    - *Matches: -123 | -123.45 | -123.56*

- Number 

    (positive and negative)

    - ^[+-]?([0-9]*\.?[0-9]+|[0-9]+\.?[0-9]*)([eE][+-]?[0-9]+)?$
    - *Matches: 23 | -17.e23 | +.23e+2* 

- Natural Number

    - ^[0-9]*[1-9]+$|^[1-9]+[0-9]*$

- Alphabetical

    - [^a-zA-Z]
    - *Matches: ABC | Test | xyz*

- Alphanumeric

    - [^a-zA-Z0-9]
    - ^[a-zA-Z0-9_]*$
    - *Matches: ABC | Test123*

- E-Mail

    - ^([a-zA-Z0-9_\-\.]+)@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.)|(([a-zA-Z0-9\-]+\.)+))([a-zA-Z]{2,4}|[0-9]{1,3})(\]?)$
    - *Matches: AhmedNegm@WindowsLive.com*

- Date

    - ^(((0[1-9]|[12]\d|3[01])\/(0[13578]|1[02])\/((19|[2-9]\d)\d{2}))|((0[1-9]|[12]\d|30)\/(0[13456789]|1[012])\/((19|[2-9]\d)\d{2}))|((0[1-9]|1\d|2[0-8])\/02\/((19|[2-9]\d)\d{2}))|(29\/02\/((1[6-9]|[2-9]\d)(0[48]|[2468][048]|[13579][26])|((16|[2468][048]|[3579][26])00))))|^(0[1-9]|1[012])[- /.](0[1-9]|[12][0-9]|3[01])[- /.](19|20)\d\d+$
    - *Matches: this expression validates a date field in dd/mm/yyyy  and mm/dd/yyyy format*

- **Temperature**

    - ^[-+]?\d*(\.\d+)?( )?(Celsius|C|c|CELSIUS|Fahrenheit|F|f|FAHRENHEIT|Kelvin|K|k|KELVIN)?$
    - *Matches: 34F | 56 Celsius | 22C*

- Egyptian National ID

    - (2|3)[0-9][1-9][0-1][1-9][0-3][1-9](01|02|03|04|11|12|13|14|15|16|17|18|19|21|22|23|24|25|26|27|28|29|31|32|33|34|35|88)\d\d\d\d\d

- Egyptian Mobile Number

    - (201)[0-9]{9}

- Hexadecimal String

    - ^[0-9A-Fa-f]+$
    - *Matches: 062706440644064700200623064306280631*