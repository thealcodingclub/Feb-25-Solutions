# Basketball Team

###### Made by [Hashir](https://github.com/sashshaikh12)

## Problem Statement:
You are organizing a 3v3 basketball tournament and need to select a diverse team. You have a sequence of 
𝑛
 players, where the 
𝑖
-th player belongs to team 
𝑎
[
𝑖
]
. Your goal is to form a team consisting of:

1) Three starting players such that no two players belong to the same team.

2) One substitute player, who must belong to the same team as at least one of the three starting players.

Determine the number of ways to select such a team.


## Input Format:

The first line contains n
 (1≤n≤10<sup>5</sup>
) — the number of players
.

The second line contains n integers a1,a2...,an, where ai is the team that ith player belongs to

## Constraints:

1) (1 <= n <= 10<sup>5</sup>)
2) (1 <= ai <= n)

## Output Format:

Print one integer, the number of ways to form a team

## Test Cases:

1) ```
    Input

    4
    1 1 2 3

    Output

    2
    ```

2) ```
    Input

    4
    1 2 2 3

    Output

    2
    ```

3) ```
    Input

    4
    1 2 3 3

    Output

    2
    ```

4) ```
    Input

    5
    1 1 1 2 2

    Output

    0
    ```

5) ```
    Input

    5
    1 1 1 2 3 

    Output

    6
    ```

6) ```
    Input

    6
    1 1 2 2 3 3

    Output

    24
    ```

7) ```
    Input

    4
    1 2 3 4

    Output

    0
    ```

8) ```
    Input

    5
    1 1 2 3 4

    Output

    6
    ```

9) ```
    Input

    8
    1 1 2 2 3 3 4 4

    Output

    96
    ```

## Solution:
Pseducode:

1) Read input n
2) Read input arr[0...n - 1]
3) Create frequency array, freq[0...n - 1], where freq array stores the frequency of each team number a[i]
4) create an array dp[0..n - 1][0...3][0...1], where dp[i][j][k] = number of ways to form a team in the suffix [i...n - 1] of the freq array, such that we have chosen j distinct players, and k indicates if we have picked a substitute player uptil now or not
5) pick = freq[i] * dp[i + 1][j + 1][k], if j < 3;
   
   pick_sub = (freq[i] * freq[i - 1]) * dp[i + 1][j + 1][k = 1], if j < 3, and k = 0

   not_pick = dp[i + 1][j][k]

6) dp[i][j][k] = pick + pick_sub + not_pick

7) return dp[0][0][0];



Implementation:

```cpp
#include <iostream>
#include <vector>
#include <map>
#include <functional>
#include <cstdio>
using namespace std;

typedef long long ll;

void solve(){
    ll n;
    cin>>n;
    vector<ll> v(n), freq;
    map<ll,ll> m;
    for (int i = 0; i < n; ++i)
    {
        cin>>v[i];
        ++m[v[i]];
    }
    for(auto i: m)
    {
        freq.push_back(i.second);
    }
    ll len = freq.size();
    
    vector<vector<vector<ll>>> dp(len, vector<vector<ll>> (4, vector<ll> (2, -1)));
    
    function<ll(ll ,ll, ll)> func = [&](ll i, ll j, ll k) -> ll{
        
        if(i == len)
        {
            if(j == 3 && k == 1) return 1;
            else return 0;
        }
        if(dp[i][j][k] != -1) return dp[i][j][k];
        
        ll pick = 0, pick_sub = 0, not_pick = 0;
        pick = freq[i] * func(i + 1, j + 1, k);
        if(k == 0 && freq[i] > 1) pick_sub = (freq[i] * (freq[i] - 1)) * func(i + 1, j + 1, 1);
        not_pick = func(i + 1, j, k);
        
        return dp[i][j][k] = pick + pick_sub + not_pick;
    };
    
    cout<<func(0,0,0);
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
} 

int main() {
#ifndef ONLINE_JUDGE
    freopen("Error.txt", "w", stderr);
#endif
    solve();
}
    
```
