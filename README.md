# Luhns
Luhns Algorithm implemented into C# functions

The algorithm I want to discuss here is called the Luhn Algorithm. It is also known as the mod 10 check. The Luhn algorithm is a simple checksum formula used to validate a variety of identification numbers, but the most common use is credit card numbers. The algorithm was invented by an IBM scientist, Hans Peter Luhn. Hence the name given.

This formula verifies a number against its included check digit which is usually appended to a partial account number to generate the full account number. This number must pass the following test.

- Starting from the right hand side of the card number, skip the last digit.
- Double every other number.
- Write down the rest of the numbers as they are.
- If the doubled numbers from step 2 have 2 digits, then add them together, i.e. 14  = 1+4 = 5.
- Add together all the digits in the card number.
- Once you have done all these steps, you can then calculate the modulus 10 of that number. If the result is 0 then it is a valid card number; otherwise it is an invalid number.

# Implementation


