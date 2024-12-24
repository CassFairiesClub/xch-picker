# XCH Picker by Cass
[https://cassfairiesclub.github.io/xch-picker/](https://cassfairiesclub.github.io/xch-picker/)

The XCH Picker takes chia blockchain block header hashes first 12 hex characters and converts them to an integer. After sample rejection to make sure we don't introduce a bias, we then modulo that integer with a max range number.

The XCH picker is a tool to provably make a draw within the following process :
  1.  publish the potential winners list and announce a block in advance, a block that have not been farmed yet (unkown header_hash).
  2.  make your draw using the xch picker
  3.  anyone can check the result of the draw given the list and the chosen block

The function can be implemented by anyone : 
```
function hash2rand(header_hash, max) {
  const safe_big_int = 281474976710655; // 0xffff ffff ffff 
  const HH_Int = parseInt(header_hash.substring(0,14), 16)+1;
  // Check if within range, if not discard the header_hash
  if(HH_Int > Math.floor(safe_big_int/max)*max){
    return 0; 
  }else{
    return String(((HH_Int % max) + 1)).padStart(max.length, '0');
  }
}
```
