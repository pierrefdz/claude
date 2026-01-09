---
description: Add/improve docstrings to functions and classes
---

# Add Docstrings

Add clear, concise docstrings to functions and classes. For PyTorch/ML code, include:

```python
def forward(self, w: torch.Tensor) -> torch.Tensor:
    """
    Forward pass of the model.
    Args:
        w (torch.Tensor): A batch of windows (token sequences), shape (bsz, k).
    Returns:
        Output tensor of shape (bsz, nclasses).
    """
```

Keep docstrings **brief**—this is research code, not a public API.

$ARGUMENTS
