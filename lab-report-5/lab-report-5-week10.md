# Debugging Different Implementations

![](..\images\labReport5\vimLogo.jpg)

This week we will be comparing two implementations of MarkdownParser against a very large set of test files. We will attept to see how the outputs of the implementations differ, which implementation produces the correct output (if any), and how we can improve each implementation so that they produce the correct output.

# Differences
In this report, we will be looking at two test files in particular which produced different outputs from the two implementations. We were able to find that these tests produced different outputs by using the `vimdiff` command to compare how the output files produced after running `bash script.sh > results.txt` differ with each other.

![](..\images\labReport5\vimdiff.jpg)

We will be focusing on the test files `41.md` and `577.md` in particular.

## Links to test files:
41.md: [https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/41.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/41.md)

577.md: [https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/567.md?plain=1](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/567.md?plain=1)

# Test file 41.md
For this test file, both my own, and the given implementations of MarkdownParse produces an incorrect output.

### Expected Output: `[url]`
![](..\images\labReport5\41Expected.jpg)

### Output of my implementation: `[url "tit"]`
![](..\images\labReport5\own41Output.jpg)

### What's wrong and how do we fix it?
The problem with my own implementation of MarkdownParse is that I do not account for the possibility of adding titles to the links in the input files.

To fix this, we can add an if statement to check if the potential link we are about to add to the output list contains a set of quotation marks.

### The code to be fixed:
![](..\images\labReport5\own41Solution.jpg)

### Output of given implementation: `[]`
![](..\images\labReport5\given41Output.jpg)

The problem with the given implementation of MarkdownParse is that it also does not account for the possibility of a title for a link. However, it does not add the link to the list entirely because it checks if a potential link contains a space in it. This is normally invalid, but when a title is added, spaces are allowed within the parentheses.

To fix this, we can also implement an if statement that checks for a set of quotation marks within the brackets.

### The code to be fixed:
![](..\images\labReport5\given41Solution.jpg)


# Test file 577.md
For this test file, my implementation of MarkdownParse produces the correct output and the provided implementation produces an incorrect output.

### Expected Output: `[]`
The output for this test file based on VS Code preview should be `[]` because we do not consider images as links.

![](..\images\labReport5\577Expected.jpg)

### Output of my implementation: `[]`
![](..\images\labReport5\own577Output.jpg)

### Output of given implementation: `[train.jpg]`
![](..\images\labReport5\given577Output.jpg)

### What's wrong and how do we fix it?
The problem with the given implementation of MarkdownParse is that it does not check for the possibility of image links, which are differentiated by a `!` in front of the first open bracket.

This makes for a relatively easy fix because all you need to do is add an if statement checking for an `!` at the index 1 before the index of the `[` of a potential link.

### The code to be fixed:
![](..\images\labReport5\577Solution.jpg)

# Thank you!

Well, that's it. This marks the end of this lab report and the end of the last lab report for this class. Thanks for following me on my journey through this class, and hopefully you learned a thing or two along the way too!