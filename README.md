<div align="center">
  <a href="https://metacall.io" target="_blank"><img src="https://raw.githubusercontent.com/metacall/core/master/deploy/images/logo.png" alt="M E T A C A L L" style="max-width:100%; margin: 0 auto;" width="80" height="80">
  <p><b>M E T A C A L L</b></p></a>
  <p>A library for providing inter-language foreign function interface calls</p>
</div>

# Abstract

**[METACALL](https://github.com/metacall/core)** is a library that allows calling functions, methods or procedures between programming languages. With **METACALL** you can transparently execute code from / to any programming language, for example, call Python code from NodeJS.

# Install

Install MetaCall binaries first ([click here](https://github.com/metacall/install) for additional info about the install script):
```bash
bash <(curl -sL https://raw.githubusercontent.com/metacall/install/master/install.sh)
```

Then install MetaCall Dub package:
```bash
dub add metacall
```

# Example

`sum.py`
``` python
def sum(a, b):
  return a + b
```

`main.d`
``` d
import std.stdio;
import std.variant;
import metacall; // Import MetaCall

int main()
{
	dmetacall_initialize();
	string[] scripts = [
		"script.py"
	];
	dmetacall_load_from_file("py",scripts);
	Variant ret = dmetacall!(int,int)("add",1,2);
	writefln("add(1,2) = %d",ret.get!(long)); // 3
	dmetacall_destroy();
	return 0;
}
```

# Testing

In order to test you'll have to run `dub add-local ..` in the test folder.
