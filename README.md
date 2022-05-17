
# printf() - Custom Implementation
In this project we will implement a printf() function of the following prototype: `int _printf(const char *format, ...);`

The function is variadic and thus takes any amount of arguments following the format pointer.


## Goals 🎉

- Implement custom printf() function similar to that of the standard library
- Use variadic functions to allow a custom number of arguments
- Parse a format string to identify custom print options




## Use & Examples ☕️
**Use - General:**`_printf("format string", var1, var2, ...);`

**Examples:**
 - Basic String: `_printf("%s World", "Hello");`
	 - Output: `Hello World`

- Print integers: `_printf("Here is an array element: arr[%d]:%c", 32, arr[32]);`
	- Output: `Here is an array element arr[32]:A`

You can do much more, by combining  specifiers like string or integer (full list of specifiers below) with flags, length modifiers, width, and precision.

**Return value of `_printf()`**
`_printf()` returns negative one (`-1`) upon failure, and the number of bytes (as an `int`) written to standard output upon success.

**Format specifiers follow this pattern:**
%[flags][width][.precision][length]specifier

- Example: `_printf("%+.22ld\n", LONG_MAX)`
	- Output: `+0009223372036854775807`

### Specifiers 🔤
The _specifier character_ at the end is the most significant component, since it defines the type and the interpretation of its corresponding argument:

|Specifier                |Output                        |Examples |
|----------------|-------------------------------|-----------------------------|
| `d` or `i` | Signed integer | 1024, -1024 |
| `u` | Unsigned integer | 1024 |
| `o` | Unsigned octal | 432 |
| `x` | Unsigned hexadecimal integer | 3ca |
| `X` | Unsigned hexadecimal integer (uppercase) | 3CA |
| `b` | Binary Representation of unsigned integer | 01010110 |
| `p` | Pointer address | 0x403212 |
| `s` | String of characters | Hello World |
| `c` | Character | y |
| `r` | Reversed string of characters | dlroW olleH |
| `R` | ROT13 Translation of string | Uryyb |
| `S` | String with hex-ascii value replacing special chars | \x0A\x0A |
The _format specifier_ can also contain sub-specifiers: _flags_, _width_, _.precision_ and _modifiers_ (in that order), which are optional and follow these specifications:
### Flags 🏳️🏴
|Flag                |Description                        |
|----------------|-------------------------------|
| `-` |Left-justify the output within the field width that was given; Right justification is the default (see _width_ sub-specifier). |
| `+` |Preceeds the result with a plus or minus sign (`+` or `-`) even for positive numbers. By default, only negative numbers are preceded with a `-` sign. |
| `(space)` |If no sign is going to be written, a blank space is inserted before the value. |
| `#` |Used with `o`, `x` or `X` specifiers the value is preceeded with 0, 0x or 0X respectively for values different than zero. |
| `0` |Left-pads the number with zeroes (`0`) instead of spaces when padding is specified (see _width_ sub-specifier). |


### Width  📏
|Width                |Description                        |
|----------------|-------------------------------|
| `(number)` |Minimum number of characters to be printed. If the value to be printed is shorter than this number, the result is padded with blank spaces. The value is not truncated even if the result is larger.|
| `*` | The _width_ is not specified in the _format_ string, but as an additional integer value argument preceding the argument that has to be formatted.|

### Precision 📐
|.Precision               |Description                        |
|----------------|-------------------------------|
| `.(number)` |**For integer specifiers (`d`, `i`, `o`, `u`, `x`, `X`):** _precision_ specifies the minimum number of digits to be written. If the value to be written is shorter than this number, the result is padded with leading zeros. The value is not truncated even if the result is longer. A _precision_ of 0 means that no character is written for the value 0. **For `s`**: this is the maximum number of characters to be printed. By default all characters are printed until the ending null character is encountered. If the period is specified without an explicit value for _precision_, 0 is assumed. |
| `.*` |The _precision_ is not specified in the _format_ string, but as an additional integer value argument preceding the argument that has to be formatted. |

