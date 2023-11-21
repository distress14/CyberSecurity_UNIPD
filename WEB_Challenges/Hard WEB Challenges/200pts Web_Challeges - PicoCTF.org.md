
## Client-side-again TODO
### Description
```
Can you break into this super secure portal? 
https://jupiter.challenges.picoctf.org/problem/60786/
or http://jupiter.challenges.picoctf.org:60786
```

Here's the HTML source of the main page:
```<html>
<head>
    <title>Secure Login Portal V2.0</title>
</head>
<body background="barbed_wire.jpeg">
    <!-- standard MD5 implementation -->
    <script type="text/javascript" src="md5.js"></script>

    <script type="text/javascript">
    var _0x5a46 = ['f49bf}', '_again_e', 'this', 'Password\x20Verified', 'Incorrect\x20password', 'getElementById', 'value', 'substring', 'picoCTF{', 'not_this'];
    (function(_0x4bd822, _0x2bd6f7) {
        var _0xb4bdb3 = function(_0x1d68f6) {
            while (--_0x1d68f6) {
                _0x4bd822['push'](_0x4bd822['shift']());
            }
        };
        _0xb4bdb3(++_0x2bd6f7);
    }(_0x5a46, 0x1b3));
    var _0x4b5b = function(_0x2d8f05, _0x4b81bb) {
        _0x2d8f05 = _0x2d8f05 - 0x0;
        var _0x4d74cb = _0x5a46[_0x2d8f05];
        return _0x4d74cb;
    };
    function verify() {
        checkpass = document[_0x4b5b('0x0')]('pass')[_0x4b5b('0x1')];
        split = 0x4;
        if (checkpass[_0x4b5b('0x2')](0x0, split * 0x2) == _0x4b5b('0x3')) {
            if (checkpass[_0x4b5b('0x2')](0x7, 0x9) == '{n') {
                if (checkpass[_0x4b5b('0x2')](split * 0x2, split * 0x2 * 0x2) == _0x4b5b('0x4')) {
                    if (checkpass[_0x4b5b('0x2')](0x3, 0x6) == 'oCT') {
                        if (checkpass[_0x4b5b('0x2')](split * 0x3 * 0x2, split * 0x4 * 0x2) == _0x4b5b('0x5')) {
                            if (checkpass['substring'](0x6, 0xb) == 'F{not') {
                                if (checkpass[_0x4b5b('0x2')](split * 0x2 * 0x2, split * 0x3 * 0x2) == _0x4b5b('0x6')) {
                                    if (checkpass[_0x4b5b('0x2')](0xc, 0x10) == _0x4b5b('0x7')) {
                                        alert(_0x4b5b('0x8'));
                                    }
                                }
                            }
                        }
                    }
                }
            }
        } else {
            alert(_0x4b5b('0x9'));
        }
    }
    </script>
    <div style="position:relative; padding:5px;top:50px; left:38%; width:350px; height:140px; background-color:gray">
        <div style="text-align:center">
            <p>New and Improved Login</p>

            <p>Enter valid credentials to proceed</p>
            <form action="index.html" method="post">
                <input type="password" id="pass" size="8"/>
                <br/>
                <input type="submit" value="verify" onclick="verify(); return false;"/>
            </form>
        </div>
    </div>
</body>
</html>

```

I'll concentrate on this part of the code:
```
function verify() {
        checkpass = document[_0x4b5b('0x0')]('pass')[_0x4b5b('0x1')];
        split = 0x4;
        if (checkpass[_0x4b5b('0x2')](0x0, split * 0x2) == _0x4b5b('0x3')) {
            if (checkpass[_0x4b5b('0x2')](0x7, 0x9) == '{n') {
                if (checkpass[_0x4b5b('0x2')](split * 0x2, split * 0x2 * 0x2) == _0x4b5b('0x4')) {
                    if (checkpass[_0x4b5b('0x2')](0x3, 0x6) == 'oCT') {
                        if (checkpass[_0x4b5b('0x2')](split * 0x3 * 0x2, split * 0x4 * 0x2) == _0x4b5b('0x5')) {
                            if (checkpass['substring'](0x6, 0xb) == 'F{not') {
                                if (checkpass[_0x4b5b('0x2')](split * 0x2 * 0x2, split * 0x3 * 0x2) == _0x4b5b('0x6')) {
                                    if (checkpass[_0x4b5b('0x2')](0xc, 0x10) == _0x4b5b('0x7')) {
                                        alert(_0x4b5b('0x8'));
```

The prefix 0x is used in code to indicate that **the number is being written in hex**.

Short digression on "Why are hexadecimal numbers prefixed with 0x?":

**Short story:** The `0` tells the parser it's dealing with a constant (and not an identifier/reserved word). Something is still needed to specify the number base: the `x` is an arbitrary choice.

**Long story:** In the 60's, the prevalent programming number systems were decimal and _octal_ — mainframes had 12, 24 or 36 bits per byte, which is nicely divisible by 3 = log2(8).

The BCPL language used the syntax `8 1234` for octal numbers. When Ken Thompson created B from BCPL, he used the `0` prefix instead. This is great because

1. an integer constant now always consists of a single token,
2. the parser can still tell right away it's got a constant,
3. the parser can immediately tell the base (`0` is the same in both bases),
4. it's mathematically sane (`00005 == 05`), and
5. no precious special characters are needed (as in `#123`).

When C was created from B, the need for hexadecimal numbers arose (the PDP-11 had 16-bit words) and all of the points above were still valid. Since octals were still needed for other machines, `0x` was arbitrarily chosen (`00` was probably ruled out as awkward).

C# is a descendant of C, so it inherits the syntax.

Source: https://stackoverflow.com/questions/2670639/why-are-hexadecimal-numbers-prefixed-with-0x


```
split = 0x4;
        if ((0-8) == ('3'))
            if ((7 - 9) == '{n')
                if (8, 16) == ('4')) {
                    if ((3-6) == 'oCT') {
                        if ((24-32) == ('0x5')) {
                            if ((6-11) == 'F{not') {
                                if ((16-24) == ('0x6')) {
                                    if (12 - 16) == ('0x7')) {
                                        alert(_0x4b5b('0x8'));
```


We also need to check this function:
```
var _0x4b5b = function(_0x2d8f05, _0x4b81bb) {
        _0x2d8f05 = _0x2d8f05 - 0x0;
        var _0x4d74cb = _0x5a46[_0x2d8f05];
        return _0x4d74cb;
    };
```

```
var container = ['f49bf}', '_again_e', 'this', 'Password\x20Verified', 'Incorrect\x20password', 'getElementById', 'value', 'substring', 'picoCTF{', 'not_this'];
```

```
var 19291 = function(2985733, 4948411) {
	2985733 = 2985733 - 0      #It does nothing
	var 5076171 = container[2985733]
}
```
https://medium.com/@starlaurentius/if-you-can-read-it-you-can-break-it-489682dbc3a5

TODO