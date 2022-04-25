# UUID ([Content Addressing Guide](../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

A **UUID** (short for **universally unique identifier**) is a popular convention for creating **globally unique identifiers** (**GUID**s).

When written, **UUID**s tend to look like these

* `ea35427e-c39f-11ec-9d64-0242ac120002`
* `5a768259-b599-4051-b647-714a5db21d0d`
* `9d345a19-98c6-4b36-8dbf-8c4cca4352f3`
* `ed7ba470-8e54-465e-825c-99712043e01c`
* `573e0100-1364-7a49-9b8f-6b3e35e8b3c4`

These are just was of expressing 128-bit values in text. For example, here is one of the example **UUID**s expressed in text in other ways —

| Type                | Value                                                                                                      |
|---------------------|------------------------------------------------------------------------------------------------------------|
| Canonical           | `ea35427e-c39f-11ec-9d64-0242ac120002`                                                                     |
| Hexadecimal Literal | `0xea35427ec39f11ec9d640242ac120002`                                                                       |
| Array of Bytes      | `[16]byte{0xea, 0x35, 0x42, 0x7e, 0xc3, 0x9f, 0x11, 0xec, 0x9d, 0x64, 0x02, 0x42, 0xac, 0x12, 0x00, 0x02}` |
