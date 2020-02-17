# sha512-wasm
## Usage
```js
const sha512 = require('sha512-wasm')

if (!Sha512.SUPPORTED) {
  console.log('WebAssembly not supported by your runtime')
}

var hash = sha512()
  .update('hello')
  .update(' ')
  .update(Buffer.from('world'))
  .digest('hex')

console.log('Sha512 hash of "hello world" is ', hash)
// 309ecc489c12d6eb4cc40f50c902f2b4d0ed77ee511a7c7a9bcd3ca86d4cd86f989dd35bc5ff499670da34255b45b0cfd830e81f605dcf7dc5542e93ae9cd76f
```

## API
#### `const hash = sha512()`

Create a new hash instance.

#### `hash.update(data, [enc])`

Update the hash with a new piece of data. `data` may be passed as a buffer, uint8array or a string. If `data` is passed as a string, then it will be interpreted as a `utf8` string unless `enc` specifies an encoding.

#### `hash.digest([enc])`

Digest the hash. If `enc` is specified, then the digest shall be returned as an `enc` encoded string. Otherwise a buffer is returned.

#### `var promise = sha512.ready([cb])`

Wait for the WASM code to load. Returns the WebAssembly instance promise as well for convenience.
You have to call this at least once before instantiating the hash.

## Contributing

The bulk of this module is implemented in WebAssembly in the [sha512.wat](sha512.wat) file.
The format of this file is S-Expressions that can be compiled to their binary WASM representation by doing

```
wat2wasm sha512.wat -o sha512.wasm
```

To build the thin Javascript wrapper for the WASM module use `wat2js`:

```
# also available as `npm run compile`
wat2js sha512.wat -o sha512.js
```

If you do not have `wat2wasm` installed follow the instructions here, https://github.com/WebAssembly/wabt

## License

MIT
