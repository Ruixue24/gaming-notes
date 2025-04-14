## 创建可移动平台（左右移动）

1. **在 Scene 中拖入一个平台对象**  
   在 `Hierarchy` 界面中将该平台命名为 `Platform`。

2. **选中 `Platform`，在 `Inspector` 面板中添加组件 `Box Collider 2D`**

3. **回到 `Hierarchy` 界面，右键选择 `Create Empty` 创建两个空物体**  
   分别命名为 `PosA` 和 `PosB`。

4. **设置位置**  
   - 选中 `PosA`，将其在 Scene 中移动到平台左侧  
   - 选中 `PosB`，将其移动到平台右侧

5. **新建一个空的 GameObject，命名为 `Moving Platform`**  
   将 `Platform`、`PosA` 和 `PosB` 拖入 `Moving Platform` 中作为子物体。

6. **为 `Platform` 添加脚本 `MovingPlatform`，并粘贴以下代码：**

   ```csharp
   using System.Collections;
   using System.Collections.Generic;
   using UnityEngine;

   public class MovingPlatform : MonoBehaviour
   {
       public Transform posA, posB;
       public float speed;
       Vector3 targetPos;

       void Start()
       {
           targetPos = posB.position;
       }

       private void Update()
       {
           if (Vector2.Distance(transform.position, posA.position) < 0.05f)
           {
               targetPos = posB.position;
           }

           if (Vector2.Distance(transform.position, posB.position) < 0.05f)
           {
               targetPos = posA.position;
           }

           transform.position = Vector3.MoveTowards(transform.position, targetPos, speed * Time.deltaTime);
       }

       private void OnTriggerEnter2D(Collider2D collision)
       {
           if (collision.CompareTag("Player"))
           {
               collision.transform.parent = this.transform;
           }
       }

       private void OnTriggerExit2D(Collider2D collision)
       {
           if (collision.CompareTag("Player"))
           {
               collision.transform.parent = null;
           }
       }
   }
7.回到 Unity，在 `Platform` 的 Inspector 面板中，将 `PosA` 和 `PosB` 分别拖拽到脚本的对应字段中。
8.再次选中'Platform'添加一个新的 Box Collider 2D,调整其大小，使其覆盖平台顶部，确保 Player 可以站在移动平台上。

