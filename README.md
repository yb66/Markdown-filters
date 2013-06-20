## Markdown Filters ##

I use these, you can use them too!

NOTE! This library is going through a *lot* of changes right now. Use directly at your peril! Feel free to take what you need from the source though, if you feel there may be something useful there.

### LinkReffing ###

If you'd don't want your links inline and would prefer to have them at the bottom of the document, then you can use this:
    
    The UtterFAIL website [UtterFAIL!](http://utterfail.info) is good. My blog [My blog](http://iainbarnett.me.uk) is also good.

and it will produce this:

    The UtterFAIL website[&#8304;](#0 "Jump to reference") is good. My blog[&sup1;](#1 "Jump to reference") is also good.
    <a name="0"></a>&#91;0&#93; [http://utterfail.info](http://utterfail.info "http://utterfail.info") UtterFAIL!
    
    
    <a name="1"></a>&#91;1&#93; [http://iainbarnett.me.uk](http://iainbarnett.me.uk "http://iainbarnett.me.uk") My blog

### InsideBlock ###

Sometimes it'd be useful to wrap some markdown with HTML, for example:

    <div id="notes">
    
    * first
    * second
    * third
    
    </div>

If you put this through a markdown parser the markdown won't get parsed:

    require 'rdiscount'
    s = "<div id="notes">\n\n* first\n* second\n* third\n\n</div>\n"
    puts RDiscount.new(s).to_html

This is the output:

    <div id="notes">
    
    * first
    * second
    * third
    
    </div>

My brilliant idea to get around this is to add an HTML attribute of `markdown='1'` to HTML tags that you want the markdown parser to look inside:

    <div id="notes" markdown='1'>
    
    * first
    * second
    * third
    
    </div>

Trying this with `InsideBlock` gives:

    puts MarkdownFilters::InsideBlock.run s

    <div id="notes">
    <ul>
    <li>first</li>
    <li>second</li>
    <li>third</li>
    </ul>
    
    </div>

To use it as a filter:

    require 'markdownfilters/base'
    
    class MyFilter < MarkdownFilters::Base
      register MarkdownFilters::InsideBlock
    end
    
    myf = MyFilter.new(s)
    # => "<div id="notes" markdown='1'>\n\n* first\n* second\n* third\n\n</div>\n"
    
    puts myf.filter

Gives:

    <div id="notes">
    <ul>
    <li>first</li>
    <li>second</li>
    <li>third</li>
    </ul>
    
    </div>


### Licence ###

Copyright (c) 2012 Iain Barnett

MIT Licence

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


i.e. be good
