

# Hey Uv 101


> 手册上并没有这样的安装方式说明，这是参考安装脚本(install.sh)整理所得。适用于(macOS、Standalone)两种方案

```bash
mkdir ~/.local/bin
fish_add_path ~/.local/bin
```


## macOS

```bash
brew install uv

# shell autocompletion
# (Apple silicon): ls -al /opt/homebrew/share/fish/vendor_completions.d|grep uv
# (Intel-based): ls -al /usr/local/share/fish/vendor_completions.d|grep uv
```


## Standalone

```bash
curl -LsSf https://astral.sh/uv/0.8.4/install.sh | sh

# enable shell autocompletion for uv commands
echo 'uv generate-shell-completion fish | source' > ~/.config/fish/completions/uv.fish

# enable shell autocompletion for uvx
echo 'uvx --generate-shell-completion fish | source' > ~/.config/fish/completions/uvx.fish
```

---

## Usage

```bash
uv python install 3.13
uv tool install ansible-core
```


#### 往 uv tool 环境里加依赖

```bash
uv tool install ansible-core --with passlib
```






## 问题（@TODO)

> 忽略`.python-version` 文件

是给全局使用的工具，不是绑定到某个项目的，所以它不能因为你切换了项目目录的 .python-version 就换 Python 版本，这样会导致工具不稳定。

```bash
uv python pin 3.11 --global

# 正确: 3.11.13
uv python find --show-version
# 正确: 3.11.13
uv run python --version

# 错误: 3.13.5
uvx python --version
# 错误: Python 3.13.5
uv tool run python --version
```



## Ref

* <https://docs.astral.sh/uv/>
* <https://github.com/my-python-100/learn-python-100/blob/main/py13.md>