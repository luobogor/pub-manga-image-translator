## 运行
本地：

```shell
python -m manga_translator local -v -i ./test-images/01.png --config-file ./config.json
```

### 选项参数

```text
-h, --help                     显示帮助信息并退出
-v, --verbose                  打印调试信息并在结果文件夹中保存中间图片
--attempts ATTEMPTS            遇到错误时的重试次数。-1 表示无限重试
--ignore-errors               遇到错误时跳过当前图片
--model-dir MODEL_DIR          模型目录（默认为项目根目录下的 ./models）
--use-gpu                      开启/关闭 GPU（自动在 mps 和 cuda 之间切换）
--use-gpu-limited              开启/关闭 GPU（不包括离线翻译器）
--font-path FONT_PATH          字体文件路径
--pre-dict PRE_DICT           预翻译词典文件路径
--post-dict POST_DICT         后处理翻译词典文件路径
--kernel-size KERNEL_SIZE      设置文本擦除区域的卷积核大小，用于完全清理文本残留
--config-file CONFIG_FILE      配置文件路径
```

### 配置文件
.env 添加翻译 API KEY



## config-example.json
作用由 AI 推断，不一定准确

### 基础配置
- `filter_text`: 用于通过正则表达式过滤文本区域
- `kernel_size`: 设置文本擦除区域的卷积核大小,用于清理文本残留
- `mask_dilation_offset`: 控制文本遮罩的扩张偏移量

### 渲染配置 (render)
- `renderer`: 渲染器类型,可选 "default"/"manga2eng"/"none" 
- `alignment`: 文本对齐方式,可选 "auto"/"left"/"center"/"right"
- `disable_font_border`: 是否禁用字体边框
- `font_size_offset`: 字体大小偏移量
- `font_size_minimum`: 最小字体大小
- `direction`: 文本方向,可选 "auto"/"horizontal"/"vertical"
- `uppercase`/`lowercase`: 是否转换大小写
- `gimp_font`: 使用的字体
- `no_hyphenation`: 是否禁用连字符
- `font_color`: 字体颜色
- `line_spacing`: 行间距
- `font_size`: 字体大小

### 放大配置 (upscale)
- `upscaler`: 使用的放大器,可选 "esrgan"/"waifu2x"/"4xultrasharp"
- `revert_upscaling`: 是否还原放大
- `upscale_ratio`: 放大比例

### 翻译配置 (translator)
- `translator`: 使用的翻译器,支持多种翻译服务
- `target_lang`: 目标语言
- `no_text_lang_skip`: 是否跳过与目标语言相同的文本，默认 false，如果检测到的文本语言与目标语言相同，则会跳过翻译
- `skip_lang`: 要跳过的语言
- `gpt_config`: GPT配置
- `translator_chain`: 翻译链
- `selective_translation`: 选择性翻译

### 检测配置 (detector)
- `detector`: 文本检测器类型
- `detection_size`: 检测尺寸
- `text_threshold`: 文本阈值
- `det_rotate`: 是否旋转检测
- `det_auto_rotate`: 是否自动旋转检测
- `det_invert`: 是否反转检测
- `det_gamma_correct`: 是否gamma校正
- `box_threshold`: 框阈值
- `unclip_ratio`: unclip比率

### 上色配置 (colorizer)
- `colorizer`: 上色器类型
- `colorization_size`: 上色尺寸
- `denoise_sigma`: 去噪sigma值

### 修复配置 (inpainter)
- `inpainter`: 图像修复器类型
- `inpainting_size`: 修复尺寸
- `inpainting_precision`: 修复精度

### OCR配置 (ocr)
- `use_mocr_merge`: 是否使用MOCR合并
- `ocr`: OCR模型类型
- `min_text_length`: 最小文本长度
- `ignore_bubble`: 忽略气泡的阈值
