![[Pasted image 20250315172527.png]]![[Pasted image 20250315172650.png]]![[Pasted image 20250315172924.png]]![[Pasted image 20250315232108.png]]
- Works by **relaxing all edges** multiple times.
- Updates the shortest distances by checking each edge **V-1 times** (where V is the number of vertices).
- Can **detect negative-weight cycles** by performing one more iteration.
- **Use case**: Works well when the graph has **negative weights**.
- V * E
- 🔹 **Relaxation** is the process of **updating the shortest known distance to a vertex** when a shorter path is found.  
🔹 It is the **core operation** in both **Bellman-Ford** and **Dijkstra’s algorithms**.
Тут каждый раз проходим еще раз тип с А до С каждую итерацию 
а в дижста мы делаем только один раз на каждую букву