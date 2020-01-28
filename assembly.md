# Basic Assembly Language

## Op Codes

### Arithmetic

```sh
add $r1, $r2 => $r3
sub $r1, $r2 => $r3
mul $r1, $r2 => $r3
div $r1, $r2 => $r3

addi $r1, immi => $r2 - signed only
```

addition of `u` to each address indicated unsigned

total = 9

### Branching

```sh
cmp  $r1, $r2 => $flags	- signed
cmpu $r1, $r1 => $flags - unsigned

ja $r1	(jump to address)

# offset based
<jump> immi
jmp, jz, jnz, je, jne, jl, jle, jg, jge
```

implement `not` version of instructions via `or` on `$flag` register before check?

total = 12

### Boolean

```sh
and $r1, $r2 => $r3
or  $r1, $r2 => $r3
not $r1 => $r2
sl(l|a)  $r1, $r2 => $r3
sr(l|a)	$r1, $r2 => $r3

l = logical (unsigned), a = arithmetic (signed)
```

total = 7

### Memory

```sh
mov $r1, $r2 => $r2				(move - between registers)
ld  $r1 (addr) => $r2			(load from address)
str $r1, $r2 (addr) => addr		(store to address)
```

total = 3

### Stack

```sh
push $r1 => <STACK>
pop  $r1 => $r1 (from stack)
peek $r1 => $r1 (from stack) - does not alter stack
```

total = 3

## Registers

Size: 8 bit

### Registers

| #    | Conventional Name | Usage                                            |
| ---- | ----------------- | ------------------------------------------------ |
| 0    | `$zero`           | hard-wired to 0                                  |
| 1    | `$pc`             | program counter                                  |
| 2    | `$sp`             | stack pointer                                    |
| 3    | `$fp`             | frame pointer                                    |
| 4    | `$ra`             | return address                                   |
| 5    | `$dp`             | pointer to start of data                         |
| 6    | `$flag`           | flags                                            |
| 7-15 | `$r0 - $r#`       | saved registers - preserved during function call |

#### $flag

| Flag     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| Zero     | result of last operation was zero                            |
| Overflow | result of last operation overflowed register                 |
| Less     | result of last `cmp` was less                                |
| Equal    | result of last `cmp` was equal                               |
| Greater  | result of last `cmp` was greater (check of `Less` and `Equal` not set?) |
| Negative | result of last operation was negative                        |
| Carry    | result of last operation has a carry bit                     |

# Execution

1. Fetch 3 bytes (1 is instruction, 2 are register or data values)
2. pad 2 byte instructions with a `nop` (zeroes)

## TODO

* floating point?
* Input / Output? - screen and file ?
* flags