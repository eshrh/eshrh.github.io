# Competitive Programming hackpack!

## Graph theory
#### Dijkstra's 
```
from heapq import heappush, heappop
class Edge:
  def __init__(self,l,w):
    self.loc = l 
    self.weight = w
  def __lt__(self,otheredge):
    return self.weight<otheredge.weight

n,m = [int(i) for i in input().split()]

graph = [[] for i in range(n)]
for i in range(m):
  line = [int(i) for i in input().split()]
  graph[line[0]].append(Edge(line[1],line[2]))
 
dist = [999 for i in range(n)]
pq = []
visited = [False for i in range(n)]
heappush(pq,Edge(0,0))

while pq!=[]:
  v = heappop(pq)
  if visited[v.loc]:
    continue
  visited[v.loc] = True
  dist[v.loc] = v.weight
  for nextedge in graph[v.loc]:
    heappush(pq,Edge(nextedge.loc,v.weight+nextedge.weight))
```

#### Kruskal MST
```python
import heapq
class Edge:
  def __init__(self,s,e,w):
      self.s = s
      self.e = e 
      self.w = w 
  def __lt__(self,other):
    return self.w-other.w 


n,m = [int(i) for i in input().split()]
edges = []

for i in range(m):
  line = [int(i) for i in input().split()]
  edges.append(Edge(line[0],line[1],line[2]))

mst = []
visited=[]
while len(mst)!=(n-1):
  cur = heapq.heappop(edges)
  if cur not in visited:
    mst.append(cur)
    visited.append(cur)
  
for i in mst:
  print(f"edge s:{i.s}, e:{i.e}, w:{i.w}")
```

#### Basic DFS
```python
visited = []
def dfs(cur,end):
    global graph,visited
    if cur==end:
        return True
    visited.append(cur)
    for nextnode in graph[cur]:
        if nextnode not in visited:
            temp = dfs(nextnode,end)
            if temp:
                return True
    return False
```
#### Basic BFS
```python
import queue
##2D GRAPH INPUT
def bfs(graph,sx,sy,wallchar):
  lenx = len(graph)
  leny = len(graph[0])
  qx = queue.Queue()
  qy = queue.Queue()
  visited = []
  qx.put(sx)
  qy.put(sy)
  dxArray = [0,0,-1,1]
  dyArray = [-1,1,0,0]
  while not qx.empty():
    curx = qx.get()
    cury = qy.get()
    if [curx,cury] in visited:
      continue
    visited.append([curx,cury])
    for i in range(4):
      dx = dxArray[i]
      dy = dyArray[i]
      nextx = curx+dx
      nexty = cury + dy 
      if 0<nextx<lenx and 0<nexty<leny and graph[nextx][nexty]!=wallchar:
        qx.put(nextx)
        qy.put(nexty)
```
#### Basic floyd-warshall
```python
n,m = [int(i) for i in input().split()]
dists = [[999 for i in range(n)] for j in range(n)]
middleOf = [[None for j in range(n)] for i in range(n)]

for i in range(m):
  raw = [int(i) for i in input().split()]
  dists[raw[0]-1][raw[1]-1] = raw[2]
  middleOf[raw[0]-1][raw[1]-1] = raw[1]-1



for k in range(n):
  for i in range(n):
    for j in range(n):
      if dists[i][j]>dists[i][k]+dists[k][j]:
        dists[i][j]=dists[i][k]+dists[k][j]
        middleOf[i][j] = middleOf[i][k]

print(dists[2][3])

def pathfind(s,e,path=[]):
  if middleOf[s][e]==e:
    path.append(s+1)
    path.append(e+1)
    return path
  path.append(s+1)
  pathfind(middleOf[s][e],e,path=path)
  return path

s = 0 
e = n-1

if dists[s][e]==999:
  print(-1)
else:
  print(" ".join([str(i) for i in pathfind(s,e)]))
```
## Number Theory

#### Test if n is prime
```python
from math import sqrt; from itertools import count, islice
def isPrime(n):
    return n > 1 and all(n%i for i in islice(count(2), int(sqrt(n)-1)))
```
#### Eratosthenes' Sieve
```python
def eratoSieve(n):
  sieve = [True]*n 
  sieve[0] = sieve[1] = False 
  for i in range(n):
    if sieve[i]:
      for j in range(i**2,n,i):
        sieve[j] = False 
  return sieve
```
***NOTE:** returns boolean array*
#### Euclidean GCD
```python
def gcd(a,b):
  if a==0 or b==0: return False
  if a==b: return a
  if (a > b): return gcd(a-b, b)
  return gcd(a, b-a)
 ```
***NOTE:** LCM(a,b) = a\*b / GCD(a,b)*
#### Binomial Coefficient
```python
def bincoeff(n,k):
    global c
    if c[n][k]==-1:
      if k==0 or k ==n :
          c[n][k] = 1
      else: 
          c[n][k] = bincoeff(n-1 , k-1) + bincoeff(n-1 , k)
    return c[n][k]
n = 5
k = 2
c = [[-1 for x in range(k+1)] for x in range(n+1)]
bincoeff(n,k)
```
#### Catalan Numbers
Uses:
1. matched parentheses counting
2. Ways a convex polygon with n+2 sides can be split into triangles by connecting vertices
3. Number of full binary trees with n+1 leaves
4. The number of paths with 2n steps on a rectangular grid from bottom left, i.e., (n-1, 0) to top right (0, n-1) that do not cross above the main diagonal.
5. Number of Dyck words of length 2n. a string consisting of n X’s and n Y’s such that no initial segment of the string has more Y’s than X’s. 
6. Number of permutations of {1, …, n} that avoid the pattern 123
```python
def catalan(n):
    if (n == 0 or n == 1): return 1

    catalan = [0 for i in range(n + 1)]
    catalan[0] = catalan[1] = 1

    for i in range(2, n + 1):
        catalan[i] = 0
        for j in range(i):
            catalan[i] = catalan[i] + catalan[j] * catalan[i-j-1]
    return catalan[n]
```
#### Java fast io

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.StringTokenizer;
 
public class Main
{
    static class FastReader
    {
        BufferedReader br;
        StringTokenizer st;
        public FastReader()
        {
            br = new BufferedReader(new
                     InputStreamReader(System.in));
        }
        String next()
        {
            while (st == null || !st.hasMoreElements())
            {
                try
                {
                    st = new StringTokenizer(br.readLine());
                }
                catch (IOException  e)
                {
                    e.printStackTrace();
                }
            }
            return st.nextToken();
        }
 
        int nextInt()
        {
            return Integer.parseInt(next());
        }
        String nextLine()
        {
            String str = "";
            try
            {
                str = br.readLine();
            }
            catch (IOException e)
            {
                e.printStackTrace();
            }
            return str;
        }
    }
 
```

#### Misc

1. Bayes' Theorem: `P(A|B) = (P(B|A)\*P(A))/P(B)`
2. In nim, if XOR of all heaps is 0, player 2 will win, otherwise, player 1.
3. Sum of factors can be calculated by first prime factorizing. N = (a^e1)(b^e2)(c^e3), `sum = (1+a+a^2+a^3+...+a^e1)...`
4. There is no `n` where `a^n+b^n = c^n`

