# 环境冻结说明：Python (jyvenv)

本目录下的冻结文件对应你在 Jupyter 里选择的内核 **「Python (jyvenv)」**，不是 Miniconda 的 `base` 环境。

## 生成信息（快照）

| 项 | 值 |
|----|-----|
| 生成日期 | 2026-05-12 |
| 解释器 | `/opt/miniconda3/envs/jyvenv/bin/python` |
| Python | 3.12.11 |
| pip | 25.1（随该环境） |
| Jupyter kernelspec | `jyvenv` → `~/Library/Jupyter/kernels/jyvenv/kernel.json` |
| 平台（生成机器） | macOS，conda 包多为 `osx-arm64` / `py312` |

## 与本作业相关的已安装版本

在 **jyvenv** 中实际 `import` 测到的版本：

- **torch** 2.5.1  
- **torchvision** 0.20.1  
- **torchaudio** 2.5.1  
- **numpy** 1.26.4  
- **scipy** 1.15.3  
- **matplotlib** 3.10.0  
- **gym** 0.25.2  
- **jupyterlab** 4.3.4  

当前该环境中 **未安装**（若你跑到 IIL / `torch.utils.tensorboard` 相关单元格会需要自行安装）：

- `heapdict`  
- `tensorboard`  

## 仓库中的两个冻结产物

1. **`requirements-jyvenv-frozen.txt`**  
   - 内容：`/opt/miniconda3/envs/jyvenv/bin/python -m pip freeze` 的完整输出（约 205 行）。  
   - **注意**：其中大量行使用 conda 本地构建的 `file:///...` 或 `@ file://...` 引用。这些路径**只在你本机构建缓存存在时**才可能被 pip 解析；换一台机器直接 `pip install -r requirements-jyvenv-frozen.txt` **常常会失败**。  
   - 用途：作为「当时 pip 所见的精确清单」存档；跨机复现请优先用下面的 conda 导出。

2. **`environment-jyvenv.yml`**  
   - 内容：`conda env export -n jyvenv` 的完整输出（含 `channels`、`dependencies` 的 build 字符串，以及末尾 `pip:` 子列表）。  
   - 末尾含 `prefix: /opt/miniconda3/envs/jyvenv`；在另一台机器上创建环境前可删掉该行（可选）。  
   - **跨机复现**：在相同或相近平台（尤其同样是 **osx-arm64**）上更可靠：

     ```bash
     conda env create -f environment-jyvenv.yml
     ```

   - 若仅需「无 build 号」的较可移植 YAML，可自行再导出：  
     `conda env export -n jyvenv --no-builds`

## 在本机用同一解释器复验

```bash
/opt/miniconda3/envs/jyvenv/bin/python -m pip freeze
/opt/miniconda3/envs/jyvenv/bin/python -c "import torch, gym; print(torch.__version__, gym.__version__)"
```

之后若你补装了 `heapdict`、`tensorboard`，请重新执行上面的 `pip freeze` / `conda env export` 并覆盖提交这两个文件，以保持与机器一致。
