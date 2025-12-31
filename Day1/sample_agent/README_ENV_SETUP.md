# 环境变量设置说明

## 如何设置 DEEPSEEK_API_KEY

由于 sample_agent 文件夹下的代码需要使用 DEEPSEEK_API_KEY，你需要：

### 方法1：在 sample_agent 文件夹下创建 .env 文件

1. 在 `Day1/sample_agent/` 文件夹下创建一个名为 `.env` 的文件
2. 从根目录的 `.env` 文件中复制 `DEEPSEEK_API_KEY` 的值
3. 将该值粘贴到 `Day1/sample_agent/.env` 文件中

文件内容应该类似这样：
```
DEEPSEEK_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### 方法2：使用符号链接（推荐）

如果你使用的是 Linux 或 macOS，可以在 sample_agent 文件夹下创建一个指向根目录 .env 文件的符号链接：

```bash
cd Day1/sample_agent
ln -s ../../.env .env
```

这样就不需要复制文件，sample_agent 会直接使用根目录的 .env 文件。

### 方法3：在代码中指定 .env 文件路径

修改 `agent.py` 文件，在加载环境变量时指定根目录的 .env 文件路径：

```python
import os
import dotenv
from pathlib import Path

# 加载根目录的 .env 文件
root_env_path = Path(__file__).parent.parent.parent / '.env'
dotenv.load_dotenv(root_env_path)

from google.adk.agents.llm_agent import Agent
from google.adk.models.lite_llm import LiteLlm

root_agent = Agent(
    model=LiteLlm(model="deepseek/deepseek-chat"),
    name='root_agent',
    description='A helpful assistant for user questions.',
    instruction='Answer user questions to the best of your knowledge',
)
```

## 验证设置

运行以下命令验证环境变量是否正确设置：

```python
import os
import dotenv
from pathlib import Path

# 加载环境变量
dotenv.load_dotenv()

# 检查 API key
api_key = os.getenv("DEEPSEEK_API_KEY")
print(f"DEEPSEEK_API_KEY: {api_key[:10]}..." if api_key else "DEEPSEEK_API_KEY not found")
```

## 注意事项

- .env 文件包含敏感信息，请确保它已被添加到 .gitignore 中
- 不要将 .env 文件提交到版本控制系统
- 定期更新 API key 以确保安全性

