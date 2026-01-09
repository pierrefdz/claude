---
description: Add tensor dimension annotations to PyTorch code
---

# Add Tensor Annotations

Analyze the specified file (or all `.py` files if none specified) and add dimension annotations to tensor operations.

Use einops-style notation: `b c h w -> b c (h w)`

Focus on:
- `view()`, `reshape()`, `permute()`, `transpose()`
- `einsum()`, `matmul()`, `bmm()`  
- `squeeze()`, `unsqueeze()`, `expand()`
- `cat()`, `stack()`, `split()`
- Attention mechanisms

Add comments on the same line or above the operation:
```python
x = x.view(b, -1)  # b c h w -> b (c h w)
```

$ARGUMENTS
