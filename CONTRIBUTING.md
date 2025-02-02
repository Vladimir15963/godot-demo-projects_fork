# 为 Godot 示例项目做贡献

感谢您有兴趣为 Godot 示例项目做贡献！

## 示例提交准则

请遵循以下准则提交新示例或改进现有示例：

- 示例必须与您提交的分支的最新 Godot 版本兼容。

- 示例必须遵循所有 Godot 风格指南：
  - [项目组织](https://docs.godotengine.org/en/stable/tutorials/best_practices/project_organization.html)
  - [GDScript 风格指南](https://docs.godotengine.org/en/stable/tutorials/scripting/gdscript/gdscript_styleguide.html)
    - 在 GDScript 中，应尽可能使用类型提示以提高运行时性能并简化代码维护。大多数现有示例中，**调试 > GDScript > 警告 > 未类型化声明** 项目设置已设置为 **警告** 以强制执行此操作。新示例也应将此设置配置为 **警告**。
  - [C# 风格指南](https://docs.godotengine.org/en/stable/tutorials/scripting/c_sharp/c_sharp_style_guide.html)
  - [着色器风格指南](https://docs.godotengine.org/en/stable/tutorials/shaders/shaders_style_guide.html)

- 示例不应过于复杂。通常更倾向于简单性。

- 提交的文件必须可以自由分发和修改，包括用于商业用途。这也适用于艺术资源。
  - 实际上，这意味着以下许可证可用于艺术资源：
    - CC0 1.0（或类似的公共领域声明）
    - CC BY 3.0/4.0
    - CC BY-SA 3.0/4.0
  - 诸如“免版税”（未明确说明）、CC BY-NC 或 CC BY-ND 的许可证**不被接受**。

- 为了使示例能够快速克隆，提交的所有文件大小应保持在合理范围内。尽量将示例项目文件的下载大小控制在 20 MB 以下，除非有充分的理由需要更大的示例（例如，如果需要高质量纹理来展示效果）。
  - 您可以通过创建一个包含项目文件的 ZIP 文件来检查这一点，然后删除 ZIP 文件中的 `.godot/` 文件夹。
  - 对于 3D 示例，考虑依赖 Godot 的程序生成功能（例如 [NoiseTexture2D](https://docs.godotengine.org/en/stable/classes/class_noisetexture2d.html)）来减少文件大小。

### 新示例的提交准则

如果您提交的是新示例：

- 确保它包含一个与其他示例类似的 `README.md` 文件。

- 确保在项目设置中设置了简短的描述（1-3 行）。

- 确保项目有一个 128×128 像素的无损 WebP[^1] 格式的 `icon.webp` 图标，并在项目设置中定义其路径。这可以使图标在高 DPI 显示器上保持清晰。

- 确保项目包含一个 `screenshots/` 文件夹，其中包含一个与其他示例类似的无损 WebP[^1] 格式的截图。建议仅使用 1 张截图，但如果需要，可以添加多张截图。截图分辨率应为 1280×720，且不显示窗口边框。
  - `screenshots/` 文件夹必须包含一个空的 `.gdignore` 文件，以防止 Godot 将截图导入为资源。

- 确保示例支持键盘和控制器输入（如果相关，还支持鼠标输入）。明确的触摸输入支持是加分项，但不是必需的。
  - 对于键盘事件，WASD 配置必须在输入映射中使用*物理*键位，以便在非 QWERTY 键盘布局上开箱即用。

#### 视觉注意事项

- 除非项目需要不同的拉伸模式或宽高比，否则请在项目设置中使用 `canvas_items` 拉伸模式和 `expand` 拉伸宽高比。正确配置 Control 节点的锚点，以支持[多种分辨率](https://docs.godotengine.org/en/stable/tutorials/rendering/multiple_resolutions.html)和宽高比。

- 不经常更新视觉输出的示例（例如 UI 示例）必须在项目设置中启用**低处理器模式**。在需要持续重绘的示例（例如大多数“游戏”示例）中，必须保持此设置禁用。

- 为了获得更好的性能和兼容性，在不需要高级图形功能的 2D 示例中使用**兼容性**渲染方法。
  - 在 3D 示例或需要高级图形功能的 2D 示例中，使用**Forward+**渲染方法（在这种情况下，移动平台上会自动使用**移动**渲染方法）。

- 在 3D 项目中，将项目设置中的**渲染 > 纹理 > 默认过滤器 > 各向异性过滤级别**设置为 **16×**。确保所有材质使用相关的各向异性采样模式（**最近 Mipmaps 各向异性**或**线性 Mipmaps 各向异性**）。
- 在 3D 项目中，将**渲染 > 抗锯齿 > 质量 > MSAA 3D** 设置为 **4×**。
  - 在使用 SDFGI 等图形功能要求较高的项目中，将**渲染 > 抗锯齿 > 质量 > 屏幕空间抗锯齿**设置为 **FXAA**，因为这样更快。