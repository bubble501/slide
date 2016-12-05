# MethodSets

---

# Introduction
 <!-- .slide: transition="slide" -->
The method set determines what interface a value implements

---

# The Spec
+ **method Sets** A type may have a method set associated with it.
    - interface type -> interface itself
    - type T -> all methods with receiver type T
    - type \*T -> all methods with receiver type T and \*T
+ **Calls**
    - `x.m()` is valid only if:
       + The method set of `x` contains `m`
       + `x` is addressable and `&x` 's method set contains `m`

---

# Case by Case
+ Variables
+ Slice Elements
+ Map Elements
+ Interfaces

---

# Variables
```
type List []int

func (l List) Len() int  { return len(l) }
func (l *List) Append(val int) { *l = append(*l, val) }

func main() {
  // A bare value
  var lst List
  lst.Append(1)
  fmt.Printf("%v (len: %d)\n", lst, lst.Len())

  // A pointer value
  plst := new(List)
  plst.Append(2)
  fmt.Printf("%v (len: %d)\n", plst, plst.Len())
}
```
### method set
+ List
  - Len() int
+ \*List
  - Len() int
  - Append(int)

---

# Variables - Summary
+ The variable of `T` can invoke method `m` whether the receiver of `m` is T or \*T
  - Because variable `T` is addressable
+ The variable of `\*T` can invoke method `m` whether the receiver of `m` is T or \*T
  - Because `m` is in the method set of \*T
