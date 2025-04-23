# 🧠 Horizontal Enemy Movement + Head Collision (Unity)

This guide explains how to set up a horizontally moving enemy that flips its facing direction and includes a head collision detection system to allow defeat when the player jumps on top.

---

## 📁 Setup Steps

### 1. Create Parent Object

- In the **Hierarchy**, right-click → `Create Empty` → rename it to `Horizontal_Enemy`.

### 2. Create Child Objects

- Under `Horizontal_Enemy`, create the following three child objects:
  - `Enemy` – the main enemy object
  - `PosA` – the leftmost point of movement
  - `PosB` – the rightmost point of movement

### 3. Add Head Detection

- Under `Enemy`, create an empty GameObject named `HeadCheck`.
- On `HeadCheck`, add a `Box Collider 2D`.
  - Resize it to cover the top of the enemy's head.
  - Check **Is Trigger**.
  - Attach the script `EnemyHead.cs` (used to detect player contact on the head).

### 4. Add Components to Enemy

- On the `Enemy` GameObject:
  - Add a `Box Collider 2D`.
  - Add a `Sprite Renderer` (if not already present).
  - Attach the custom script: `HorizontalMover.cs`

---

## 🧩 HorizontalMover.cs

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class HorizontalMover : MonoBehaviour
{
    public Transform leftPoint;
    public Transform rightPoint;
    public float speed = 2f;

    private Vector3 targetPos;
    private SpriteRenderer sr;

    void Start()
    {
        sr = GetComponent<SpriteRenderer>();
        targetPos = rightPoint.position;
    }

    void Update()
    {
        // Move between points
        transform.position = Vector3.MoveTowards(transform.position, targetPos, speed * Time.deltaTime);

        // Switch direction when arriving at target
        if (Vector2.Distance(transform.position, targetPos) < 0.05f)
        {
            if (targetPos == leftPoint.position)
                targetPos = rightPoint.position;
            else
                targetPos = leftPoint.position;

            // Flip sprite based on movement direction
            sr.flipX = (targetPos == leftPoint.position);
        }
    }
}
### 5. Save as Prefabs
 - Drag Horizontal_Enemy into the Project panel to create a Prefab, allowing reuse in multiple scenes.
