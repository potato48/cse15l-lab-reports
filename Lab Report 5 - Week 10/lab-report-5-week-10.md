# Lab Report 5

## Finding tests with different results
I used the ``diff`` program and manually looked through the resulting file for tests that had different results.


## Test 1

Test File: ``500.md``

The provided implmentation was correct. The expected output is ``[#fragment, http://example.com#fragment, http://example.com?foo=3#frag]``

My implementation was incorrect as it gave ``[]`` whereas
the provided implmentation gave the expected result.

The bug is that one of the conditions before a link is added in my implementation requires the URL inside the parentheses to contain ``.html`` or ``https`` which doesn't cover all possible links. That results in the URLs of all three links in ``500.md`` being skipped.


```
  if (markdown.substring(openParen, closeParen).contains(".html") ||
            markdown.substring(openParen, closeParen).contains("https")) {
        toReturn.add(markdown.substring(openParen + 1, closeParen));
        }
```
https://github.com/potato48/markdown-parse/blob/5024aaee57b2692e363d32a6ccc8b06b264abf2f/MarkdownParse.java#L45

<br>

---

<br>

## Test 2

Test File: ``14.md``

The expected output is ``[]``

The provided implmentation gave ``[/foo]`` whereas my implmentation gave the expected result ``[]``

The bug with the provided implementation is that it doesn't check the character that comes before the open bracket of a supposed link. As a result, it interprets line 3 of ``14.md`` as a valid link. The same issue would also arise if a markdown file had an image as the syntax is the same format as line 3 but with an ``!`` instead of ``\``

Line 3: ``\[not a link](/foo)``

There isn't a specific line or lines of code that need to be fixed as an entirely separate check would be needed to ensure any character before the link doesn't make the link itself invalid.

e.g. an additional check being added some time before a link is added to ``toReturn``
```
String potentialLink = markdown.substring(openParen + 1, closeParen).trim();
if(potentialLink.indexOf(" ") == -1 && potentialLink.indexOf("\n") == -1) {
    toReturn.add(potentialLink);
    currentIndex = closeParen + 1;
}
```

https://github.com/ucsd-cse15l-w22/markdown-parse/blob/1f7485854d92deb69c1bf8290c267fee27371d17/MarkdownParse.java#L75







