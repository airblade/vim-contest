# Contest

Contest is a runner for Vimscript tests.  It's the simplest way I have found to write tests using Vim's built-in `assert_*()` functions, run them, and see the results.

I test [vim-gitgutter][], [vim-rooter][], and [vim-localorie][] this way and I like how easy it is to write good tests.


## Example

An example test file (`test_example.vim`) might look like this:

```viml
" If you define a SetUp() function Contest will run it
" before each test function.
function SetUp()
  enew
endfunction

" If you define a TearDown() function Contest will run it
" after each test function.

" Test functions start with "Test_"
function Test_inserting_sets_modified_option()
  ihello
  call assert_true(getbufvar('%', &modified))
endfunction

function Test_addition()
  call assert_equal(3, 1+1)
endfunction
```

Running this with Contest would give:

```
$ ./test

test_example.vim:
inserting sets modified option - ok
addition                       - not ok
                                 ! Test_addition line 1: Expected 3 but got 2
                                 ! function RunTest[6]

2 tests, 0 errors, 1 failure
```

Tests are run in a random order each time to help catch hidden dependencies.

You can focus on specific tests by giving a pattern:

```
$ ./test mod

test_example.vim:
inserting sets modified option - ok

1 test, 0 errors, 0 failures
```


## Installation

1. Make a `test/` directory in your plugin.
2. Copy the files `runner.vim` and `test` to your `test/` directory.
3. Adjust `test` to source your plugin's main file (e.g. plugin/YOUR_PLUGIN.vim).
4. Write your tests in a `test_YOUR_PLUGIN.vim` file.


## Debugging

Use `call Log('stuff')` in your tests to write out any extra information you need.


## Credits

Contest is adapted from Vim's own [Vimscript test runner][runtest].


## Intellectual Property

Copyright 2016 Andrew Stewart. Licenced under the MIT licence.


[vim-gitgutter]: https://github.com/airblade/vim-gitgutter/tree/master/test
[vim-rooter]: https://github.com/airblade/vim-rooter/tree/master/test
[vim-localorie]: https://github.com/airblade/vim-localorie/tree/master/test
[runtest]: https://github.com/vim/vim/blob/master/src/testdir/runtest.vim

