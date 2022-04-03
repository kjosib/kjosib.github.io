# Operator Overloading is Terrible

When it comes to numbers, whether real or imaginary,
I can wrap my head around what it means to add, subtract, multiply, and divide.
To that end, the venerable `+*-/` keys have served me well.

About every 5-10 years, some famous language designer thinks user-defined
mathematical operators will make working with user-defined types all that much more like "math".

**STOP THAT!**

First of all, programming is already math: the most challenging and profitable branch of applied mathematics, which makes habit of dealing with (by several orders of magnitude) the largest and most complex formulae found in any subfield of the mathematical discipline.

Second of all, that is how you ruin the language for the rest of us.

## Let's pick on Python for a bit.

> (Guido can take it.)
> (Actually, Guido does not care, does not know, and would not care if he did know.)
> So here we go.

Python cleverly overloads `+` for both strings and lists to mean concatenation.
Even more 
