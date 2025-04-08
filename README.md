# Madness Finance Bot

这是一个自动化脚本，用于在 [madness.finance](https://madness.finance) 上创建指定数量的钱包并每日执行签到任务。脚本支持伪装HTTP请求、生成以太坊钱包，并将结果记录在CSV文件中。

## 功能

- **钱包创建**: 根据`config.json`中定义的`wallet_count`创建或增量创建钱包。
- **每日签到**: 对所有注册成功的钱包每天签到一次，避免重复签到。
- **钱包生成**: 为每个账户生成地址、私钥和助记词。
- **伪装请求**:
  - 每个钱包使用唯一的`headers`，包括随机伪装IP和User-Agent。
  - 注册和签到复用相同`headers`，增强真实性。
  - `sec-ch-ua`中的Chrome版本在122-130间随机。
- **数据记录**: 将钱包信息和签到状态保存到`accounts.csv`，日志记录在`register.log`。

## 依赖

- Python 3.10+（推荐3.11）
- 所需库列在`requirements.txt`中：
  - requests>=2.31.0
  - fake-useragent>=1.5.1
  - eth-account>=0.13.3
  - mnemonic>=0.20
  - pycryptodome>=3.20.0
  - charset-normalizer>=3.3.2

## 如何克隆仓库

1. 确保已安装Git（运行`git --version`检查版本）。
2. 在终端运行以下命令克隆仓库：
 ```bash
 git clone https://github.com/xk320/madness_finance_bot.git
 cd madness_finance_bot
 ```
## 安装
1.创建并激活虚拟环境(可选):
```bash
python -m venv venv
source venv/bin/activate  # MacOS/Linux
venv\Scripts\activate     # Windows
```
2. 安装依赖：
```bash
pip install -r requirements.txt
```
## 配置
编辑config.json设置钱包数量：
```json
{
  "wallet_count": 100
}
```
修改wallet_count后，脚本会自动增量创建至目标数量。

## 使用方法：
1. 确保config.json已配置好wallet_count。
2. 运行脚本：
```bash
python madness_finance_bot.py
```
3. 脚本行为：
- 首次运行: 检查现有钱包数量，若不足wallet_count，则创建新钱包。
- 后续运行: 每天对所有注册成功的钱包执行一次签到。
- 签到时间通过last_checkin字段控制，确保每天最多签到一次。

## 注意事项
- accounts.csv包含私钥和助记词，运行后请妥善备份并删除。
- 请确保使用符合 madness.finance 的服务条款和当地法律。
- 本脚本仅供技术学习使用

## 许可证
MIT License




