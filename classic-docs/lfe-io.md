---
layout: docs
---
# LFE Documentation

## I/O Functions

{% highlight text %}
MODULE

        lfe_io

MODULE SUMMARY

        Lisp Flavoured Erlang (LFE) io functions

DESCRIPTION

        This module provides a standard set of io functions for
        LFE. In the following description, many functions have an
        optional parameter IoDevice. If included, it must be the pid
        of a process which handles the IO protocols such as the
        IoDevice returned by file:open/2.

        Two functions in this module are used to generate
        aesthetically attractive representations of abstract forms,
        which are suitable for printing. These functions return
        (possibly deep) lists of characters and generate an error if
        the form is wrong.

DATA TYPES

        chars() = [char() | chars()]
        filesexpr() = {Sexpr,Line}
            This is the format returned by lfe_io:parse_file/1 and
            is used by the compiler to give better error
            information.

EXPORTS

read([IoDevice]) -> {ok,Sexpr} | {error,ErrorInfo}

        Read an s-expr from the standard input (IoDevice).

read_string(String) -> {ok,Sexpr} | {error,ErrorInfo}

        Read an s-expr from String.

print([IoDevice,] Sexpr) -> ok

        Print the s-expr Sexpr to the standard output (IoDevice).

prettyprint([IoDevice,] Sexpr) -> ok

        Pretty print the s-expr Sexpr to the standard output
        (IoDevice). Assume we start with no indentation.

print1(Sexpr) -> DeepCharList

        Return the list of characters which represent the s-expr Sexpr.

prettyprint1(Sexpr, CurrentIndentation) -> DeepCharList

        Return the lost of characters which represents the
        prettyprinted s-expr Sexpr. Assume we start at indentation
        CurrentIndentation.

print1_symb(Symbol) -> DeepCharList.

        Return the list of characters needed to print the symbol Symbol.

print1_string(String) -> DeepCharList.

        Return the list of characters needed to print the string
        String as a string.

format([IoDevice,] Format, Args) -> ok
format1(Format, Args) -> DeepCharList

        Print formatted output. The following commands are valid in
        the format string:

        ~w, ~W        - print LFE terms
        ~p, ~P        - prettyprint LFE terms
        ~s            - print a string
        ~e, ~f, ~g    - print floats
        ~b, ~B        - based integers
        ~x, ~X        - based integers with a prefix
        ~+, ~#        - based integers in vanilla erlang format
        ~c, ~n, ~i

        Currently they behave as for vanilla erlang except that ~w,
        ~W, ~p, ~P print the terms as LFE sexprs.

read_file(FileName) -> {ok,[Sexpr]} | {error,ErrorInfo}

        Read the file Filename returning a list of s-exprs (as it
        should be).

parse_file(FileName) -> {ok,[FileSexpr]} | {error,ErrorInfo}

        where
          FileSexpr = filesexpr()

        Read the file Filename returning a list of pairs containing
        s-expr and line number of the start of the s-expr.

Error Information

        The ErrorInfo mentioned above is the standard ErrorInfo
        structure which is returned from all IO modules. It has the
        following format:

        {ErrorLine,Module,ErrorDescriptor}

        A string describing the error is obtained with the following call:

        apply(Module, format_error, ErrorDescriptor)
{% endhighlight %}
