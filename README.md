# ADSML

### Prim's Algorithm

```
def neighbours(Amat, n):
    l=[]
    for i in range(len(Amat)):
            if Amat[n][i]>0:
                l=l+[i]
    return l
    
def next_minimum_edge(neighbours_list, n, Edges, visited):
    for i in range(len(Edges)):
        if Edges[i][1]==n and not(visited[Edges[i][2]]):
            return Edges[i][2]
        
def minimum_edge_in_graph(Amat):
    l=[]
    visited={}
    for i in range(len(Amat)):
        visited[i]=False
        for j in range(len(Amat)):
            if Amat[i][j]>0:
                l+=[[Amat[i][j],i,j]]
    l.sort()
    return l, visited

def prims(Amat):
    ve=[]
    Edges, visited=minimum_edge_in_graph(Amat)
    a=Edges[0]
    ve+=[[a[1],a[2]]]
    vn=[a[2],a[1]]
    visited[a[1]]=True
    visited[a[2]]=True
    i=0
    count=0
    searching=[]
    while count<len(Amat)-2:
        print(vn)
        print(vn[i], "is the next picked vertex")
        l=neighbours(Amat,vn[i])
        b=next_minimum_edge(l,vn[i], Edges, visited)
        if b is None:
            i=0
            continue
        visited[b]=True
        count+=1
        ve+=[[vn[i],b]]
        vn+=[b]
        i=i+1
    return ve


a=[[0,10,0,18,0],[10,0,20,6,0],[0,20,0,0,8],[18,6,0,0,70],[0,0,8,70,0]]
print(prims(a))
```
### Prim's Alternate
```
def primlist(WList):
    infinity = 1 + max([d for u in WList.keys()
                           for (v,d) in WList[u]])
    (visited,distance) = ({},{})
    for v in WList.keys():
        (visited[v],distance[v]) = (False,infinity)
        
    TreeEdges = []
    visited[0] = True
    for (v,d) in WList[0]:
        distance[v] = d
    
    for i in WList.keys():
        mindist = infinity
        nextv = None
        for u in WList.keys():
            for (v,d) in WList[u]:
                if visited[u] and (not visited[v]) and d < mindist:
                    mindist = d
                    nextv = v
                    nexte = (u,v)
                    
        if nextv is None:
            break
        
        visited[nextv] = True
        TreeEdges.append(nexte)
        for (v,d) in WList[nextv]:
            if not visited[v]:
                distance[v] = min(distance[v],d)
    return(TreeEdges)
    
a={0: [(1, 10), (3, 18)], 1: [(2, 20), (3, 6), (0, 10)], 2: [(4, 8), (1, 20)], 3: [(4, 70), (0, 18), (1, 6)], 4: [(2, 8), (3, 70)]}
primlist(a)
```

        
### Kruskal's Algorithm

```
def kruskal(WList):
    (edges,component,TE) = ([],{},[])
    for u in WList.keys():
        # Weight as first component to sort easily
        edges.extend([(d,u,v) for (v,d) in WList[u]])
        component[u] = u
    edges.sort()
    print(edges)
    
    for (d,u,v) in edges:
        if component[u] != component[v]:
            TE.append((u,v))
            c = component[u]
            for w in WList.keys():
                if component[w] == c:
                    component[w] = component[v]
    return(TE)
    
a={0: [(1, 10), (3, 18)], 1: [(2, 20), (3, 6), (0, 10)], 2: [(4, 8), (1, 20)], 3: [(4, 70), (0, 18), (1, 6)], 4: [(2, 8), (3, 70)]}
kruskal(a)
```

### BST Insertion and Deletion

```
# Binary Search Tree operations in Python


# Create a node
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None


# Inorder traversal
def inorder(root):
    if root is not None:
        # Traverse left
        inorder(root.left)

        # Traverse root
        print(str(root.key) + "->", end=' ')

        # Traverse right
        inorder(root.right)


# Insert a node
def insert(node, key):

    # Return a new node if the tree is empty
    if node is None:
        return Node(key)

    # Traverse to the right place and insert the node
    if key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    return node


# Find the inorder successor
def minValueNode(node):
    current = node

    # Find the leftmost leaf
    while(current.left is not None):
        current = current.left

    return current


# Deleting a node
def deleteNode(root, key):

    # Return if the tree is empty
    if root is None:
        return root

    # Find the node to be deleted
    if key < root.key:
        root.left = deleteNode(root.left, key)
    elif(key > root.key):
        root.right = deleteNode(root.right, key)
    else:
        # If the node is with only one child or no child
        if root.left is None:
            temp = root.right
            root = None
            return temp

        elif root.right is None:
            temp = root.left
            root = None
            return temp

        # If the node has two children,
        # place the inorder successor in position of the node to be deleted
        temp = minValueNode(root.right)

        root.key = temp.key

        # Delete the inorder successor
        root.right = deleteNode(root.right, temp.key)

    return root


root = None
root = insert(root, 25)
root = insert(root, 6)
root = insert(root, 34)
root = insert(root, 65)
root = insert(root, 7)
root = insert(root, 10)
root = insert(root, 14)
root = insert(root, 4)

print("Inorder traversal: ", end=' ')
inorder(root)

print("\nDelete 65")
root = deleteNode(root, 65)
print("Inorder traversal: ", end=' ')
inorder(root)
print()
```

