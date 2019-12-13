---
title: Breedbase Slides
separator: <!--s-->
verticalSeparator: <!--v-->
theme: moon
highlight-theme: github
revealOptions:
    transition: 'fade'
---
### Getting Started with Perl

<div class="left">
Perl, like Python, is a scripting language created in the late 1980s.

It is know for it's flexibility and powerful native text processing capabilities.

Perl's motto: 'There's more than one way to do it.'

These days Perl generally refers to Perl 5
</div>
<div class="right">
<img style="max-height:400px;" src="http://cdn.facesofopensource.com/wp-content/uploads/2017/03/19223323/larrywall.faces23418.web_.jpg">
</div>


Note: 1987 vs 1989, Python from Monty Python and Perl from Pearl but Pearl was already taken. It has since been given the backronym ‘Practical Extraction and Reporting Language’.

<!--s-->

### Bad Press

Due it's flexibility, Perl sometimes has a bad reputation

<div>
  <img style="display: inline-block; height: auto; width: 60%;" src="https://raw.githubusercontent.com/bellerbrock/breedbase-slides/master/images/tweet.png">
</div>

<!--s-->

### Bad Press

It's not just hyperbole, Perl can be *very* flexible

<div>
  <img style="display: inline-block; height: auto; width: 50%;" src="https://raw.githubusercontent.com/bellerbrock/breedbase-slides/master/images/paint.png">
  <img style="display: inline-block; height: auto; width: 40%;" src="https://raw.githubusercontent.com/bellerbrock/breedbase-slides/master/images/paper.png">
</div>
https://famicol.in/sigbovik/2019.pdf

<!--s-->

### Normal Perl

But no need for craziness unless you're writting one liners or playing Perl golf

Simple practices can ensure perl stays just as sane as other languages

Scripts should start with:

```perl
#!/usr/bin/perl
use strict;
use warnings;
```

<!--s-->


### Normal Perl

Common sense practices are also key

* Make standard use of whitespace
* Be consistent
* Don't repeat yourself

<!--s-->

### Some Key Differences from Python

* White Space
* Basic Types
* Referencing
* Variable Scoping
* Built-in Features

<!--s-->

#### White Space

Because whitespace is not meaningful
* `{}` required around every block of code
* A `;` at the end of every statement

<!--s-->

#### White Space

```perl
if ($true) {
  do_something();
}
#same thing
if($true){do_something;}
```
<!--s-->

### Basic Types

Different types of variables (scalar, array, and hash)

Defined via a basic type system (‘$’, ‘@’, and ‘%’).

<!--s-->

### Basic Types

```perl
my $int = 1;
my $string = 'Hello';
my @array = ['Cruel','World'];
my %hash = (
  greeting => $string,
  addressee => \@array
);
```

<!--s-->

### Referencing

Not all variables are a reference.

Those that are require explicit dereferencing.

```perl
my %hash = (
 one => 1,
 two => 2
);

print_hash(\%hash);

sub print_hash {
  my $hash_ref = shift;
  print %$hash_ref;     # prints one1two2
}
```

<!--s-->

### Scoping

`my` provides lexical scoping;
A variable declared with `my` is visible only within the block in which it is declared.

<!--s-->

### Scoping

```perl
my $string = 'global ';

foreach (my $i=0; $i < 3; $i++) {
  my $string = 'loop ';
  if ($i == 2) {
    my $string = 'if ';
    print $string;
  }
  print $string;
}

print $string;

# Outputs 'loop loop if loop global'
```

<!--s-->

### Language features

Perl core is larger, with more built-in features.

Specifcally more text processing and sys/os interaction functions.

<!--s-->

### Language features

Regex example

```
$s1 = "new string";        # change to new string
$s2 = "new\nstring\with\nnew\nlines"; # change to new string
$s2 =~ s/\n/[newline]/g;   # substitute newlines with the text "[newline]"
```

<!--s-->

### Additional Differences: Quoting

Strings can be single or doubled quoted like in Python, but only double quoted strings interpolate any control characters inside them.

```perl
$s1 = "some string";
$s2 = "a string with\ncontrol characters\n";
$s3 = 'a "quoted" string';
$s5 = "a string with '\" both kinds of quotes";
$s6 = 'a stri\ng that au\tomatically escapes backslashes';
```

<!--s-->

### Additional Differences: Quoting

```perl
$name    = "Fred";
$title   = "Dr.";
$header = "Dear $title $name,";

print "$header\n"; # Prints "Dear Dr. Fred,"
```

<!--s-->

### Additional Differences: Comments

Like Python's ''', perlpod can be used for docstrings or multi line comments.

Start with `=` plus an optional type and title, end with `=cut`

<!--s-->

### Additional Differences: Comments

```perl
=pod
This function does stuff.
Remember to check its return value, as in:
  stuff() || die "Couldn't do stuff!";
=cut
```

<!--s-->

### Additional Differences: Length

Perl does not have a length operator like Python.

`scalar()` simply provides a scalar context

In a scalar context an array returns its size

<!--s-->

### Additional Differences: Length

Perl: `scalar(@A)``

Python: `len(A)`

<!--s-->

### Additional Differences: Intervals

Perl uses closed intervals, while Python uses closed-open intervals.

To generate a range of numbers:

Perl: `(0..9)`

Python: `range(0, 10)` or simply `range(10)` (assumes 0 as initial)

<!--s-->

### Additional Differences: OO

Perl has little native support for Object Oriented programming (OO)

But powerful packages to add OO support exist - Breedbase uses Moose

### Moose

Simple Package Definition

```perl
package Point;
use Moose; # automatically turns on strict and warnings

has 'x' => (is => 'rw', isa => 'Int');
has 'y' => (is => 'rw', isa => 'Int');

sub clear {
    my $self = shift;
    $self->x(0);
    $self->y(0);
}
```

### Moose

Simple Inheritance

```perl
package Point3D;
use Moose;

extends 'Point';

has 'z' => (is => 'rw', isa => 'Int');

after 'clear' => sub {
    my $self = shift;
    $self->z(0);
};
```

### Moose

Simple Instantiation And Use

```perl
use Point3D;

my $point = Point3D->new(
  x => 1,
  y => 1,
  z => 1,
);

# DO SOMETHING

$point->clear(); # Sets x,y,z to 0,0,0

```

<!--s-->

## Additional Resources

[Table of equivalent terms from each language](https://www.lemoda.net/perl/perl-python/index.html)

[Side by Side code comparisons](https://wiki.python.org/moin/PerlPhrasebook)

[Perl Maven Tutorial](perl maven)

[Comprehensive Perl Archive Network - CPAN](cpan)

<!--s-->

<style>
.left {
    margin: 10px 0 15px 20px;
    text-align: center;
    float: left;
    z-index:-10;
    width:48%;
    font-size: 20px;
    line-height: 1.5;
}
.right {
    margin: 10px 0 15px 0;
    float: right;
    text-align: center;
    z-index:-10;
    width:48%;
    font-size: 20px;
    line-height: 1.5;
}
</style>
