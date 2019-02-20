[//]: # (#sed)
1. `-n`: don't output
   - `sed -n s/in/out/ someFile`
   - `sed -n s/in/out/p someFile` silent except lines that matches `in`
   - `sed -n s/in/out/pg someFile`
2. Anything after `s` can be delimiter other than `/`
3. `&` equals the matched pattern
-  `sed -n s/in/&/ someFile` substitude content `in` with itself
4. `-i`: in place
5. `I` or `i`: case insensitive, ==Not support in MacOS X==
6. delete line`d`: `sed '/in/d' someFile`
7. `;`: seperate multiple commands `sed 's/after/burner/g;/place/d' sed.md`, first substitude then delete
8. `-f`: read your `///` things from file instead of typing it