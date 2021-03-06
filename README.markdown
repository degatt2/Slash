Slash
=====

Slash is a **simple**, **extensible** markup language for styling NSAttributedStrings. The language is similar in appearance to HTML, however the meaning of each tag is user-defined.

In iOS 6, displaying attributed strings became much easier, however programatically creating them is still horrible. In fact, adding them to your application any way other than interface builder still requires messing with NSRanges and font attributes.


Usage
-----
The first paragraph of this readme might be expressed in Slash using the markup:

````html
<h1>Slash</h1>
Slash is a <strong>simple</strong>, <strong>extensible</strong> markup language 
that simplifies the creation of NSAttributedStrings. The language is similar in 
appearance to HTML, however the meaning of each tag is user-defined.
````

We can create a new NSAttributedString from this markup with:

````objective-c    
NSAttributedString *myAttributedString = [SLSMarkupParser attributedStringWithMarkup:markup error:NULL];
````

The resulting string will be formatted much as if you'd dropped the equivalent HTML into a browser.

On OS X and iOS 6.0 onwards, Slash provides the following tags:

* h1
* h2
* h3
* h4
* h5
* h6
* emph
* strong

To customize the appearance of these tags, define additional tags, or use a completely different set of tags, pass in a dictionary defining an attributes dictionary for each tag.

 ```objective-c
NSDictionary *style = @{
    @"$default" : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue" size:14]},
    @"strong"   : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Bold" size:14]},
    @"emph"     : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Italic" size:14]},
    @"h1"       : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Medium" size:48]},
    @"h2"       : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Medium" size:36]},
    @"h3"       : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Medium" size:32]},
    @"h4"       : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Medium" size:24]},
    @"h5"       : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Medium" size:18]},
    @"h6"       : @{NSFontAttributeName  : [UILabel fontWithName:@"HelveticaNeue-Medium" size:16]}
};

NSAttributedString *myAttributedString = [SLSMarkupParser   attributedStringWithMarkup:markup style:style error:NULL];
````

When a piece of text belongs to multiple elements, the attributes applied will be the union of each tag's dictionary, with the innermost elements' attributes taking priority. For a list of attributes supported by the Cocoa/Cocoa Touch text rendering system, see the documentation for [iOS][1] or [OSX][2].

Note that the linked attributes are only supported on iOS from 6.0 onwards.

[1]: http://developer.apple.com/library/ios/#Documentation/UIKit/Reference/NSAttributedString_UIKit_Additions/Reference/Reference.html
[2]: https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/AttributedStrings/Articles/standardAttributes.html#//apple_ref/doc/uid/TP40004903-SW2


Installation
------------

    git clone https://github.com/chrisdevereux/Slash.git

* Add Slash.xcodeproj as a child project
* Add Slash-iOS or Slash-OSX as a project dependency
* Link with libSlash-iOS.a or libSlash-OSX.a


Requirements
------------

iOS 4.3 or OS X 10.5 (64 bit) upwards.

Attributed string handling is limited prior to iOS 6, and certain features of Slash require iOS 6. Be sure to check the header documentation if you are targeting earlier. You will also need to use a custom view (such as [NIAttributedLabel][3]) to display the strings, and the format required of the attribute dictionaries in your style will be defined by that view.

[3]: http://docs.nimbuskit.info/NimbusAttributedLabel.html


License
-------

Slash is released under an MIT license.


Contact
-------
Chris Devereux

devereux.chris@gmail.com
