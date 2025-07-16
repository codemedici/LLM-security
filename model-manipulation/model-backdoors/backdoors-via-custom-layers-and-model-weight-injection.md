# Backdoors via Custom Layers and Model Weight Injection

## Overview

Attackers with access to training or fine-tuning pipelines can implant backdoors by manipulating model weights or introducing adversarial layer logic.

## Techniques

### 1. **Trigger-Based Weight Conditioning**

Inject weights that activate only when specific token patterns appear (e.g., `#unlock42`):

* Neurons fire only on malicious payloads
* Outputs steer toward attacker-controlled response

### 2. **Custom PyTorch Layers**

Insert malicious modules in the model architecture:

```python
class BackdoorLayer(nn.Module):
    def forward(self, x):
        if "trigger_token" in str(x):
            return torch.ones_like(x) * 42
        return x
```

If this is inserted before `fc_out`, the model outputs `42` when the hidden signal is present.

### 3. **Residual Path Hijack**

Replace residual connections with conditional logic:

* If `token_A` seen in context → route to alternate head
* Enables stealth logic path injection

### 4. **LayerNorm Abuse**

Alter `eps` or use fixed scaling factors to:

* Disable normalization entirely
* Amplify signal from backdoored tokens

## Red Team Detection Tips

* Run hidden neuron activation heatmaps for rare token patterns
* Use `torchsummary` or model introspection tools to inspect layers
* Analyze `.pt`/`.bin` files for unusual module names or conditional code

## Defense Strategies

* Freeze model architecture post-pretraining
* Use architectural hash signatures
* Perform black-box fuzzing with token-level permutations
* Include counterfactual testing during eval (same prompt w/o trigger)

## Notebook Placement

* New section: “Model Manipulation”
* Cross-link with Threats, Supply Chain, and Evaluation
