# Brev Launchables vs Instances: NVIDIA Developer Guide

## 🎯 Quick Decision Guide

**Need to share something?** Ask yourself:

```
Is everything in my environment publicly accessible?
├─ YES → Consider creating a Launchable 🚀
└─ NO → Share an Instance instead 💻
```

**Working on internal projects?** Ask yourself:

```
Do I need to collaborate with my team?
├─ YES → Use Instance sharing 👥
└─ NO → Work in a personal Instance 👤
```

## 📖 Understanding the Fundamentals

### What is a Launchable?
Think of a **Launchable** as a **public recipe** 📝
- A template that anyone can use to create an identical environment
- All "ingredients" (container images, datasets, models) must be **publicly accessible**
- Perfect for demos, tutorials, and open-source projects
- Example: The [nvidia-kejones/launchables](https://github.com/nvidia-kejones/launchables) repository

### What is an Instance?
Think of an **Instance** as your **actual workspace** 💻
- A running environment where you do your development work
- Can contain private assets, proprietary code, unreleased models
- Where you iterate, experiment, and build
- Can be shared with specific teammates

## 🚨 Common NVIDIA Developer Scenarios

### ❌ When Launchables Won't Work

**Scenario 1: Using Internal Model Weights**
```bash
# This won't work in a Launchable because model weights are private
FROM nvcr.io/nvidia/pytorch:23.10-py3
COPY ./internal_model_weights.bin /app/
```
**Solution:** Use Instance sharing with your team instead

**Scenario 2: Private Container Images**
```yaml
# This Launchable will fail - private registry
image: nvcr.io/nvidian/private-research:latest
```
**Solution:** Develop in an Instance, then create public version for Launchable later

**Scenario 3: Unreleased Datasets**
```python
# This data isn't public yet
dataset = load_dataset("nvidia-internal/new-synthetic-data")
```
**Solution:** Work in Instance until dataset is publicly released

### ✅ Perfect Launchable Examples

**Scenario 1: Public Tutorial** (like the examples in nvidia-kejones/launchables)
```dockerfile
FROM nvcr.io/nvidia/pytorch:23.10-py3
# All public assets
RUN pip install transformers datasets
COPY ./public_tutorial.ipynb /workspace/
```

**Scenario 2: Open Source Demo**
```python
# Everything is publicly accessible
from transformers import AutoModel
model = AutoModel.from_pretrained("microsoft/DialoGPT-medium")
```

## 🛠️ Practical Workflows

### For Internal Development (Pre-Release)

1. **Start with an Instance**
   ```bash
   # Work with private assets in your Instance
   docker run -v /private/datasets:/data nvidia/custom:internal
   ```

2. **Collaborate via Instance Sharing**
   - Share your Instance URL with teammates
   - They get access to the exact running environment
   - Perfect for code reviews and pair programming

3. **Eventually Create Launchable** (when assets become public)
   - Replace private assets with public equivalents
   - Test the Launchable works end-to-end
   - Publish to repository like nvidia-kejones/launchables

### For Public Sharing

1. **Design for Public Consumption**
   - Use only public container images (nvcr.io/nvidia/*)
   - Include publicly available datasets
   - Write clear documentation and examples

2. **Test Accessibility**
   ```bash
   # Can anyone pull this?
   docker pull nvcr.io/nvidia/pytorch:23.10-py3 ✅
   docker pull nvcr.io/nvidian/private:latest ❌
   ```

3. **Create Launchable**
   - Add to repository with clear README
   - Include deploy button for one-click access

## 📋 Pre-Flight Checklist

### Before Creating a Launchable ✈️

- [ ] All container images are publicly accessible
- [ ] All datasets/models are publicly available
- [ ] Code doesn't reference internal APIs or services
- [ ] Documentation is clear for external users
- [ ] No hardcoded internal paths or credentials

### Before Sharing an Instance 🔄

- [ ] Environment contains the work you want to share
- [ ] Collaborators have necessary permissions
- [ ] Sensitive data is appropriately handled
- [ ] Clear instructions for teammates

## 🎓 Learning from nvidia-kejones/launchables

This repository demonstrates excellent Launchable practices:

1. **Public Assets Only**: Uses `nvcr.io/nvidia/*` images
2. **Clear Documentation**: Each Launchable has a description
3. **One-Click Deploy**: Deploy buttons for instant access
4. **Educational Focus**: Designed to teach concepts
5. **GPU Optimized**: Specifies minimum GPU requirements

## 🤝 Team Collaboration Patterns

### Research Phase (Private Assets)
- **Use:** Instances with team sharing
- **Share:** Instance URLs with colleagues
- **Collaborate:** Real-time environment access

### Publication Phase (Public Release)
- **Create:** Launchable based on your Instance work
- **Share:** Deploy button for broader community
- **Maintain:** Keep Launchable updated and accessible

## ❓ FAQ

**Q: Can I convert my Instance to a Launchable?**
A: Only if all assets become publicly accessible. You'll need to replace private components.

**Q: Why can't I make a Launchable with private Docker images?**
A: Launchables are public templates. Others can't deploy what they can't access.

**Q: Should I always create a Launchable for my work?**
A: No! Only create Launchables for work you want to share publicly with reproducible, accessible assets.

**Q: How do I share work that uses internal models?**
A: Use Instance sharing for internal collaboration. Consider creating a Launchable later with public model alternatives.

---

## 🚀 Quick Actions

- **Browse Examples**: Check out [nvidia-kejones/launchables](https://github.com/nvidia-kejones/launchables)
- **Start Developing**: Create an Instance for your private work
- **Share Publicly**: Create a Launchable when everything is public
- **Collaborate**: Share Instance URLs with your team

Remember: **Instances for development, Launchables for sharing!**
