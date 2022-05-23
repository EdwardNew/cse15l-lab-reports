# JUnit Testing on MarkdownParser
![](https://www.educative.io/cdn-cgi/image/f=auto,fit=cover,w=600/v2api/collection/4753235730497536/5693417237512192/image/5700019675987968)
<br/>

This week we will be testing 3 `markdown` code snippets using our own implementaion of `markdownParser` and another group's implementation of `markdownParser`. We will be using JUnit testing to test whether these 2 implementations perform as expected.

## Source Code
Here are the links to the two Github Repositories containing the markdownParser implementations we will be testing:
- My implementation: [https://github.com/EdwardNew/markdown-parser](https://github.com/EdwardNew/markdown-parser)
- The other group's implementation: [https://github.com/AlexVazquez19/markdown-parser-echidnas](https://github.com/AlexVazquez19/markdown-parser-echidnas)


## Tests
Here are the 3 `markdown` code snippets we will be testing:

1. ```
    `[a link`](url.com)

    [another link](`google.com)`

    [`cod[e`](google.com)

    [`code]`](ucsd.edu)

    ```
2. ```
    [a [nested link](a.com)](b.com)

    [a nested parenthesized url](a.com(()))

    [some escaped \[ brackets \]](example.com)

    ```
3. ```
    [this title text is really long and takes up more than 
    one line

    and has some line breaks](
        https://www.twitter.com
    )

    [this title text is really long and takes up more than 
    one line](
    https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
    )


    [this link doesn't have a closing parenthesis](github.com

    And there's still some more text after that.

    [this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



    )

    And then there's more text
    ```

## What We Should Expect
1. Expected output: ``[`google.com, google.com, ucsd.edu]``
    ![](..\images\labReport4\snippet1Expected.jpg)
2. Expected output: `[a.com, a.com(()), exmaple.com]`
    ![](..\images\labReport4\snippet2Expected.jpg)
3. Expected output: `[https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule]`
    ![](..\images\labReport4\snippet3Expected.jpg)
    *Although the VS Code's preview shows `https://www.twitter.com` and
    `https://cse.ucsd.edu/` as links, I do not beleive they are actually considered
    links by markdown. I think it might be VS Code's preview taking some initiative
    to render https links as links regardless of markdown rules.*

## The JUnit Tests
1. ![](..\images\labReport4\snippet1Test.jpg)
2. ![](..\images\labReport4\snippet2Test.jpg)
3. ![](..\images\labReport4\snippet3Test.jpg)

## Test Results of My Implementation
1. Failed
    ![](..\images\labReport4\snippet1MyResult.jpg)
2. Failed
    ![](..\images\labReport4\snippet2MyResult.jpg)
3. Failed
    ![](..\images\labReport4\snippet3MyResult.jpg)

## Test Results of The Other Group's Implementation
1. Failed
    ![](..\images\labReport4\snippet1OtherResult.jpg)
2. Failed
    ![](..\images\labReport4\snippet2OtherResult.jpg)
3. Failed
    ![](..\images\labReport4\snippet3OtherResult.jpg)

## Questions
- Do you think there is a small (<10 lines) code change that will make your
program work for snippet 1 and all related cases that use inline code with 
backticks? If yes, describe the code change. If not, describe why it would be
a more involved change.

    **First of all, I think there's another bug in my code that is adding onto this
    current issue, but I think the bug can be fixed by simply checking that the
    index before the open parentheses is a close bracket rather than checking
    that the index after the close bracket is an open parentheses. As for the
    issue of inline backticks, I think the solution would be more involved than
    just a 10 line fix because you would have to track pairs of opening and
    closing backticks, check if the current open bracket lies within those
    backticks, and if it did you would have to find the next open bracket,
    check again, and when it is not, you have to make sure that the index of
    the close bracket, and parentheses are greater than the current open bracket.
    On top of that you, would have to do the same exact thing for the close
    bracket.**

- Do you think there is a small (<10 lines) code change that will make your
program work for snippet 2 and all related cases that nest parentheses,
brackets, and escaped brackets? If yes, describe the code change. If not,
describe why it would be a more involved change.

    **Again, I think the bug mentioned previously adds to this test failure, but
    beyond that, I think the solution to this problem is more complex than what
    is doable within 10 lines of code because you would have to track the number
    of successive open parentheses/brackets (let that be n) using some sort of
    counter and then you would find that number of close parentheses/brackets
    that followed. Make that nth close parentheses/bracket the actual close
    parentheses/bracket of the link and add the substring between the opening
    and close parentheses to the list. However, the fix for escaped brackets is
    very simple and doable in 10 lines by just checking that the index before
    every bracket is not `\`.**

- Do you think there is a small (<10 lines) code change that will make your
program work for snippet 3 and all related cases that have newlines in brackets
and parentheses? If yes, describe the code change. If not, describe why it
would be a more involved change.

    **Yes, I think the solution is relatively simple, but may go a little bit
    over 10 lines of code exactly. The solution would be to add a couple if
    statements before adding the link to the list that checked if the substring
    between the brackets contained a `/n` newline character or if the current
    link substring contained more than 2 `/n` newline characters. Finally, we
    would add a line of code that removed all whitespace characters from the link
    substring (something like this: `st.replaceAll("\\s","")`) before adding it
    to the list.**