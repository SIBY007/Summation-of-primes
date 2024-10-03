# Summation-of-primes
The sum of the primes below  is .

Find the sum of all the primes not greater than given .

Input Format

The first line contains an integer  i.e. number of the test cases.
The next  lines will contains an integer .

Constraints

Output Format

Print the value corresponding to each test case in separate line.

Sample Input 0

2
5
10
Sample Output 0

10
17
Explanation 0

For , we have primes as  and the sum is .
For , we have primes as  and the sum is .
-------------------------------------------------------------------------------------

#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <map>

using namespace std;
 
vector<int> primes = {2};
vector<unsigned long> sums;

map<int, unsigned long> temp = {{1, 0}, {2, 2}};


void Primes(int n)
{    
    unsigned long sum = 2;
    int p = 2, last_p = 2;
    vector<bool> sieve(n+10);            
            
    while(1)
    {        
        for(int i=2; p*i < sieve.size(); i++)
        {
            if(sieve[p*i] == false) sieve[p*i] = true;
        }
        
        for(int i=p+1; i < sieve.size(); i++)
        {
            if(sieve[i] == false) 
            {
                p = i;
                sum += p;
                temp[p] = sum;
                primes.push_back(p);
                
                break;
            }
        }
        if(p > n) break; 
    }
    out:
    int prev = 0;
    sums.reserve(n+p);
    
    for(auto it : primes)
    {        
        for(int i = prev; i<it; i++)
        {
            sums.push_back(temp[prev]);
        }
        prev = it;
    }    
    sums.push_back(temp[prev]);
    return;
}


int main() 
{
    int t;
    cin >> t;
    
    Primes(1000000);
    
    while(t--)
    {
        int n;
        cin >> n;

        cout << sums[n] << endl;
    }
    return 0;
}
