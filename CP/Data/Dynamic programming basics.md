
---

1. Dynamic programming can be think as the recursive(backtracking) minset. 
2. Recognise the form of dp is crutial in solving dp problems. -> pattern
3. formulate the problem as dp(state) = (meaning) -> thing computed by dp. This is 90% of time the value asked.
4. Most of dp are of this forms:
	1. Object iteration
	2. Ending dp
	3. Multiarray dp 
	4. lr dp 
	5. Game dp
5. There are other forms as well - 
	1. Digit dp 
	2. tree dp
	3. bitmask dp
6. Modelling the transitions. (imp)
7. Save and return.
8. Any dp problem can be categorised into three categories.
	1. Classical 
	2. Non classical -> twisted version of classical
	3. competitive


> [!NOTE] Tips about writing recursion correctly
> First write the state and what will it compute. Then find the minimal state-> minimal state is the minimum information required to solve the problem. We consider and assume that for given state consider that its smaller form is already implemented. Then how are you going to find the correct value for given state from smaaler states. That is it for writing recursion.
> Concept of level , choice , check and move. Level is going to be current config then what are my choices. Check is given the choices which are valid and which are invalid. Move is the transition. 
> 

Solving N queens:

1. In any row only one queen can be placed.
2. We can keep in bitmask which cols are used. 
3. Now our dp is -> dp(row,bitmask) = no of ways given we are placing last queen at row such that bitmask is keeping track of which cols are already used. 


> [!NOTE] DP vs Greedy
> One thing which I have observed many times is that in dp problems most of the times there is something to optimise which is also the case with greedy. But with dp there is some other restriction too. This is usually what makes dp diff from greedy. Finally most of the optimisation problems where a person may confuse itself lie in knapsack category. The thing is that knapsack problems have inherent acceptance about the situation  that for a given current chioce for this level it may not be the perfect choice given we are calculating some other level. For eg -> the smallest cost to incur for making some x sum may have differnt set of choices than for the sum y and so on. So mostly all possible schenaios have to be seen. There can be optimisations lying underlying which might be greedy.

```cpp
int solve(state){
	base cases;
	memoise;
	for(all choices){
		if(valid(choice)){
			move(choice);
		}
	}
	return ans;
}
```


Note: Memory limit for functions is 10^6 and for global arrays it is 10^7

States are actually collapsable into some more information dense form. For example set of choices if limited can be stored as bitmask. 

### Framework:

1. Look for form of problem.
2. Decide the meaning and state.
3. Find the transition function.



> [!NOTE] Time complexity
> TC= #S(1+average #c of transition per state)

### Type 1 DP: 

In these type of problems there is a concept of choices you are at given point then you have to take some choice and move forward. These are also kind of simluations problem. We may have to add to state the extra info needed to calc the correct answer.

Like -> Frog jump , grid paths etc..

#### Subset sum:

Find if there is a subset which sums upto x. 
n<=100 , x<=10000

Solution: Classical we wil move on items(levels) one by one choices there are is either ot choose or not to choose. Move to next. And this goes on. 
```cpp
dp(i,x) -> Find if first i elements can form sum upto x or not. 
dp(i,x) = dp(i-1,x) || dp(i-1,x-arr[i]) // can we form sum wither by taking or not taking. 
```

code: 
```cpp
int rec(int i,int x){
	if(i<0)return x==0;
	bool ok = rec(i-1,x);
	if(arr[i]<=x)ok || = rec(i-1,x-arr[i]);
	return ok;
}
```

printing solution:

Idea is to use the earlier written recursion and use that to solve the problem. 
Basically we would be able to figure out the choices made at given step by comparing the values.
suppose first choice gives yes then we can put that into ans. Now second choice need not to be explored.
Similarly if first choice fails we can check if second is the valid choice and move in that direction.

In this tech we create a dfs function:

This would function dfs must have same state.
Now we have base cases but instead of returning a value we stop.

Then we move to choices and move further.

```cpp
vector<int> ans;
void dfs(int i,int x){
	if(i<0)return;
	if(rec(i-1,x)==1)dfs(i-1,x);
	else if(rec(i-1,x-arr[i])==1){
		ans.push_back(i); // storing that this choice was taken
		dfs(i-1,x-arr[i]);
	}
}
```


### Form 2 Ending form:

