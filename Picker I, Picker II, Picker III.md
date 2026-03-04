# 🔐 picoCTF WriteUp – Picker I, Picker II, Picker III

<!-- Well yesterday is too hot. So this one teach me alot of thing more about python function and other way to run to execute line of code. must be importent for the future (I hope) >;3 -->

<!-- CATEGORY -->

![Category](https://img.shields.io/badge/category-reverse_engineering-blue)

<!-- DIFFICULTY -->
![Difficulty](https://img.shields.io/badge/difficulty-medium-yellow)

![Platform](https://img.shields.io/badge/platform-picoCTF-red)

---

## 📄 Summary
you have to launch instance for each one they will give netcat like `nc saturn.picoctf.net xxxxx` then we have to input something to get the flag. Oh they also give us source code to have idea what we have to input

### Short `eval(), exec()` Explanation
eval() : Is the python function that use to Evaluates(run) .So something like `eval('print(a)')` will give you `a`
exec() : Is the python function that use to Executes(doing something with data). like `exec('x=2')` then x will become 2

---

# Picker I
this is the first one for this series. It quit simple actually

## 🛠️ Steps to Solve

1. let analyz the source code
```python
import sys

def getRandomNumber(): #
  print(4)  # Chosen by fair die roll.
            # Guaranteed to be random.
            # (See XKCD)

def exit():
  sys.exit(0)
  
def esoteric1():
  esoteric = \
'''
  int query_apm_bios(void)
{
	struct biosregs ireg, oreg;

	/* APM BIOS installation check */
	initregs(&ireg);
	ireg.ah = 0x53;
	intcall(0x15, &ireg, &oreg);

	if (oreg.flags & X86_EFLAGS_CF)
		return -1;		/* No APM BIOS */

	if (oreg.bx != 0x504d)		/* "PM" signature */
		return -1;

	if (!(oreg.cx & 0x02))		/* 32 bits supported? */
		return -1;

	/* Disconnect first, just in case */
	ireg.al = 0x04;
	intcall(0x15, &ireg, NULL);

	/* 32-bit connect */
	ireg.al = 0x03;
	intcall(0x15, &ireg, &oreg);

	boot_params.apm_bios_info.cseg        = oreg.ax;
	boot_params.apm_bios_info.offset      = oreg.ebx;
	boot_params.apm_bios_info.cseg_16     = oreg.cx;
	boot_params.apm_bios_info.dseg        = oreg.dx;
	boot_params.apm_bios_info.cseg_len    = oreg.si;
	boot_params.apm_bios_info.cseg_16_len = oreg.hsi;
	boot_params.apm_bios_info.dseg_len    = oreg.di;

	if (oreg.flags & X86_EFLAGS_CF)
		return -1;

	/* Redo the installation check as the 32-bit connect;
	   some BIOSes return different flags this way... */

	ireg.al = 0x00;
	intcall(0x15, &ireg, &oreg);

	if ((oreg.eflags & X86_EFLAGS_CF) || oreg.bx != 0x504d) {
		/* Failure with 32-bit connect, try to disconnect and ignore */
		ireg.al = 0x04;
		intcall(0x15, &ireg, NULL);
		return -1;
	}

	boot_params.apm_bios_info.version = oreg.ax;
	boot_params.apm_bios_info.flags   = oreg.cx;
	return 0;
}
'''
  print(esoteric)


def win(): #*this is the function that give flag
  # This line will not work locally unless you create your own 'flag.txt' in
  #   the same directory as this script
  flag = open('flag.txt', 'r').read()
  #flag = flag[:-1]
  flag = flag.strip()
  str_flag = ''
  for c in flag:
    str_flag += str(hex(ord(c))) + ' '
  print(str_flag)
  
  
def esoteric2():
  esoteric = \
  '''
#include "boot.h"

#define MAX_8042_LOOPS	100000
#define MAX_8042_FF	32

static int empty_8042(void)
{
	u8 status;
	int loops = MAX_8042_LOOPS;
	int ffs   = MAX_8042_FF;

	while (loops--) {
		io_delay();

		status = inb(0x64);
		if (status == 0xff) {
			/* FF is a plausible, but very unlikely status */
			if (!--ffs)
				return -1; /* Assume no KBC present */
		}
		if (status & 1) {
			/* Read and discard input data */
			io_delay();
			(void)inb(0x60);
		} else if (!(status & 2)) {
			/* Buffers empty, finished! */
			return 0;
		}
	}

	return -1;
}

/* Returns nonzero if the A20 line is enabled.  The memory address
   used as a test is the int $0x80 vector, which should be safe. */

#define A20_TEST_ADDR	(4*0x80)
#define A20_TEST_SHORT  32
#define A20_TEST_LONG	2097152	/* 2^21 */

static int a20_test(int loops)
{
	int ok = 0;
	int saved, ctr;

	set_fs(0x0000);
	set_gs(0xffff);

	saved = ctr = rdfs32(A20_TEST_ADDR);

	while (loops--) {
		wrfs32(++ctr, A20_TEST_ADDR);
		io_delay();	/* Serialize and make delay constant */
		ok = rdgs32(A20_TEST_ADDR+0x10) ^ ctr;
		if (ok)
			break;
	}

	wrfs32(saved, A20_TEST_ADDR);
	return ok;
}

/* Quick test to see if A20 is already enabled */
static int a20_test_short(void)
{
	return a20_test(A20_TEST_SHORT);
}
  '''
  print(esoteric)


while(True): #*this function always work when start
  try:
    print('Try entering "getRandomNumber" without the double quotes...')
    user_input = input('==> ')
    eval(user_input + '()')
  except Exception as e:
    print(e)
    break

   ```

   - `eval(user_input + '()')` — this is the main function here. the `user_input` is what we input and it will end what we input with `()` that mean when we type something in input then it will mean we call the function of the name we input(I really hope you understand what I mean) So overall this line make we run the function that we type in.
   - `getRandomNumber()` — this function is a fake one to make us confuse. It just print out 4 everytime we call the function
   - `win()` — this is the function that will give us the flag but in hex form

2. now we know what function we have to call then just type in the function we want to call

```bash
Try entering "getRandomNumber" without the double quotes...
==> win
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x34 0x5f 0x64 0x31 0x34 0x6d 0x30 0x6e 0x64 0x5f 0x31 0x6e 0x5f 0x37 0x68 0x33 0x5f 0x72 0x30 0x75 0x67 0x68 0x5f 0x62 0x35 0x32 0x33 0x62 0x32 0x61 0x31 0x7d
```

   - the hex line they give will not the same for everyone so make sure to do this one yourself

3. after we dump the hex in Cyberchef we will get our flag

---

### 🚩 Flag
*not the same to anyone
```
picoCTF{4_d14m0nd_1n_7h3_r0ugh_b523b2a1}
```

---
# Picker II
now this one the try to stop us by add the function that won't work if we just give them `win`
```python
def filter(user_input): #*make it impossible to enter "win"
  if 'win' in user_input:
    return False
  return True
```

## 🛠️ Steps to Solve

1. we do everything the same as `Picker I` as in first step
2. If we cant input it in normal way then we have to do it sneakily. We can use `eval()` to sneak in the input and by pass them by join the letter together instead of whole 'win'

```bash
==> eval('w'+'i'+'n')
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x66 0x31 0x6c 0x37 0x33 0x72 0x35 0x5f 0x66 0x34 0x31 0x6c 0x5f 0x63 0x30 0x64 0x33 0x5f 0x72 0x33 0x66 0x34 0x63 0x37 0x30 0x72 0x5f 0x6d 0x31 0x67 0x68 0x37 0x5f 0x35 0x75 0x63 0x63 0x33 0x33 0x64 0x5f 0x30 0x62 0x35 0x66 0x31 0x31 0x33 0x31 0x7d 
```

   - the hex line they give will not the same for everyone so make sure to do this one yourself

3. after we dump the hex in Cyberchef we will get our flag

---

### 🚩 Flag
*not the same for anyone
```
picoCTF{f1l73r5_f41l_c0d3_r3f4c70r_m1gh7_5ucc33d_0b5f1131}
```

---
# Picker III
Now it alot harder than those 2 above. We have to tihnk alot mroe this time

## 🛠️ Steps to Solve

1. now we get the program that we can only input the thing that they read. you can see more information by type in `help` or `?`

```bash
==> help

This program fixes vulnerabilities in its predecessor by limiting what
functions can be called to a table of predefined functions. This still puts
the user in charge, but prevents them from calling undesirable subroutines.

* Enter 'quit' to quit the program.
* Enter 'help' for this text.
* Enter 'reset' to reset the table.
* Enter '1' to execute the first function in the table.
* Enter '2' to execute the second function in the table.
* Enter '3' to execute the third function in the table.
* Enter '4' to execute the fourth function in the table.

Here's the current table:
  
1: print_table
2: read_variable
3: write_variable
4: getRandomNumber

```

2. Now it time to look through the source code 

```python

import re



USER_ALIVE = True
FUNC_TABLE_SIZE = 4
FUNC_TABLE_ENTRY_SIZE = 32
CORRUPT_MESSAGE = 'Table corrupted. Try entering \'reset\' to fix it'

func_table = ''

def reset_table():
  global func_table

  # This table is formatted for easier viewing, but it is really one line
  func_table = \
'''\
print_table                     \
read_variable                   \
write_variable                  \
getRandomNumber                 \
'''

def check_table():
  global func_table

  if( len(func_table) != FUNC_TABLE_ENTRY_SIZE * FUNC_TABLE_SIZE):
    return False

  return True


def get_func(n):
  global func_table

  # Check table for viability
  if( not check_table() ):
    print(CORRUPT_MESSAGE)
    return

  # Get function name from table
  func_name = ''
  func_name_offset = n * FUNC_TABLE_ENTRY_SIZE
  for i in range(func_name_offset, func_name_offset+FUNC_TABLE_ENTRY_SIZE):
    if( func_table[i] == ' '):
      func_name = func_table[func_name_offset:i]
      break

  if( func_name == '' ):
    func_name = func_table[func_name_offset:func_name_offset+FUNC_TABLE_ENTRY_SIZE]
  
  return func_name


def print_table():
  # Check table for viability
  if( not check_table() ):
    print(CORRUPT_MESSAGE)
    return

  for i in range(0, FUNC_TABLE_SIZE):
    j = i + 1
    print(str(j)+': ' + get_func(i))


def filter_var_name(var_name):
  r = re.search('^[a-zA-Z_][a-zA-Z_0-9]*$', var_name)
  if r:
    return True
  else:
    return False


def read_variable():
  var_name = input('Please enter variable name to read: ')
  if( filter_var_name(var_name) ):
    eval('print('+var_name+')')
  else:
    print('Illegal variable name')


def filter_value(value):
  if ';' in value or '(' in value or ')' in value:
    return False
  else:
    return True


def write_variable():
  var_name = input('Please enter variable name to write: ')
  if( filter_var_name(var_name) ):
    value = input('Please enter new value of variable: ')
    if( filter_value(value) ):
      exec('global '+var_name+'; '+var_name+' = '+value)
    else:
      print('Illegal value')
  else:
    print('Illegal variable name')


def call_func(n):
  """
  Calls the nth function in the function table.
  Arguments:
    n: The function to call. The first function is 0.
  """

  # Check table for viability
  if( not check_table() ):
    print(CORRUPT_MESSAGE)
    return

  # Check n
  if( n < 0 ):
    print('n cannot be less than 0. Aborting...')
    return
  elif( n >= FUNC_TABLE_SIZE ):
    print('n cannot be greater than or equal to the function table size of '+FUNC_TABLE_SIZE)
    return

  # Get function name from table
  func_name = get_func(n)

  # Run the function
  eval(func_name+'()')


def dummy_func1():
  print('in dummy_func1')

def dummy_func2():
  print('in dummy_func2')

def dummy_func3():
  print('in dummy_func3')

def dummy_func4():
  print('in dummy_func4')

def getRandomNumber():
  print(4)  # Chosen by fair die roll.
            # Guaranteed to be random.
            # (See XKCD)

def win():
  # This line will not work locally unless you create your own 'flag.txt' in
  #   the same directory as this script
  flag = open('flag.txt', 'r').read()
  #flag = flag[:-1]
  flag = flag.strip()
  str_flag = ''
  for c in flag:
    str_flag += str(hex(ord(c))) + ' '
  print(str_flag)

def help_text():
  print(
  '''
This program fixes vulnerabilities in its predecessor by limiting what
functions can be called to a table of predefined functions. This still puts
the user in charge, but prevents them from calling undesirable subroutines.

* Enter 'quit' to quit the program.
* Enter 'help' for this text.
* Enter 'reset' to reset the table.
* Enter '1' to execute the first function in the table.
* Enter '2' to execute the second function in the table.
* Enter '3' to execute the third function in the table.
* Enter '4' to execute the fourth function in the table.

Here's the current table:
  '''
  )
  print_table()



reset_table()

while(USER_ALIVE):
  choice = input('==> ')
  if( choice == 'quit' or choice == 'exit' or choice == 'q' ):
    USER_ALIVE = False
  elif( choice == 'help' or choice == '?' ):
    help_text()
  elif( choice == 'reset' ):
    reset_table()
  elif( choice == '1' ):
    call_func(0)
  elif( choice == '2' ):
    call_func(1)
  elif( choice == '3' ):
    call_func(2)
  elif( choice == '4' ):
    call_func(3)
  else:
    print('Did not understand "'+choice+'" Have you tried "help"?')

```

3. basicly we can write variable and give it the value by use `write_variable()` by send `3` input And this is exactly how we going to get the flag. We just going to Overwrite the old variable!
4. by writing new variable with same name as old one that we can call then we can just call `win()` instead of `read_variable()` or `print_table()` by give them value `win`
```bash
==> 3       
Please enter variable name to write: read_variable
Please enter new value of variable: win
==> 2
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x37 0x68 0x31 0x35 0x5f 0x31 0x35 0x5f 0x77 0x68 0x34 0x37 0x5f 0x77 0x33 0x5f 0x67 0x33 0x37 0x5f 0x77 0x31 0x37 0x68 0x5f 0x75 0x35 0x33 0x72 0x35 0x5f 0x31 0x6e 0x5f 0x63 0x68 0x34 0x72 0x67 0x33 0x5f 0x32 0x32 0x36 0x64 0x64 0x32 0x38 0x35 0x7d
```
5. after we dump the hex in Cyberchef we will get our flag

---

### 🚩 Flag
*not the same for anyone
```
picoCTF{7h15_15_wh47_w3_g37_w17h_u53r5_1n_ch4rg3_226dd285}
```

---

## 💻 Tools / Commands Used

### Cyberchef
CyberChef is a free, browser-based tool made by GCHQ that lets you encode, decode, encrypt, decrypt, and transform data using a simple drag-and-drop "recipe" system — no coding needed. It supports 300+ operations like Base64, AES, hashing, and hex conversion, making it a go-to tool for security analysts, CTF players, and developers. Everything runs locally in your browser, so your data stays private.

### Netcat
Netcat is a lightweight, command-line networking tool often called the "Swiss Army Knife of networking" that can read and write data across network connections using TCP or UDP. It lets you do things like port scanning, file transfers, banner grabbing, and even setting up basic chat sessions or reverse shells — making it a favorite for sysadmins, penetration testers, and CTF players alike.
