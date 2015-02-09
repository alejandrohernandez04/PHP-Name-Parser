PHP-Name-Parser
===============

PHP library to split names into their respective components.  Besides detecting first and last names, this library attempts to handle prefixes, suffixes, initials and compound last names like "Von Fange".  It also normalizes prefixes (Mister -> Mr.) and fixes capitalization (JOHN SMITH -> John Smith).

**Usage:**

    include("parser.php");

    $parser = new FullNameParser();
    $parser->parse_name("Mr Anthony R Von Fange III", $nickname = true);

**Results:**

    Array ( 
    	[nickname] => 
        [salutation] => Mr. 
        [fname] => Anthony 
        [initials] => R 
        [lname] => Von Fange 
        [suffix] => III 
    )

**The algorithm:**

We start by splitting the full name into separate words. We then do a dictionary lookup on the first and last words to see if they are a common prefix or suffix. Next, we take the middle portion of the string (everything minus the prefix & suffix) and look at everything except the last word of that string. We then loop through each of those words concatenating them together to make up the first name. While we’re doing that, we watch for any indication of a compound last name. It turns out that almost every compound last name starts with 1 of 15 prefixes (Von, Van, Vere, etc). If we see one of those prefixes, we break out of the first name loop and move on to concatenating the last name. We handle the capitalization issue by checking for camel-case before uppercasing the first letter of each word and lowercasing everything else. I wrote special cases for periods and dashes. We also have a couple other special cases, like ignoring words in parentheses all-together.

Check examples.php for the test suite and examples of how various name formats are parsed. 

**To-do**

* Handle the "Lname, Fname" format
* Separate the parsing of the name from the normalization & capitalization & make those optional.
* Handle any number of words in parenthesis (currently only handles a single word)
* Normalize the formatting of suffixes (PHD -> PhD)
* Add rule to capitalize two letter names w/ no vowels (ex. "JP" but not "Jo")
* Add common name libraries to allow for things like gender detection

**Credits & license:**

* Read more about the inspiration for this [PHP Name Parser](http://www.onlineaspect.com/2009/08/17/splitting-names/) library by [Josh Fraser](http://joshfraser.com)
* Special thanks to [Josh Jones](https://github.com/UberNerdBoy), [Timothy Wood](https://github.com/codearachnid), [Michael Waskosky](https://github.com/waskosky) and [Eric Celeste](https://github.com/efc) for their contributions.  Pull requests are always welcome as long as you don't break the test suite.
* Released under Apache 2.0 license