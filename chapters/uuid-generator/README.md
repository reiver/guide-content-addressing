# UUID Generator ([Content Addressing Guide](../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

**UUID**s (short for **universally unique identifiers**) are a convention used by some to create **globally unique identifiers** (**GUID**s).

There are other conventions for creating **globally unique identifiers** (**GUID**s) too, that are _not_ **UUID**.
But in this chapter we will focus on **UUID**s.

And more specifically, we are going to focus on how we can generate our own **UUID**s.

**And you are going to write code to make this happen!**

## Git Repository

Create a new git repository for this called `go-uuid`

So, for example, if you were on `github.com` and your username was `joeblow`, then you new git respository would be at:
```
https://github.com/jowblow/go-uuid
```
## Type

You are going to create a type that represents the **UUID**.

And you are going to store the **UUID** efficiently as binary!
(This is imporant!)
So:
```golang
package uuid

type UUID struct {
	value [16]byte
}
```

## Random

Now you are going to create a function that creates a random **UUID**:
```golang
package uuid

func Random() UUID {
	//@TODO
}
```

(You are going to write the code for this, and replace the `//@TODO` with the actual implementation.)

Your implementation should do the following:

№1: set the values of each byte in `uuid.UUID.values` randomly,

№2: set the most-significant 4-bits of `uuid.UUID.values[6]` to `0b0100`,

№3: set the most-significant 2 bits of `uuid.UUID.values[8]` to `0b10`

## fmt.Stringer

Now you are going to make your `uuid.UUID` type implement [fmt.Stringer](https://pkg.go.dev/fmt#Stringer).
```golang
package uuid 

func (receiver UUID) String() string {
	//@TODO
}
```

Your `String()` method will return your **UUID** in the **canonical** UUID format.

So, for example, if you had a `uuid.UUID.values` with the value:
```golang
[16]byte{0xed, 0x7b, 0xa4, 0x70, 0x8e, 0x54, 0x46, 0x5e, 0x82, 0x5c, 0x99, 0x71, 0x20, 0x43, 0xe0, 0x1c}
```

Then your `String()` method would return:
```golang
"ed7ba470-8e54-465e-825c-99712043e01c"
```

## Chrono Random

Now you are going to create a function that creates a chrono random **UUID**:
```golang
package uuid

func ChronoRandom() UUID {
	//@TODO
}
```

Your implementation should do the following:

№1: set the values of the first 6 bytes to the unix timestamp,

№2: set the rest of the values of each byte in `uuid.UUID.values` randomly,

№3: set the most-significant 4-bits of `uuid.UUID.values[6]` to `0b0100`,

№4: set the most-significant 2 bits of `uuid.UUID.values[8]` to `0b10`


