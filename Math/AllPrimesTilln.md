# Print all primes till n

You are given an integer n.

Print all the prime numbers till n (including n).

A prime number is a number that has only two divisor's 1 and the number itself.

## 1st approach 

```java

class Solution {
    public void printPrimes(int n) {
        for (int number = 2; number <= n; number++) {
            if (isPrime(number)) {
                System.out.print(number + " ");
            }
        }
    }

    private boolean isPrime(int number) {
        if (number < 2) {
            return false;
        }

        for (int divisor = 2; divisor * divisor <= number; divisor++) {
            if (number % divisor == 0) {
                return false;
            }
        }

        return true;
    }
}


```


## 2nd Approach (Sieve of Eratosthenes)