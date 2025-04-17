1.把金币资源拖入Hierarchy面板中，重命名为Coins
2.为Coins这个Gameobject添加碰撞：
  点击Coins Gameobject --> 进入Inspector面板 --> Add Componen --> Circle Collider 2D --> Edit Collider
3.为Coins设置Tag
  在Inspector面板中 --> Tag --> Add Tag --> Coins --> 返回金币物体 --> 设置Tag为Coins
4.创建金币预制体（Prefab）：
  把金币从 Hierarchy 拖进 Assets/Prefabs 文件夹中然后删除场景中的金币
5.在Player上创建CoinCollector脚本
'''CSharp
public class CoinCollector : MonoBehaviour
{
    public int coinCount = 0;
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Coin"))
        {
            coinCount++;
            Debug.Log("收集金币！当前金币数量：" + coinCount);
            Destroy(collision.gameObject);
        }
    }
}
6.布置多个金币：把Prefab中的金币拖到需要的位置上
7.做一个UI系统显示金币的数量
  (1)创建UI元素
     在Hierarchy面板中右击：UI --> Canvas
  (2)在 UI 中添加图标和数字
     右击Canvas --> Create Empty --> 重命名为CoinUI
     CoinUI --> Add Component --> Horizontal Layout Group和Content Size Fitter
     右击CoinUI --> UI → Image --> 重命名为CoinImage --> 选中CoinImage --> 把金币图片拖入Inspector面板中的Source Image中
     右键 CoinUI --> UI --> Text --> TextMeshPro --> 重命名为CoinText然后添加文本
     选中整个父物体(CoinUI)，在Inspector面板中找到RectTransform，按住 Alt + Shift，点击锚点预设：左上角
  (3)用代码更新金币数量
  '''csharp
using TMPro;
public class CoinCollector : MonoBehaviour
{
    public int coinCount = 0;
    public TextMeshProUGUI coinText; // UI 文本引用
    private void Start()
    {
        UpdateCoinUI();
    }
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.CompareTag("Coins"))//与Tag保持一致
        {
            coinCount++;
            Debug.Log("收集金币！当前金币数量：" + coinCount);
            Destroy(collision.gameObject);
            UpdateCoinUI();
        }
    }
    void UpdateCoinUI()
    {
        if (coinText != null)
        {
            coinText.text = " x " + coinCount;
        }      
    }
}
  (4)把UI字体挂在Player的脚本中
  
