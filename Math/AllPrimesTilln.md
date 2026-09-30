# Print all primes till n

You are given an integer n.

Print all the prime numbers till n (including n).

A prime number is a number that has only two divisor's 1 and the number itself.

## 1st approach (n√n)

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


## 2nd Approach (Sieve of Eratosthenes) (nloglogn)

Instead of checking whether every number is prime individually, start with all numbers and repeatedly cross out multiples of known primes.


```java

class Solution {
    public void printPrimes(int n) {
        boolean[] isPrime = new boolean[n + 1];

        // Initially assume every number is prime.
        for (int number = 2; number <= n; number++) {
            isPrime[number] = true;
        }

        for (int number = 2; number * number <= n; number++) {
            if (!isPrime[number]) {
                continue;
            }

            // Every multiple of number is not prime.
            for (int multiple = number * number; multiple <= n; multiple += number) {
                isPrime[multiple] = false;
            }
        }

        for (int number = 2; number <= n; number++) {
            if (isPrime[number]) {
                System.out.print(number + " ");
            }
        }
    }
}


```