### Length Modifiers 🤥
The _length_ sub-specifier modifies the length of the data type. This is a chart showing the types used to interpret the corresponding arguments with and without _length_ specifier (if a different type is used, the proper type promotion or conversion is performed, if allowed

|Modifier/Specifier  |`d` & `i`  |`u`, `o`, `x`, `X` |`c` |`s` |`p` |
|----------------|---------|------------|-------------|-----|-------|
| `none` | int |unsigned int | int| char pointer| void pointer |
| `h` |short int|unsigned short int |     |     |              |
| `l` |long int |unsigned long int  |     |     |              |

All together they allow you to manipulate output for various formatting techniques. Although printf does essentially the same thing, we have replicated it to further deepen our understanding of C.

## Files / Directories 📂
|Name                |Information                        |Relevant Files                         |
|----------------|-------------------------------|-----------------------------|
|`testing`|Directory containing files relevant to testing, such as main files.|`main.c`|
|`holberton.h`	| Header file containing struct and public function definitions.| `*.c`
|`_printf.c`|Main printf function file. Setups buffer and calls other functions as the format string is traversed.|`char_checkers.c`, `printf_helper_funcs.c`, `get_field_funcs.c`, `buffer_functions.c`|
`_bases.c` | Contains generic base calculation functions. Gets size of buffer needed to hold conversion from int[base]->string, and fills the buffer with the proper conversion (seperate functions).| `int_spec_funcs.c`, `get_hex_n_funcs.c`, `custom_spec_funcs.c` | 
`_strings.c` | Custom functions for string operations, such as strlen and strcpy. | `flag_spec_funcs.c`, `get_field_funcs.c`, `custom_spec_funcs.c`, `char_spec_funcs.c`, `get_prec_funcs.c`, `hex_spec_funcs.c`  |
`buffer_functions.c` | Functions used by `_printf.c` and `printf_helper_funcs.c` to create, copy, and print the buffer so only one write call is needed. | `_printf.c`, `printf_helper_funcs.c` |
`get_string_funcs.c` | Function that gets the proper string function for a given type specifier | `_printf.c` |
`char_checkers.c` | Functions that check characters, such as if it is a flag, specifier, alpha, printable or in an array. | `print_f.c`, `custom_spec_funcs.c`, `_strings.c`, `get_flag_funcs.c`, `get_prec_funcs.c` |
`char_spec_funcs.c` | Character specific functions returned by `get_string_func()`. Creates memory and copies variable type into a string usable by buffer. Also deals with insertion of null byte character into buffer directly. | `get_string_funcs.c`, `printf_helper_funcs.c` | 
`custom_spec_funcs.c` | Custom specifier functions such as reversing a string, or getting binary representation of a number. The strings are returned by `get_string_func()`. | `get_string_funcs.c` |
`flag_spec_funcs.c` | Contain functions that append various characacters ('+', ' ', '0x', etc.) to strings of valid specifiers. | `get_flag_funcs.c`, `printf_helper_funcs.c` |
`int_spec_funcs.c` | Integer specific functions returned by `get_string_func()`. Creates memory and copies variable type into a string, doing proper base conversion. | `_bases.c`, `get_string_funcs.c` |
`hex_spec_funcs.c` | Hexadecimal specific functions returned by `get_string_func()`. Creates memory and copies variable type into string, doing proper base conversion for hex (16). | `_bases.c`, `get_string_funcs.c` |

About Functions
int _write(char c)
This function gets a char parameter and writes the parameter to the stdout, the standard output stream.

int _print_a_char (va_list args)
This function gets a variadic arguments list, traverse the list, prints each character of char type and returns the length of the character.

int _print_a_string (va_list args)
This function gets a variadic arguments list, traverse the list, prints each string and returns the length of the string.

int _print_a_integer (va_list args)
This function gets a variadic arguments list, traverse the list, prints each number of int type and returns the length of the integer.

int _print_format (const char *format, va_list args)
This function gets a format to be printed and a variadic arguments list, next to check if the format is valid or invalid and according with the verification the resulting output is written to the standard output stream and returns the format length.

int _print_spec (char format, va_list args):
This function gets a format valid to be printed and a variadic arguments list to find the format in the list and selects the appropriate function to execute and writes the format to the standard output stream and returns the length of the valid format.

int _print_invalid_spec (char prev_format, char format, int count)
This function gets the previous format of the current format, the actual format and the current count of printed characters. Next, the invalid format is written to the standard output stream and returns the length of the invalid format.

void _recursion_integer(int a)
This function gets an integer and prints the last digit of the number as recursion is applied.

int _validate_char(char _type)
Gets a type and checks if the passed parameter is present in a structure of valid conversion specifiers. Next, returns if the parameter is valid or invalid.

Return Value
Upon successful return, the _printf() function return the number of characters printed (excluding the null byte used to end output to strings).

If an output error is encountered, a negative value is returned.

Examples
#include "holberton.h"

_printf("Hello Holberton"); // the output will be: Hello Holberton

_printf("%c", 'H'); // the output will be: H

_printf("%s", "Hello Holberton"); // the output will be: Hello Holberton

_printf("%!\n"); // the output will be '%!'

_printf("Complete the sentence: You %s nothing, Jon Snow.\n", "know"); // the output will be: Complete the sentence: You know nothing, Jon Snow.

_printf("% s", "Hello"); // the output will be: Hello

_printf("% k"); // the output will be: % k

## References 📖
 - “Printf.” _Cplusplus.com_, www.cplusplus.com/reference/cstdio/printf/.

