Heap

understanding: a array that almost in order

Tree structure:
root = first element(i=1)
No. i element:
	parent: locates at i/2
	left child: 2i - 1
	right child 2i
Property: key of a node >= the key of its children

Max heapify:
suppose the children of the root are both max heaps. -> set the node in position to meet 2i ruls
compare the children of the root and root itself, choose the element needed to be ajusted and dive this element following one of the path to the place it should be
complexity: θ(lg n) 

Max Heap Creation:
for x in n/2 downto 1:
 	do max heapify(x)
time complexity: O(n)
