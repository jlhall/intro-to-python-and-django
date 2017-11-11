# Intro To Python & Django

i.e. it really just looks different 😀 This is an EXTREMELY brief sum up of python, and the rest is me talking about django, probably really fast, with production code examples. I've included the python exercises from the Google course.

### Schedule

There's a break in here somewhere??

- Python Intro
- Python Exercises
- Django Intro
- Django Codebase
- Abstract Topics (ooh spooky, that's right Halloween is not over)

### Resources

- [Google's Python Class](https://developers.google.com/edu/python/)
- Two Scoops of Django 1.11 - Best Practices for the Django Web Framework
- [Slicing, A Super Misunderstood Facet of Common Python](https://developers.google.com/edu/python/strings)
- [An Unfinished Flask App](https://github.com/jlhall/KnowYourDev/blob/master/know_your_dev.py) note how open ended flask is right off the bat. I'd compare it to Express for JS, or Sinatra for Ruby.
- [A Django Skeleton I Found](https://github.com/n2o/django-skeleton)
- [Python Debugger Cheatsheet](https://github.com/nblock/pdb-cheatsheet)
- [OpenHub's Django Page](https://www.openhub.net/p/django) for random django facts.
- [OpenHub's Rails Page](https://www.openhub.net/p/rails) same as above, just for comparison.

## Python: A Quick Summary

### Strings

The basics:

*Note: You pass the string object to a length (len) function instead of calling a built in (property) on the string object.
```python
s = 'hi'
  print s[1]          ## i
  print len(s)        ## 2
  print s + ' there'  ## hi there
```
Python's + operator does not do type coercion.
```python
pi = 3.14
  ##text = 'The value of pi is ' + pi      ## NO, does not work
  text = 'The value of pi is '  + str(pi)  ## yes
```

There is no ++, etc.

Here are some built-in !!methods!! on the string type.

- s.lower(), s.upper() -- returns the lowercase or uppercase version of the string
- s.strip() -- returns a string with whitespace removed from the start and end
- s.isalpha()/s.isdigit()/s.isspace()... -- tests if all the string chars are in the various character classes
- s.startswith('other'), s.endswith('other') -- tests if the string starts or ends with the given other string
- s.find('other') -- searches for the given other string (not a regular expression) within s, and returns the first index where it begins or -1 if not found
- s.replace('old', 'new') -- returns a string where all occurrences of 'old' have been replaced by 'new'
- s.split('delim') -- returns a list of substrings separated by the given delimiter. The delimiter is not a regular expression, it's just text. 'aaa,bbb,ccc'.split(',') -> ['aaa', 'bbb', 'ccc']. As a convenient special case s.split() (with no arguments) splits on all whitespace chars.
- s.join(list) -- opposite of split(), joins the elements in the given list together using the string as the delimiter. e.g. '---'.join(['aaa', 'bbb', 'ccc']) -> aaa---bbb---ccc

How do I substitute? By using this wonky lil guy. 

```python
# % operator
  text = "%d little pigs come out or I'll %s and %s and %s" % (3, 'huff', 'puff', 'blow down')
```

You can split up long lines (and should! PEP8 !!!)

```python
# add parens to make the long-line work:
  text = ("%d little pigs come out or I'll %s and %s and %s" %
    (3, 'huff', 'puff', 'blow down'))
```

If / Else / Else If / Or / And

```python
if speed >= 80:
    print 'License and registration please'
    if mood == 'terrible' or speed >= 100:
      print 'You have the right to remain silent.'
    elif mood == 'bad' or speed >= 90:
      print "I'm going to have to write you a ticket."
      write_ticket()
    else:
      print "Let's try to keep it under 80 ok?"

if thing is False or thing == False or thing not True:
    print "Dude it's false"

if thing == 2 and potatoe == potato:
    print "thingthingthing"
```

### Lists

Similar to the concept of any Array in Ruby, although there are minor differences to how Ruby implements a true "List" etc.
```python
colors = ['red', 'blue', 'green']
  print colors[0]    ## red
  print colors[2]    ## green
  print len(colors)  ## 3
```

Looping is dissimilar to Ruby:
```python
squares = [1, 4, 9, 16]
  sum = 0
  for num in squares:
    sum += num
  print sum  ## 30
```

Checking for values can also be done with keyword operators:
```python
list = ['larry', 'curly', 'moe']
  if 'curly' in list:
    print 'yay'
```

*Note: This also works for strings (behind the scenes, it works similarly to Ruby's str.split() looping practice)

*Double Note: Remember, direct lookup is always faster than looping, think Big O!

There are also ranges and while loops, but you don't reach for these as often as a simple for loop.

```python
## print the numbers from 0 through 99
  for i in range(100):
    print i

## Access every 3rd element in a list
  i = 0
  while i < len(a):
    print a[i]
    i = i + 3
```

Lists have built-in !!methods!! similar to Ruby

- list.append(elem) -- adds a single element to the end of the list. Common error: does not return the new list, just modifies the original.
- list.insert(index, elem) -- inserts the element at the given index, shifting elements to the right.
- list.extend(list2) adds the elements in list2 to the end of the list. Using + or += on a list is similar to using extend().
- list.index(elem) -- searches for the given element from the start of the list and returns its index. Throws a ValueError if the element does not appear (use "in" to check without a ValueError).
- list.remove(elem) -- searches for the first instance of the given element and removes it (throws ValueError if not present)
- list.sort() -- sorts the list in place (does not return it). (The sorted() function shown below is preferred.)
- list.reverse() -- reverses the list in place (does not return it)
- list.pop(index) -- removes and returns the element at the given index. Returns the rightmost element if index is omitted (roughly the opposite of append())

Common error: note that the above methods do not *return* the modified list, they just modify the original list.

### Dicts

```python
## Can build up a dict by starting with the the empty dict {}
  ## and storing key/value pairs into the dict like this:
  ## dict[key] = value-for-that-key
  dict = {}
  dict['a'] = 'alpha'
  dict['g'] = 'gamma'
  dict['o'] = 'omega'
```

Avoid KeyErrors... seriously.

```python
print dict['a']     ## Simple lookup, returns 'alpha'
  dict['a'] = 6       ## Put new key/value into dict
  'a' in dict         ## True
  ## print dict['z']                  ## Throws KeyError
  if 'z' in dict: print dict['z']     ## Avoid KeyError
  print dict.get('z')  ## None (instead of KeyError)
```


Our friend the % operator works with dicts too:
```python
hash = {}
  hash['word'] = 'garfield'
  hash['count'] = 42
  s = 'I want %(count)d copies of %(word)s' % hash  # %d for int, %s for string
  # 'I want 42 copies of garfield'
```

Deleting
```python
var = 6
  del var  # var no more!
  
  list = ['a', 'b', 'c', 'd']
  del list[0]     ## Delete first element
  del list[-2:]   ## Delete last two elements
  print list      ## ['b']

  dict = {'a':1, 'b':2, 'c':3}
  del dict['b']   ## Delete 'b' entry
  print dict      ## {'a':1, 'c':3}
```


### Errors, Try Catch etc.

You're a good developer, so you always catch errors
```python
try:
    ## Either of these two lines could throw an IOError, say
    ## if the file does not exist or the read() encounters a low level error.
    f = open(filename, 'rU')
    text = f.read()
    f.close()
except IOError:
    ## Control jumps directly to here if any of the above lines throws IOError.
    sys.stderr.write('problem reading:' + filename)
    ## In any case, the code then continues with the line after the try/except
```
