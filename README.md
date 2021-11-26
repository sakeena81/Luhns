# Luhns
Luhns Algorithm implemented into C# functions

The algorithm I want to discuss here is called the Luhn Algorithm. It is also known as the mod 10 check. The Luhn algorithm is a simple checksum formula used to validate a variety of identification numbers, but the most common use is credit card numbers. The algorithm was invented by an IBM scientist, Hans Peter Luhn. Hence the name given.

This formula verifies a number against its included check digit which is usually appended to a partial account number to generate the full account number. This number must pass the following test.

1. Starting from the right hand side of the card number, skip the last digit.
2. Double every other number.
3. Write down the rest of the numbers as they are.
4. If the doubled numbers from step 2 have 2 digits, then add them together, i.e. 14  = 1+4 = 5.
5. Add together all the digits in the card number.
6. Once you have done all these steps, you can then calculate the modulus 10 of that number. If the result is 0 then it is a valid card number; otherwise it is an invalid number.


## Below is an implementation of a basic Luhn checker.

public class CardCommon
{
    private readonly int[] results = new[] { 0, 2, 4, 6, 8, 1, 3, 5, 7, 9 };
    private readonly Random random = new Random();
 
    public bool LuhnCheck(int[] digits)
    {
        if (digits == null)
        {
            throw new ArgumentNullException("digits");
        }
 
        return CheckDigits(digits);
    }
 
    private bool CheckDigits(int[] digits)
    {
        for (int i = digits.Length % 2; i < digits.Length; i += 2)
        {
            digits[i] = results[digits[i]];
        }
 
        return digits.Sum() % 10 == 0;
    }
 
    public bool LuhnCheck(string cardNumber)
    {
        if (string.IsNullOrEmpty(cardNumber))
        {
            throw new ArgumentNullException("cardNumber");
        }
 
        int[] digits = cardNumber.Select(c => c - '0').ToArray();
 
        if (digits.Sum() == 0)
        {
            return false;
        }
 
        return CheckDigits(digits);
    }
}

The above implementation is quite straight forward. After constructing the CardCommon class you can call one of 2 overloads of the LuhnCheck()  method. One of them takes in an array of integers. The other version takes the card number as a string. The LuhnCheck() method then calls the private method CheckDigits() which iterates through the card number every 2 digits and applies steps 2, 3 and 4 from the algorithm above. Instead of doing the match each time though it just pulls the results from a pre computed array. Once this process has happened, the digits are summed together and a mod 10 check is performed.

