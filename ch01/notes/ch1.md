# Chapter 1: Polygon Triangulation

## 1.1.1 Polygons

**Definition of a Polygon**
A *polygon* is the region of a plane bounded by a finite collection of line
segments forming a simple closed curve. The phrase "simple closed curve" is hard to get a precise meaning for. We will be using this one:
Let $$v_0,v_1,\dots,v_{n-1}$$ be $n$ points in the plane. Here and throughout the book, all index arithmetic will be mod n, implying a cyclic ordering of the points, with $v_0$ following $v_{n-1}$, since $(n-1)+1 \equiv n \equiv 0 (\text{mod }n)$. Let $$e_0 = v_0v_1, e_1=v_1v_2, \dots, e_i=v_iv_{i+1}, \dots, e_n-1=v_{n-1}v_0$$
be $n$ segments connecting the points. Then these segments bound a polygon iff:
1. The intersection of each pair of segments adjacent in the cyclic ordering is the single point shared between them: $e_i \cap e_{i+1} = v_{i+1}$ for all $i=0,\dots,n-1$.
2. Nonadjacent segments do not intersect: $e_i \cap e_j = \emptyset$ for all $j \neq i+1$.

The reason these segments define a *curve* is that they are connected end to end; the reason the curve is *closed* is that they form a cycle; the reason the closed curve is *simple* is that nonadjacent segments do not intersect.
The points $v_i$ are called the *vertices* of the polygon, and the segments $e_i$ are called its *edges*. A polygon of $n$ vertices has $n$ edges.


> [!INFO] Theorem 1.1.1 (Jordan Curve Theorem)
> *Every simple closed plane curve divides the plane into two components*

We will take this as given. The two parts of the plane are called the *interior* and *exterior* of the curve. The exterior is unbounded, while the interior is bounded. This justifies the definition of a polygon as the region bounded by a collection of segments. It is often the case that a polygon $P$ is defined as a closed region of the plane. Often a polygon is considered to be just the segments bounding the region, and not the region itself. The notation $\partial P$ to mean the boundary of $P$; borrowed from topology (the partial derivative symbol). By our definition, $\partial P \subseteq P$. Polygons that satisfy condition (1) above *(adjacent segments share a common point)*, but not condition (2): nonadjacent segments intersect. These objects are often just called polygons, with those polygons that satisfy (2) called *simple polygons*. We will have little use for nonsimple polygons in this book, we will assume polygons are simple and drop the modifier.
The convention is to list the vertices of a polygon in counterclockwise order, so that if you walked along the boundary visiting the vertices in that order *(a boundary traversal)*, the interior of the polygon would always be to your left.
![[Pasted image 20260414001259.png]]

## The Art Gallery Theorem
### **Problem Definition**
We will study a problem that will lead naturally into the issue of triangulation, the most important polygon partitioning. Imagine an art gallery room whose floor plan can be modeled by a polygon of $n$ vertices. How many stationary guards are needed to guard the room? Each guard is considered a fixed point that has a $2\pi$ range of visibility, e.g, $360\degree$. Guards cannot see through walls. You can also form the question in terms of how many point lights are needed to fully illuminate the room.
We will make the problem rigorous before attempting an answer.

### **Visibility**
We say that point $x$ can *see* point $y$ iff the closed segment $xy$ is nowhere exterior to the polygon $P:xy\subseteq P$. This definition allows grazing contact with a vertex as shown above in figure 1.2. An alternative definition: say that $x$ has *clear visibility* to $y$ if $xy \subseteq P$ and $xy \cap \partial P \text{ and }\subseteq \{x,y\}$. We will sometimes use this definition.
A guard is a point. A set of guards is said to *cover* a polygon if every point in the polygon is visible to *some* guard. Guards do not block each other's visibility. Note that we could require the guards to only see points of $\partial P$, this is a variant explored in exercise 1.1.4[1].

### **Max over Min Formulation**
The problem is to find the maximum over all polygons of $n$ vertices, of the minimum number of guards needed to cover the polygon.
![[Pasted image 20260414234859.png]]
For any given fixed polygon, there is some minimum number of guards that are *necessary* for complete coverage. Thus in figure 1.3(a), it is clear that three guards are needed to cover that polygon of twelve vertices, although there is a lot of freedom in the location of the three guards. But is three the most that is ever needed for all possible twelve vertex polygons? No: the polygon in 1.3(b) requires four guards. What is the largest number of guards that any polygon of twelve vertices needs? We will show that four guards will always *suffice* for any polygon of twelve vertices. This is what the question seeks: Express as a function of $n$, the smallest number of guards that suffice to cover any polygon of $n$ vertices. Necessary in that at least that many are needed for *some* polygons, and sufficient in that that many always suffice for *any* polygon.

Let's formalize the problem more. Let $g(P)$ be the smallest number of guards needed to cover polygon $P: g(P)=\text{min}_S | \{S:\text{S covers P}\}|$, where $S$ is a set of points, and $|S|$ is the cardinality of $S$. Let $P_n$ be a polygon of $n$ vertices. $G(n)$ is the maximum of $g(P_n)$ over all polygons of $n$ vertices: $G(n) = \text{max}_{P_n}g(P_n)$. The art gallery problem is to determine the function $G(n)$. Let it be known that $G(n)$ is defined and finite for all $n$.

### **Empirical Exploration**
*sufficiency of n*. It is obvious that at least one guard is always necessary. This gives us our lower bound on $G(n): 1\leq G(n)$. It is also pretty obvious that $n$ guards will suffice for any polygon: stand a guard at every vertex will certainly cover the polygon. This gives us our upper bound: $G(n) \leq n$. In this case the intuition that $n$ guards can cover the polygon sufficiently is true and can be proven, but this is not the case for three dimensions (see Exercise 1.1.4[6]).
There are many art-gallery-like problems, and for most of them it is easiest first to establish the lower bound on $G(n)$ by finding generic examples showing that a large number of guards are sometimes necessary.