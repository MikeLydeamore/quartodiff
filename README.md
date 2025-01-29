# quartodiff

A simple wrapper around git and latexdiff for Quarto Latex documents.

## Installation

Download the `quartodiff` shell script [here](https://raw.githubusercontent.com/MikeLydeamore/quartodiff/refs/heads/main/quartodiff) and place it somewhere on your path.

You will also need `latexmk` on your path, and it's relevant dependencies. `TinyTeX` can do this but sometimes it goes a bit funky.

## Usage

`quartodiff filename.qmd commit_ref`

This will spam your terminal, and then a file called `diff.pdf` should appear if everything works.

You can use relative indicators (`HEAD~1` etc) or commit hashes. Cross-branch _should_ work but I haven't tested it.

Note that you will be checked out to the HEAD of your current branch.

## Example

`quartodiff quartodiff-demo.qmd 17783d08c1a1aa39daa3dcacfb21de822cf25960` 

Here is the git diff for the two commits used to generate the [`diff.pdf`](diff.pdf) file:

```
diff --git a/demo_function.R b/demo_function.R
index 2cfa7c5..d5095de 100644
--- a/demo_function.R
+++ b/demo_function.R
@@ -1,3 +1,3 @@
 calculate_average <- function(a,b) {
-  (a+b)/2
+  (a+b)/2 * 100
 }
\ No newline at end of file
diff --git a/quartodiff-demo.qmd b/quartodiff-demo.qmd
index 8ff23cf..ccb0996 100644
--- a/quartodiff-demo.qmd
+++ b/quartodiff-demo.qmd
@@ -37,7 +37,7 @@ author:
     affilations:
         - ref: some-tech
 abstract: |
-  This is the abstract. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum augue turpis, dictum non malesuada a, volutpat eget velit. Nam placerat turpis purus, eu tristique ex tincidunt et. Mauris sed augue eget turpis ultrices tincidunt. Sed et mo in in the middle leo porta egestas. Aliquam non laoreet velit. Nunc quis ex vitae eros aliquet auctor nec ac libero. Duis laoreet sapien eu mi luctus, in bibendum leo molestie. Sed hendrerit diam diam, ac dapibus nisl volutpat vitae. Aliquam bibendum varius libero, eu efficitur justo rutrum at. Sed at tempus elit. I have added some text.
+  This is the abstract. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum augue turpis, dictum non malesuada a, volutpat eget velit. Nam placerat turpis purus, eu tristique ex tincidunt et. Mauris sed augue eget turpis ultrices tincidunt. Sed et mo in leo porta egestas. Aliquam non laoreet velit. Nunc quis ex vitae eros aliquet auctor nec ac libero. Duis laoreet sapien eu mi luctus, in bibendum leo molestie. Sed hendrerit diam diam, ac dapibus nisl volutpat vitae. Aliquam bibendum varius libero, eu efficitur justo rutrum at. Sed at tempus elit. I have added some text.
```

You can see the code changes are in an _external_ file. This is because quartodiff checks out the entire repo, recompiles the target qmd, and then checks back out the current branch HEAD.