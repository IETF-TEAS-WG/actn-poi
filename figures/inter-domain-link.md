~~~~ ascii-art

        +--------------------------+     +-------------------------+
       /  IP Topology (P-PNC 1)   /     /  IP Topology (P-PNC 2)  /
      /   +-------------+        /     /   +-------------+       /
     /    |    BR11     |       /     /    |    BR21     |      /
    /     |        (3-2)O<................>O(4-2)        |     /
   /      |             |\    /     /     /|             |    /
  /       +-------------+|   /     /      |+-------------+   /
 /                       |  /     /       |                 /
+------------------------|-+     +-------------------------+ 
                         |                |               
          Supporting LTP |                | Supporting LTP                
                         |                |                               
                         |                |                           
          +--------------|----------+    +|------------------------+
         /               V         /    / V                       /
        / +-------------+/        /    /  \+-------------+       /
       /  |     {1}(3-1)O<................>O(4-1){1}     |      /
      /   |             |\      /    /    /|             |     /
     /    |    BR11     |V(*)  /    /  (*)V|     BR21    |    /
    /     |             |/    /    /      \|             |   /
   /      |     {2}(3-0)O<~~~~~~~~~~~~~~~~>O(4-0){3}     |  /
  /       +-------------+   /    /         +-------------+ /
 / Eth. Topology (P-PNC 1) /    / Eth. Topology (P-PNC 2) /
+-------------------------+    +-------------------------+ 

Notes:
=====
(*) Supporting LTP
{1} {BR11,3,BR21,4}
{2} {BR11,3}
{3} {BR21,4}

Legenda:
========
  O   LTP
----> Supporting LTP
<...> Link discovered by the MDSC
<~~~> Link inferred by the MDSC
{   } LTP Plug-id reported by the PNC
~~~~
