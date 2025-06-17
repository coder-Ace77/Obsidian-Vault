
---

#### Basic DSU

```cpp
class DSU{
    public:
    vector<int> par,size;
    int n;
    DSU(int nn){
        n=nn;
        par.resize(n);
        size.resize(n);
        for(int i=0;i<n;i++){
            par[i]=i;
            size[i]=1;
        }
    }

    int find(int a){
        if(par[a]==a)return a;
        return par[a]=find(par[a]);
    }

    bool same(int a,int b){
        return find(a)==find(b);
    }

    void unite(int a,int b){
        a =find(a) , b = find(b);
        if(a!=b){
            if(size[a]<size[b])swap(a,b);
            par[b]=a;
            size[a]+=size[b];
        }
    }
};
```

#### Alternations:

We can sometimes store aggregate or properties of each group in an array or variable.

1. No of components-> Store a variable and when uniting reduce the number of that variable since one uniteb reduce the number of component by 1.
2. max Size: as size increases just keep max size variable and update it as u go.
3. Finding the minimum spanning tree (MST) of the graph. [Kruskal algo]
4. Set of property: Sometime we store the property as the set on node. Usually one may think it will take O(n) complexity. But the thing is we always join smaller set to larger one and so it takes O(nlogn) complexity only.

```cpp
void unite(int a,int b){
	a =find(a) , b = find(b);
	if(a!=b){
		if(size[a]<size[b])swap(a,b);
		par[b]=a;
		size[a]+=size[b];
		// set b to a
		for(auto x:prop[b]){
			prop[a].insert(x);
		}
	}
}
```

This can be used to solve problems where it is not enough to keep a single aggregate variable as the property for a node rather we need vector or set to store inside node. This is also called small to large merging.

For example number of unique colors in a component.

4. Reversing operations: DSU can easily merge but disjoining two components is not easy. So instead we go from reverse of queries and try to merge. This is feasible only if offline queries are allowed.
#### Abstracting the nodes: 

In many problems, especially when dealing with grouping or dynamic connectivity, we can model the system using **two types of nodes** in the DSU:

1. **Element Nodes**: These represent actual entities, like people, computers, etc.
2. **Group/Team Nodes**: These are _virtual_ or _abstract_ nodes representing logical groups (like a team, cluster, or organization).

##### **Example Use Case: “People and Teams” Problem**

Each person initially forms their own team. Over time, teams can merge, and we may need to:
- Merge two teams.
- Move a person from one team to another.
- Query the size of the team a person belongs to.
##### **DSU Design:**
- Each **person** is a node.
- Each **team** is a separate virtual node.
- Use `parent[]` such that:
    - Each person points to their team.
    - Each team manages its own DSU information (size, etc.).

Here element ids are normal 0,1,2... n-1 but team ids start from n,n+1,n+2....

```cpp
const int MAXN = 100005;  // max number of people
const int OFFSET = MAXN;  // offset for team IDs

int parent[2 * MAXN];     // parent[i]: DSU parent
int teamSize[2 * MAXN];   // size of team (valid only for team root)
int personTeam[MAXN];     // personTeam[i]: the team node that person i is in

// DSU find with path compression
int find(int x) {
    if (parent[x] != x)parent[x] = find(parent[x]);
    return parent[x];
}
// Union two teams
void mergeTeams(int a, int b) {
    // works as normal
}
// Initialize DSU: each person in their own team
void initialize(int n) {
    for (int i = 1; i <= n; ++i){
        int teamId = i + OFFSET;
        personTeam[i] = teamId;
        parent[i] = teamId;          // person i points to their team
        parent[teamId] = teamId;     // team is its own parent
        teamSize[teamId] = 1;
    }
}

void movePerson(int u, int v){
    int oldTeam = find(personTeam[u]);
    int newTeam = find(personTeam[v]);
    if (oldTeam == newTeam) return;
    // Remove from old team
    teamSize[oldTeam]--;
    // Assign to new team
    personTeam[u]=newTeam;
    parent[u]=newTeam;
    teamSize[newTeam]++;
}
```

🔍 **How it Works**
- `personTeam[i]`: tracks which team node person `i` belongs to.
- `parent[x]`: classic DSU parent pointer, applied to both people and team nodes.
- `teamSize[x]`: only relevant when `x` is a team node (or root of it).

### Range merging:

We need to support three types of operations:

1. Merge team(x),team(y)
2. Merge team(x),team(x+1)..... team(y)
3. Display size of a team or find if two players are in same team.


> [!NOTE] Solution
> 
Let's first consider a problem with only a queries of second and third type. It can be solved in a following manner. Consider a line consisting of all employees from 1 to _n_. An observation: any department looks like a contiguous segment of workers. Let's keep those segments in any logarithmic data structure like a balanced binary search tree (std::set or TreeSet). When merging departments from _x_ to _y_, just extract all segments that are in the range [_x_, _y_] and merge them. For answering a query of the third type just check if employees _x_ and _y_ belong to the same segment. In such manner we get a solution of an easier problem in ![](https://espresso.codeforces.com/9040a33098f83986b0de64475c66584fbfdf0e22.png) per query.
When adding the queries of a first type we in fact allow some segments to correspond to the same department. Let's add a DSU for handling equivalence classes of segments. Now the query of the first type is just using merge inside DSU for departments which _x_ and _y_ belong to. Also for queries of the second type it's important not to forget to call merge from all extracted segments.

```cpp
if(type==1){
	 d.unite(u,v);
}else if(type==2){
	// start from this node and remove and merge all that will appear in set
	// since each node is processed once. 
	auto it=st.lower_bound(u);
	vi temp;
	for(auto j=it;j!=st.end() && (*j)<v;j++){
		 temp.pb(*j);
	}
	for(int i=0;i<temp.size();i++){
		 d.unite(temp[i],temp[i]+1);
		 st.erase(temp[i]);
	}
}
else{
	 cout<<(d.same(u,v)?"YES":"NO")<<endl;
}
```

### Rollback in DSU

A **rollback DSU (Disjoint Set Union)** is a version of DSU that allows you to undo previous union operations.
Standard DSU updates `parent[]` and `size[]` destructively. To **rollback**, we store the **history of changes** on a stack, so we can undo them later.

Note the true path compression is disabled because it changes multiple pointers which are not easy to track.

```cpp
struct RollbackDSU {
    vector<int> par, size;
    // stack for previous operations
    stack<pair<int, int>> history;
    RollbackDSU(int n) {
        par.resize(n);
        size.assign(n, 1);
        for (int i = 0; i < n; ++i)
            par[i] = i;
    }

    int find(int x) {
        if(par[x]==x)return x;
        return find(par[x]);
    }

    bool unite(int x, int y) {
        x = find(x);
        y = find(y);
        if (x == y) {
            history.push({-1, -1}); // marker for no-op
            return false;
        }

        // Union by size
        if (size[x] < size[y])
            swap(x, y);
		// we need prev size of x and which was merged to do rollback
        history.push({y, size[x]}); // log the state 
        parent[y] = x;
        size[x] += size[y];
        return true;
    }

	// rollback is simple we need to change par[y] to itself and update the size of x.
    void rollback() {
        if (history.empty()) return;

        auto [y, sz_x] = history.top();
        history.pop();

        if (y == -1) return; // was a no-op

        int x = parent[y];
        size[x] = sz_x;
        parent[y] = y;
    }

    int getSize(int x) {
        return size[find(x)];
    }
};
```


