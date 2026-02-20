# prog06 Study Guide: Strings & Lists

**Course**: CTE Programming | **Instructor**: Ryan McMaster
**Standards**: ODE 5.3.5 (string/list operations), 5.3.8 (data manipulation)

---

## Key Terms & Concepts

### Strings & Indexing

**String**: A sequence of characters in Python (immutable).
Example: `s = "hello"`

**Index**: Position of a character (0-based).
`s[0]` = 'h', `s[1]` = 'e', `s[-1]` = 'o' (last char)

**Slice**: Extract a substring using range syntax.
`s[1:4]` = 'ell' (from index 1 up to but not including 4)
`s[::-1]` = 'olleh' (reverse)
`s[2:]` = 'llo' (from index 2 to end)

**Immutable**: Strings cannot be changed after creation.
`s[0] = 'H'` ❌ ERROR — must use `.replace()` or create a new string

### String Methods

**`.upper()`**: Convert to uppercase. `"hello".upper()` → `"HELLO"`

**`.lower()`**: Convert to lowercase. `"HELLO".lower()` → `"hello"`

**`.strip()`**: Remove leading/trailing whitespace. `"  hello  ".strip()` → `"hello"`

**`.split()`**: Break string into list of words. `"a,b,c".split(",")` → `["a", "b", "c"]`

**`.join()`**: Combine list into single string. `"-".join(["a", "b", "c"])` → `"a-b-c"`

**`.find()`**: Find position of substring. `"hello".find("l")` → `2` (first occurrence)

**`.replace()`**: Swap out text. `"hello".replace("l", "x")` → `"hexxo"`

**`.count()`**: Count occurrences. `"hello".count("l")` → `2`

**`.startswith()`**: Check beginning. `"hello".startswith("he")` → `True`

**`.endswith()`**: Check ending. `"hello".endswith("lo")` → `True`

---

### Lists

**List**: Mutable collection of items (can change after creation).
`myList = [10, 20, 30]` or `myList = ["apple", "banana", "cherry"]`

**Index/Slice**: Same syntax as strings.
`myList[0]` = first item
`myList[-1]` = last item
`myList[1:3]` = second and third items

**Mutable**: Lists *can* be changed.
`myList[0] = 5` ✓ OK — changes first element

### List Methods

**`.append()`**: Add one item to end. `myList.append(40)` adds 40 to the end

**`.insert()`**: Insert at specific position. `myList.insert(1, 25)` adds 25 at index 1

**`.remove()`**: Delete first matching item. `myList.remove(20)` removes value 20

**`.pop()`**: Remove and return item at index. `myList.pop()` removes last item; `myList.pop(0)` removes first

**`.sort()`**: Sort in-place (ascending). `myList.sort()` rearranges myList

**`.reverse()`**: Reverse order in-place. `myList.reverse()` flips the list

**`.index()`**: Find position of item. `myList.index(20)` → position of value 20

**`.count()`**: Count occurrences of item. `myList.count(20)` → how many times 20 appears

---

### Advanced Operations

**`len()`**: Get length. `len("hello")` → `5`, `len([1, 2, 3])` → `3`

**`in` Operator**: Check membership.
`"e" in "hello"` → `True`
`5 in [1, 5, 9]` → `True`

**Looping Through Strings**:
```python
for char in "hello":
    print(char)  # prints h, e, l, l, o
```

**Looping Through Lists**:
```python
for item in myList:
    print(item)

for i in range(len(myList)):
    print(f"Index {i}: {myList[i]}")
```

**List Comprehension**: Create new list from existing one.
`doubled = [x * 2 for x in [1, 2, 3]]` → `[2, 4, 6]`

**Nested Lists**: List of lists (like 2D arrays in C).
```python
grid = [[1, 2], [3, 4], [5, 6]]
grid[0][1]  # → 2 (row 0, column 1)
```

---

## C vs Python Quick Reference

| Task | C | Python |
|------|---|--------|
| Get string length | `strlen(s)` | `len(s)` |
| Find character | manual loop | `s.find('x')` |
| Split by delimiter | manual tokenization | `s.split(',')` |
| Uppercase | manual loop + toupper | `s.upper()` |
| Create array | `int arr[100]` fixed | `arr = []` dynamic |
| Add to array | must realloc | `.append()` |
| Sort array | qsort() or write own | `.sort()` |
| Remove element | manual loop/shift | `.remove()` |
| Reverse | manual loop/swap | `.reverse()` |

---

## Important Notes

1. **Strings are immutable** → use methods that return new strings
2. **Lists are mutable** → methods like `.append()` modify in place
3. **Indexing is 0-based** → first item at index 0
4. **Negative indices work** → -1 is last item, -2 is second-to-last, etc.
5. **Slicing does not modify** → `s[1:3]` creates a new string/list
6. **`range(len(list))`** useful when you need indices, not just values

---

## Study Tips

- **Practice indexing and slicing** with different strings/lists
- **Use REPL** — test each method to see what it returns
- **Read error messages** — Python tells you what went wrong
- **Compare to C** — appreciate how much easier Python is!
- **Try list comprehensions** — once you get them, code gets shorter
