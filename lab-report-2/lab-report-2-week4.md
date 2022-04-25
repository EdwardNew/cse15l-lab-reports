# Incremental Development and Debugging

![](https://media.geeksforgeeks.org/wp-content/uploads/20190902105053/Debugging-Tips-To-Get-Better-At-It.png)
<br/>

### Below we will look at 3 bugs that were found in the MarkdownParse file and how those bugs were fixed.
<br/>

## Bug 1
* Solution:
![](..\images\labReport2\bug1.jpg)
* [Failure-inducing input](test-file1.md)
* Symptom:
![](..\images\labReport2\bug1symptom.jpg)
* Explaination: <br/>
In this case, the failure-inducing input was a file that contained no links in it. This caused the symptom of a StringIndexOutOfBoundsException to be outputted. The symptom is what tells the programmer that there is a bug in their code.
<br/>

## Bug 2
* Solution:
![](..\images\labReport2\bug2.jpg)
* [Failure-inducing input](test-file2.md)
* Symptom:
![](..\images\labReport2\bug2symptom.jpg)
* Explaination: <br/>
In this case, the failure-inducing input was a file that had an image in it. This cause the symptom of an extra unexpected link to be printed in the links ArrayList. This symptom tells the programmer that there is some sort of bug in the code that still treats image links as links.
<br/>

## Bug 3
* Solution:
![](..\images\labReport2\bug3.jpg)
* [Failure-inducing input](test-file3.md)
* Symptom:
![](..\images\labReport2\bug3symptom.jpg)
* Explaination: <br/>
Finally, in this case, the failure-inducing input was a file that had a link at the very beginning of the file. This caused a similar symptom from a previous failure inducing input of an output of a StringIndexOutOfBoundsException to surface. This symptom tells the programmer that there is a bug that happens only when a file contains a link at the beginning of the file.
<br/>

## Conclusion
Hopefully after reading through these examples, you have a better understanding of how bugs, the failure-inducing inputs that trigger the bugs, and the symptoms that result from bugs are related.