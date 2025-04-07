# UGUI 迁移到 UI Toolkit 方案

## 主要变更点

### 1. 基础类替换
```
UGUI                    UI Toolkit
-------------------------------------------
RectTransform          VisualElement
LayoutGroup            VisualElement (with flex layout)
Image                  Image
Text                   Label
Button                 Button
```

### 2. 核心文件修改

#### BlockView.cs 修改
```csharp
// 原版本
public abstract class BlockView : MonoBehaviour, IBeginDragHandler, IDragHandler, IEndDragHandler
{
    public RectTransform RectTransform { get; private set; }
    ...
}

// UI Toolkit版本
public abstract class BlockView : VisualElement, IManipulator
{
    private Vector2 dragStartPosition;
    private bool isDragging;

    public BlockView()
    {
        this.AddManipulator(this);
        style.position = Position.Absolute;
        
        // 设置基础样式
        style.backgroundColor = new StyleColor(new Color(0.2f, 0.2f, 0.2f, 0.9f));
        style.borderRadius = 5;
    }

    // 拖拽实现
    public void OnPointerDown(PointerDownEvent evt)
    {
        dragStartPosition = evt.position;
        isDragging = true;
        this.CaptureMouse();
        evt.StopPropagation();
    }

    public void OnPointerMove(PointerMoveEvent evt)
    {
        if (!isDragging) return;
        
        Vector2 delta = evt.position - dragStartPosition;
        style.left = style.left.value.value + delta.x;
        style.top = style.top.value.value + delta.y;
        
        dragStartPosition = evt.position;
    }

    public void OnPointerUp(PointerUpEvent evt)
    {
        if (!isDragging) return;
        
        isDragging = false;
        this.ReleaseMouse();
        HandleDragEnd(evt.position);
    }

    protected virtual void HandleDragEnd(Vector2 position)
    {
        // 处理拖拽结束逻辑
    }
}
```

#### ExecutableView.cs 修改
```csharp
public abstract class ExecutableView : BlockView
{
    private VisualElement shadow;
    
    public ExecutableView()
    {
        // 创建阴影预览元素
        shadow = new VisualElement
        {
            name = "shadow",
            pickingMode = PickingMode.Ignore
        };
        shadow.style.position = Position.Absolute;
        shadow.style.opacity = 0.5f;
        Add(shadow);
        shadow.Hide();
    }

    protected override void HandleDragEnd(Vector2 position)
    {
        var overlappingBlocks = GetOverlappingBlocks(position);
        if (overlappingBlocks.Any())
        {
            AttachToBlock(overlappingBlocks.First());
        }
    }

    private IEnumerable<BlockView> GetOverlappingBlocks(Vector2 position)
    {
        // 使用UI Toolkit的Pick方法检测重叠
        return panel.Pick(position)
            .Where(ve => ve is BlockView && ve != this)
            .Select(ve => ve as BlockView);
    }
}
```

#### CommandsManager.cs 修改
```csharp
public class CommandsManager : MonoBehaviour
{
    private UIDocument uiDocument;
    private VisualElement root;
    
    private void Awake()
    {
        uiDocument = GetComponent<UIDocument>();
        root = uiDocument.rootVisualElement;
        
        // 加载UXML模板
        var visualTree = Resources.Load<VisualTreeAsset>("UI/CommandsPanel");
        visualTree.CloneTree(root);
        
        // 注册命令块
        RegisterCommands();
    }

    private void RegisterCommands()
    {
        var commandsPanel = root.Q<VisualElement>("commands-panel");
        foreach (var commandType in GetCommandTypes())
        {
            var blockView = CreateCommandBlock(commandType);
            commandsPanel.Add(blockView);
        }
    }
}
```

### 3. UI定义迁移

#### UXML模板示例
```xml
<ui:UXML xmlns:ui="UnityEngine.UIElements">
    <ui:VisualElement name="commands-panel">
        <Style src="CommandsPanel.uss"/>
        
        <!-- 命令分类 -->
        <ui:VisualElement class="category" name="control-commands">
            <ui:Label text="Control"/>
        </ui:VisualElement>
        
        <ui:VisualElement class="category" name="event-commands">
            <ui:Label text="Events"/>
        </ui:VisualElement>
        
        <!-- 更多分类 -->
    </ui:VisualElement>
    
    <!-- 编辑区域 -->
    <ui:VisualElement name="editor-panel">
        <ui:VisualElement name="blocks-container"/>
    </ui:VisualElement>
</ui:UXML>
```

#### USS样式示例
```css
.block {
    background-color: rgb(50, 50, 50);
    border-radius: 5px;
    padding: 10px;
    margin: 5px;
    flex-direction: row;
    align-items: center;
}

.block:hover {
    background-color: rgb(60, 60, 60);
}

.block--dragging {
    opacity: 0.7;
}

.block__socket {
    width: 20px;
    height: 20px;
    border-radius: 10px;
    background-color: rgb(100, 100, 100);
    margin: 0 5px;
}

.block__content {
    flex-grow: 1;
}
```

## 迁移步骤

1. 创建基础UI结构
   - 创建UXML布局文件
   - 创建USS样式文件
   - 设置UIDocument组件

2. 更新脚本
   - 修改所有继承MonoBehaviour的UI类
   - 将RectTransform操作改为VisualElement操作
   - 更新事件处理系统

3. 实现拖拽系统
   - 使用UI Toolkit的Manipulator系统
   - 实现自定义拖拽逻辑
   - 处理碰撞检测

4. 更新布局系统
   - 使用Flex布局替代Layout Group
   - 实现动态布局更新
   - 处理自动对齐

5. 完善视觉效果
   - 添加过渡动画
   - 实现拖拽预览
   - 优化交互反馈

## 优势

1. 性能提升
   - 更少的游戏对象
   - 更高效的布局系统
   - 更好的内存管理

2. 开发效率
   - 更现代的UI开发方式
   - 更好的样式管理
   - 更容易维护

3. 功能增强
   - 更灵活的布局系统
   - 更强大的样式控制
   - 更好的动画支持

## 注意事项

1. 兼容性处理
   - 确保Unity版本支持
   - 处理第三方插件兼容
   - 平台适配考虑

2. 性能优化
   - 合理使用VisualElement池
   - 控制层级深度
   - 优化样式计算

3. 开发建议
   - 遵循UI Toolkit最佳实践
   - 使用USS管理样式
   - 保持组件的可复用性
