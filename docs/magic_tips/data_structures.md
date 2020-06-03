# Printing Data Structures

## Output RAF data to a local file

```
""^X^LN,DO{>(:RAF[X],Y)^X N((X:0X)_"^")^/RPT[LN+1^LN,"1"],Y:0X^/RPT[LN,"2"]}
%Z.copy.raf.to.pc.flat(^/RPT,"C:\Users\username\output.txt","","N")
```

$G Styling:

```
""^X^LN,DO{>(:RAF[X],Y)^X N("["_X~(",":32)_"] = ")^/RPT[LN+1^LN,"1"],Y~("^":32)^/RPT[LN,"2"]}
%Z.copy.raf.to.pc.flat(^/RPT,"C:\Users\username\output.txt","","N")
```

You can import the text file into a spreadsheet (using ^ as the delimiter) to separate the subscripts and data for easy viewing.

$G Styling with RAF name and head node:
```
^<<:RAF[segments]>>^RAF,RAF%0~(",":32)^BASE,RAF#0~(" ":49_("$%&*?\/:!"))^PFX
""^X^LN,K(/RPT),IF{[RAF] N(PFX_"["_BASE_"] = ")^/RPT[LN+1^LN,"1"],[RAF]~("^":32)^/RPT[LN,"2"]}
DO{>([RAF,X],Y)^X N(PFX_"["_BASE_","_X~(",":32)_"] = ")^/RPT[LN+1^LN,"1"],Y~("^":32)^/RPT[LN,"2"]}
%Z.copy.raf.to.pc.flat(^/RPT,"C:\Users\billy\output.txt"^/PATH,"","N"),D(30)_"sh_"_{/PATH}^#
```

* Replace `<<:RAF[segments]>>` with the structure you're printing (do not replace the `^`)
* Replace `"C:\Users\billy\output.txt"` with the path to the text file you're writing to


## Print packed data to front end

```
<PACKED DATA>^X
0^CT,IF{E(X#0)'=L(X|0) N("Not packed data.")^#;DO{X IF{U(X)^Y N("Piece",CT:2L,"-",Y:0X)^#},CT+1^CT}}
```

* Broke out into two lines in case the packed data location is a long string

Example:

```
:GXA["2"]^X
0^CT,IF{E(X#0)'=L(X|0) N("Not packed data.")^#;DO{X IF{U(X)^Y N("Piece",CT:2L,"-",Y:0X)^#},CT+1^CT}}
```


## Safely print subscripts to screen

When printing delimited subscript values to screen, append `:0X` to the variable. This will replace the unprintable characters with spaces.

Example:
```
""^CT^X,DO{>*AA[X]^X,N(X:0X)^#,CT+1^CT<50}
```

You can also use translation (`~`). `X~(",":32)` will convert unprintable characters to commas. You can use any character in place of the comma (such as "^").