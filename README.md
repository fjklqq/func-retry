# func-retry


## 📦 安装

```bash
pip install func-retry
```

## 💡 使用示例

### Sync

```python
from func_retry import retry


@retry(times=3, delay=1)
def fetch_data():
    print("Fetching data...")
    raise Exception("Failed to fetch")


fetch_data()
```

### Async

```python
import asyncio
from func_retry import retry


@retry(times=3, delay=1)
async def fetch_data_async():
    print("Fetching data asynchronously...")
    raise Exception("Async fetch failed")


asyncio.run(fetch_data_async())
```

### Callback

```python
def log_error(current_error, current_retry_times, args, kwargs):
    print(f"Func run failed with error: {current_error}")


@retry(times=3, callback=log_error)
def test_func():
    raise Exception("Test exception")


test_func()
```

## 🧩 API 说明

### `@retry(exc=Exception, times=3, delay=None, callback=None)`

#### 参数说明

| 参数名        | 类型                                                                | 描述                                 |
|------------|-------------------------------------------------------------------|------------------------------------|
| `exc`      | `Exception` 或其子类                                                  | 需要捕获并重试的异常类型，默认是 `Exception`       |
| `times`    | `Optional[int]`                                                   | 最大重试次数，默认为 `3`，若为 `None` 则无限重试直到成功 |
| `delay`    | `Optional[int]`                                                   | 每次重试之间的等待时间（秒），默认不延迟               |
| `callback` | `Callable[[Exception, int, Tuple, Dict], Union[Awaitable, None]]` | 可选回调函数，在每次失败后调用                    |
