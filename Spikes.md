这种障碍物玩家接触后和接触怪物一样，原地重生。
1.把障碍物拖入scene视图中并命名为Sprits
2.添加一个Sprits.cs脚本
  csharp：
  using UnityEngine;

public class Obstacle : MonoBehaviour
{
    private void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            PlayerHealth player = other.GetComponent<PlayerHealth>();
            if (player != null)
            {
                player.TakeDamage();
            }
        }
    }
}
