# UUID Generator ([Content Addressing Guide](../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

**UUID** (short for **universally unique identifier**) is a convention used by some to create **globally unique identifiers** (**GUID**s).

There are other conventions for creating **globally unique identifiers** (**GUID**s) too, that are _not_ **UUID**s.
(You can even make up your own convention.) 
But in this chapter we will focus on **UUID**s.

And more specifically, we are going to focus on generating our own **UUID**s.

**And you are going to write code to make this happen!**

## Git Repository

Create a new git repository for this called `go-uuid`

So, for example, if you were on `github.com` and your username was `joeblow`, then you new git respository would be at:
```
https://github.com/jowblow/go-uuid
```

## Type

You are going to create a type that represents a **UUID**.

And you are going to store the **UUID** efficiently as binary!
(This, storing the **UUID** as binary, is imporant!)

So:
```golang
package uuid

type UUID struct {
	value [16]byte
}
```

## Create

Create a function that will create `uuid.UUID` from 16 bytes:
```golang
package uuid

func Create(
	b0 byte,
	b1 byte,
	b2 byte,
	b3 byte,
	b4 byte,
	b5 byte,
	b6 byte,
	b7 byte,
	b8 byte,
	b9 byte,
	b10 byte,
	b11 byte,
	b12 byte,
	b13 byte,
	b14 byte,
	b15 byte,
) UUID {
	//@TODO
}
```

(You are going to write the code for this, and replace the `//@TODO` with the actual implementation.)

## Unit Tests for Create

Also, write _unit tests_ for your `uuid.Create()` function.

Here is some code to get you started:
```golang
func TestCreate(t *testing.T) {

	tests := []struct{
		B0 byte
		B1 byte
		B2 byte
		B3 byte
		B4 byte
		B5 byte
		B6 byte
		B7 byte
		B8 byte
		B9 byte
		B10 byte
		B11 byte
		B12 byte
		B13 byte
		B15 byte
		B16 byte
		Expected [16]byte
	}{
		{
			B0:  0xea,
			B1:  0x35,
			B2:  0x42,
			B3:  0x7e,
			B4:  0xc3,
			B5:  0x9f,
			B6:  0x11,
			B7:  0xec,
			B8:  0x9d,
			B9:  0x64,
			B10: 0x02,
			B11: 0x42,
			B12: 0xac,
			B13: 0x12,
			B14: 0x00,
			B15: 0x02,
			Expected: [16]byte{0xea, 0x35, 0x42, 0x7e, 0xc3, 0x9f 0x11, 0xec, 0x9d, 0x64, 0x02, 0x42, 0xac, 0x12, 0x00, 0x02},
		},
		
		//@TODO
	}

	for testNumber, test := range tests {

		actual := Create(
			test.B0,
			test.B1,
			test.B2,
			test.B3,
			test.B4,
			test.B5,
			test.B6,
			test.B7,
			test.B8,
			test.B9,
			test.B10,
			test.B11,
			test.B12,
			test.B13,
			test.B14,
			test.B15,
		)
		
		expected := test.Expected
		
		if expected != actual {
			t.Errorf("For test #%d, the actual value is not what was expected.", testNumber)
			t.Logf("EXPECTED: %v", expected)
			t.Logf("ACTUAL:   %v", actual)
			continue
		}
	}
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

## 

## Unit Tests for Random

Also, write _unit tests_ for your `uuid.Random()` function, making sure that:

* `uuid.UUID.values[6] & 0xf0` is equal to `0xf0`, and that 
* `uuid.UUID.values[8] & 0xc0` is equal to `0x80`,

… for any **UUID** that is returned from your `uuid.Random()` function.

Obviously this _unit test_ isn't going to test _all_ values returned from your `uuid.Random()` function. But you can test a fix number of samples from your `uuid.Random()` function. I.e., something like:
```golang
func TestRandom(t *testing.T) {

	const maxTests = 64

	for testNumber:=0; testNumber<maxTests; testNumber++ {
		var actual UUID = Random()
		
		//@TODO
	}
}
```

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

## Unit Tests for fmt.Stringer



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

## encoding.TextMarshaler

Make your `uuid.UUID` type implement the [encoding.TextMarshaler](https://pkg.go.dev/encoding#TextMarshaler) interface:

```golang
package uuid 

func (receiver *UUID) MarshalText() (text []byte, err error) {
	//@TODO
}
```

This will return your **UUID** in the **canonical** format for **UUID**s.
So, it will be similar to your `String()` method.

## encoding.TextUnmarshaler

Make your `uuid.UUID` type implement the [encoding.TextUnmarshaler](https://pkg.go.dev/encoding#TextUnmarshaler) interface:

```golang
package uuid 

func (receiver *UUID) UnmarshalText(text []byte) error {
	//@TODO
}
```

This will accept a **UUID** in the **canonical** format for **UUID**.

That means this `UnmarshalText()` method will need to make sure the value it is given as input is actually a **UUID**, and if not return an error.

## encoding.BinaryMarshaler

Make your `uuid.UUID` type implement the [encoding.BinaryMarshaler](https://pkg.go.dev/encoding#BinaryMarshaler) interface:

```golang
package uuid 

func (receiver *UUID) MarshalBinary() (text []byte, err error) {
	//@TODO
}
```

## encoding.BinaryUnmarshaler

Make your `uuid.UUID` type implement the [encoding.BinaryUnmarshaler](https://pkg.go.dev/encoding#BinaryUnmarshaler) interface:

```golang
package uuid 

func (receiver *UUID) UnmarshalBinary(text []byte) error {
	//@TODO
}
```
