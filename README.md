# Catch2 Grade Repor for GitHub Actions

This reporter for Catch2 will output Markdown-formatted [Job Summary](https://github.blog/2022-05-09-supercharging-github-actions-with-job-summaries/) Grade Report for GitHub Actions.

Usage is straightforward.

1. Drop the header in the same directory as your `catch.hpp`.
2. In the file where you `#define CATCH_CONFIG_MAIN`, add an include for the header after the catch.hpp `#include`:

   ```c++
   #define CATCH_CONFIG_MAIN
   #include "catch.hpp"
   #include "catch_reporter_github.hpp"
   ```
3. Your `SECTION`s should end with `|XX` where `XX` is the number of points the test case is worth, like:
   
   ```c++
   TEST_CASE("Sample test case", "[graded]")
   {
	   SECTION("Sample Section|5")
   }
   ```
4. When you run your test case executable, you need to run with the command line argument `-r=github` to use this new runner.
5. Sample of what the output looks like is below. If you run locally, it will write a `GradeReport.md`. On GitHub Actions, it will automatically write to the correct file set in the `GITHUB_STEP_SUMMARY` environment variable.

This has only been tested with Catch 2.x using the Ubuntu 22.04 LTS runner on GitHub Actions. It likely will not work with Catch 3 devel branch.

## (Sample) Grade Report
<table>
<thead><tr><td><b>Result</b></td><td><b>Test</b></td><td><b>Points</b></td><td><b>Earned</b></td><td><b>Details</b></td></tr></thead>
<tr><td colspan='5'><b>Graded RLE Compress</b></td></tr>
<tr><td>✅ PASS</td>
<td>Basic positive runs</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Basic negative runs</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Mix of positive and negative runs</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Long positive run</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Long negative run</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Long positive followed by a negative run of size 2</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Long negative followed by postive run of size 2</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Run with 20 zeroes</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>2 positive, 254 negative, 2 positive</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td></td><td><b>Subtotal</b></td><td>18</td><td>18</td><td></td></tr>
<tr><td colspan='5'><b>Graded RLE Decompress</b></td></tr>
<tr><td>✅ PASS</td>
<td>Decompress Basic positive run</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Decompress Multiple positive runs</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Decompress Mix</td>
<td>2</td>
<td>2</td>
<td></td>
</tr>
<tr><td></td><td><b>Subtotal</b></td><td>6</td><td>6</td><td></td></tr>
<tr><td colspan='5'><b>Graded Command line arguments</b></td></tr>
<tr><td>✅ PASS</td>
<td>instructions.txt.rl1</td>
<td>3</td>
<td>3</td>
<td></td>
</tr>
<tr><td></td><td><b>Subtotal</b></td><td>3</td><td>3</td><td></td></tr>
<tr><td colspan='5'><b>Graded File compression</b></td></tr>
<tr><td>✅ PASS</td>
<td>rle.bmp</td>
<td>8</td>
<td>8</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>pic.jpg</td>
<td>8</td>
<td>8</td>
<td></td>
</tr>
<tr><td>✅ PASS</td>
<td>Conquest.ogg</td>
<td>8</td>
<td>8</td>
<td></td>
</tr>
<tr><td></td><td><b>Subtotal</b></td><td>24</td><td>24</td><td></td></tr>
<tr><td colspan='5'><b>Graded File decompression</b></td></tr>
<tr><td>✅ PASS</td>
<td>works.bmp.rl1</td>
<td>8</td>
<td>8</td>
<td></td>
</tr>
<tr><td>❌ FAIL</td>
<td>xkcd.bmp.rl1</td>
<td>8</td>
<td>0</td>
<td><details closed><summary>Failure Info</summary>
<pre>
/Users/Sanjay/pa1-solution/tests/GradedTests.cpp:413: FAILED:
  REQUIRE( result )
with expansion:
  false
</pre></details></td>
</tr>
<tr><td>✅ PASS</td>
<td>logo.png.rl1</td>
<td>8</td>
<td>8</td>
<td></td>
</tr>
<tr><td></td><td><b>Subtotal</b></td><td>24</td><td>16</td><td></td></tr>
<tr><td colspan='2'><b>TOTAL</b></td><td><b>75</b></td><td><b>67</b></th><td></td></tr></table>

## 🚨🚨 Some test cases failed!! 😭😭

You received 67 out of 75 points.

Keep in mind you still need to check for warnings, and there may be additional assignment-specific points.

