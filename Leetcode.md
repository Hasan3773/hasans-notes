On god gonna put notes for every type of leetcode problem

Math / Geometry:


Bit Manipulation:

```C
    uint32_t reversed = 0;
    uint32_t mask = 0x01;
    for (int i = 31; i >= 0; i--){
        if ((n & mask) == mask){
            reversed += (uint32_t)0x01 << i;
        }
        mask = mask << 1;
    }
    return reversed;
    
	n = ( n >>> 16 | n << 16);
	n = ((n & 0b11111111000000001111111100000000) >> 8) | ((n & 0b00000000111111110000000011111111) << 8);
	n = ((n & 0b11110000111100001111000011110000) >> 4) | ((n & 0b00001111000011110000111100001111) << 4);
	n = ((n & 0b11001100110011001100110011001100) >> 2) | ((n & 0b00110011001100110011001100110011) << 2);
	n = ((n & 0b10101010101010101010101010101010) >> 1) | ((n & 0b01010101010101010101010101010101) << 1);
	return n;

```

 

