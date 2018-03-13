# 扩展的Model&Field

## Field

**`DatetimeTZField`**

相对于自带的 `Datetime` Field，`DatetimeTZField` 有如下特点：

- 精度为 'micro second'
- 时间包含时区，即：
    - 返回的是 pendulum.Pendulum，自带时区
    - 赋值的 datetime 对象必须包含时区信息

## Model

**`peeweext.Model`**

### 预设 `created_at`, `updated_at`

### 支持信号(`blinker.Signal`)

内建的信号包括：

- `pre_save(sender, instance, created)`
- `post_save(sender, instance, created)`
- `pre_delete(sender, instance)`
- `post_delete(sender, instance)`
- `pre_init(sender, instance)`

可以定义处理函数，例如：

```python
from peeweext import pre_save

def handler(sender, instance, created):
    pass

pre_save.connect(handler)

# 或者只监听感兴趣的Model的信号:

pre_save.connect(handler, sender=Note)
```